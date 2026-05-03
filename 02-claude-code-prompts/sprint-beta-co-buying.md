# Sprint β — Co-buying flow end-to-end

*Paste this into the new Claude Code chat AFTER the handoff orientation prompt has been read AND the digest 1829522191 bug has been fixed and verified. Do not start this sprint until those prerequisites are done.*

---

# Sprint β — Co-buying flow

## Why this sprint matters

Co-buying is the moat product. Without it, TruePlots is "verified 99acres" — better trust layer, but nothing structurally new. The 3-buyer-advance fractional facilitation is the legal and operational innovation that no competitor (NoBroker, MagicBricks, Farmland Bazaar, Saptashwa, Swasya) has shipped at scale in India. Read `/docs/trueplots-project-document-v4.md` sections 3.2-3.4 and the Glossary's "3-buyer advance" entry before writing any code.

The mechanic in plain English:

1. A plot is too large for a single buyer (e.g., a ₹1.5Cr 7-acre Mandya farmland that the largest buyer segment at ₹40-60L cannot afford alone)
2. Three buyers each commit a small advance (₹5,000) on a specific slice (e.g., 2.3 acres each)
3. Once all three slots are filled, Delight Eco Farms acquires the entire plot using its own balance-sheet capital
4. TruePlots executes legal subdivision: revenue department for farmland (sub-survey numbers + new RTC) or BBMP khata bifurcation for urban
5. Final sale deeds go directly from Delight to each buyer at the published per-slice price
6. Each buyer ends up with an individually-titled parcel (own RTC, own khata)

What this is NOT:
- Not pooled investment (would trigger SEBI CIS regulation — Growpital was shut down by SEBI in 2024 for exactly this; TruePlots is engineered around that failure mode)
- Not co-ownership (no shared title — each buyer has their own deed)
- Not fractional shares in an SPV (no securities; physical land directly to each buyer)

The buyer-facing flow has to communicate this clearly: customer funds never pool, no coordination risk, you walk out with your own khata. The legal cleanliness is the product feature.

## Scope

By the end of this sprint, a buyer can:

1. Browse co-buy-eligible plots on `/farmland` (filtered by a "Co-buy ready" toggle)
2. View a co-buy-eligible plot's LDP and see the 3-slot picker showing current commitment status
3. Select a specific slice (e.g., "Slice B — 2.3 acres, north portion") and commit ₹5,000 advance to that slot
4. See live commitment status: "1 of 3 slots committed", "2 of 3 slots committed", etc.
5. See anonymized co-buyer information: "Slot 1: Buyer A · Bangalore · committed 3 days ago"
6. When all three slots fill, see a "fully committed" state with subdivision progress timeline
7. From `/account/co-buys`, track all their active co-buy commitments across plots
8. Receive (stub) WhatsApp notifications at status milestones

The admin can:

1. View all active co-buys at `/admin/co-buys` with full status across the pipeline
2. Manually advance subdivision stage for any co-buy
3. See full buyer details (admin sees real names; buyers see anonymized labels)
4. Approve/reject withdrawal requests
5. See expected vs actual subdivision timelines

Out of scope this sprint:
- Real Razorpay payment for the ₹5,000 advance (stub: mark `co_buy_commitments.status = 'committed'` directly without payment flow)
- Real WhatsApp notification sending (stub the API call but don't actually send)
- Urban 60×40 → 30×40 split flow (this is 2-buyer; ship the 3-buyer farmland flow first, urban is conditional on month-4 gates anyway)
- Subdivision document generation (PDF deeds — that's Sprint δ when we have a PDF generator)
- Agent commission calculation on co-buy closings (Sprint γ)

## Schema additions

### Co-buy parcel definition (per-listing slot config)

Listings already have an `is_cobuy_eligible` flag (or similar — verify the existing column name). Add a `co_buy_config` JSONB column on `listings`:

```sql
alter table listings add column if not exists co_buy_config jsonb;
-- Structure:
-- {
--   slots: [
--     { id: 'A', label: 'North slice', acres: 2.3, price: 5400000, position: 'north' },
--     { id: 'B', label: 'East slice', acres: 2.4, price: 5640000, position: 'east' },
--     { id: 'C', label: 'South-west slice', acres: 2.3, price: 5400000, position: 'south-west' }
--   ],
--   advance_per_slot: 500000,  -- ₹5,000 in paise
--   subdivision_estimated_weeks: 16,
--   total_acres: 7.0,
--   total_price: 16500000  -- ₹1.65 Cr in paise
-- }
```

The slot count is configurable per listing (3 for farmland default, 2 for urban 60×40 splits). Slots can have different acreage and price (corner plots are typically more valuable).

### Co-buy commitments (one per slot per active deal)

```sql
create type co_buy_commitment_status as enum (
  'open',          -- slot available
  'committed',     -- buyer paid advance, waiting for siblings
  'withdrawn',     -- buyer withdrew before fill (5-day window)
  'locked',        -- all 3 slots committed, ready for Delight acquisition
  'acquired',      -- Delight acquired the parent plot
  'subdividing',   -- subdivision in progress with revenue department
  'titled',        -- final deed registered, buyer has individual title
  'closed'         -- deal complete
);

create table co_buys (
  id uuid primary key default gen_random_uuid(),
  listing_id uuid not null references listings(id) on delete cascade,
  status co_buy_commitment_status not null default 'open',
  slots_total integer not null default 3,
  slots_committed integer not null default 0,
  acquired_at timestamptz,
  delight_acquisition_amount integer,  -- in paise, after Delight buys
  subdivision_started_at timestamptz,
  subdivision_completed_at timestamptz,
  expected_completion_date date,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now(),
  unique (listing_id)  -- one active co-buy per listing
);

create table co_buy_commitments (
  id uuid primary key default gen_random_uuid(),
  co_buy_id uuid not null references co_buys(id) on delete cascade,
  buyer_user_id uuid references auth.users(id),  -- nullable if anonymous (signed up later)
  buyer_name text,  -- anonymized public label like "Buyer A · Bangalore" stored separately
  buyer_phone text,
  buyer_email text,
  buyer_city text,
  slot_id text not null,  -- 'A', 'B', or 'C' (matching co_buy_config.slots[].id)
  slot_acres numeric(5,2) not null,
  slot_price integer not null,  -- in paise
  advance_amount integer not null default 500000,  -- ₹5,000 in paise
  advance_status text not null default 'pending_offline', -- same pattern as reservations
  status co_buy_commitment_status not null default 'committed',
  committed_at timestamptz not null default now(),
  withdrawn_at timestamptz,
  withdrawal_reason text,
  unique (co_buy_id, slot_id)  -- one committed buyer per slot
);

create index co_buys_listing_idx on co_buys(listing_id);
create index co_buys_status_idx on co_buys(status);
create index co_buy_commitments_buyer_idx on co_buy_commitments(buyer_user_id);
```

### RLS

```sql
-- co_buys table: public read (anyone browsing the LDP can see status), admin write
alter table co_buys enable row level security;
create policy co_buys_public_read on co_buys for select using (true);
create policy co_buys_admin_write on co_buys for all using (
  exists(select 1 from profiles where id = auth.uid() and role = 'admin')
);

-- co_buy_commitments: buyers see their own, admins see all, anonymous public sees aggregate count + anonymized labels (no phone/email/buyer_user_id)
alter table co_buy_commitments enable row level security;
create policy commits_own on co_buy_commitments for all using (auth.uid() = buyer_user_id);
create policy commits_admin on co_buy_commitments for select using (
  exists(select 1 from profiles where id = auth.uid() and role = 'admin')
);
create policy commits_aggregate_public on co_buy_commitments for select using (true);  -- but only via a view that strips PII, see below
```

### Anonymized public view

Create a view `co_buy_commitments_public` that exposes only:
- co_buy_id
- slot_id
- slot_acres
- slot_price
- public_label (e.g., "Buyer A · Bangalore" — derived from city + sequential letter)
- status
- committed_at

PII (name, phone, email, buyer_user_id) is hidden.

LDP queries against this view, never the raw table.

## UI surfaces

### 1. Listings page filter — "Co-buy ready" toggle

Existing `/farmland` page already has a "Co-buy eligible" toggle. Verify it filters correctly. If broken, fix.

When toggled, show only listings where `is_cobuy_eligible = true` AND `co_buys.status IN ('open', 'committed')` (i.e., still has open slots).

Add a subtle badge to listing cards when co-buy is active: "Co-buy ready · 1 of 3 committed" in Harvest Gold. Updates live as commitments come in (revalidate on commit).

### 2. LDP — Co-buy section (replaces/augments existing right-rail Reserve CTA on co-buy-eligible plots)

When `listings.is_cobuy_eligible = true`, the LDP right rail changes:

Above the existing Reserve CTA, add a new section "Co-buy this plot":

```
CO-BUY THIS PLOT
Three buyers, three khatas. Delight acquires; we subdivide.

[Slot A — 2.3 acres · ₹54L]    [Slot B — 2.4 acres · ₹56L]    [Slot C — 2.3 acres · ₹54L]
[ Available ]                   [ Buyer A · Bangalore ]         [ Available ]
                                committed 3 days ago

  1 of 3 slots committed · expected subdivision in 16 weeks

[ Commit to a slot — ₹5,000 advance ]
```

If a slot is taken by the current viewer (logged-in buyer), show "Your slot" instead of the anonymized label, with a "Withdraw" link.

The "Reserve this whole plot" CTA still exists below for buyers who want the entire parcel. Whichever fills first wins; if all 3 co-buy slots commit, the whole-plot reserve becomes unavailable.

### 3. `/plot/[slug]/co-buy` — slot picker page

When user clicks "Commit to a slot", route to this dedicated commit flow:

#### Step 1 — Slot selection

Visual representation of the 3 slots overlaid on the plot's survey sketch (or satellite imagery). Each slot is a colored region: green for available, gold for already-committed, blue for current selection.

Below: list view of slots with details (acres, price, advance, what's included).

CTA: "Continue with [selected slot]"

#### Step 2 — Buyer details

Same as Reserve flow Step 2: name, phone, OTP stub, email, city. If the buyer is logged in, prefill from their profile.

#### Step 3 — Co-buy terms

This is critical for the legal-cleanliness positioning. Display the terms clearly:

```
What you're agreeing to

✓ Your ₹5,000 advance holds Slot {X} for 30 days while we wait for two co-buyers
✓ If we don't get three committed buyers within 30 days, your ₹5,000 is fully refunded
✓ Once three buyers commit, Delight Eco Farms acquires the entire plot using its own
  capital — your money is never pooled with the other buyers
✓ You sign a sale deed directly with Delight for your slot — Delight is the seller of
  record, not us, not the other buyers
✓ TruePlots handles the legal subdivision (revenue department, sub-survey numbers,
  new RTC). Estimated 16 weeks from acquisition to your individual title.
✓ At closing, you pay {slot_price - advance} via bank transfer to Delight. Final khata
  in your name.
```

Terms checkbox: "I understand the legal structure and confirm my commitment".

CTA: "Confirm commitment". On click:
- Insert row into `co_buy_commitments` with `status = 'committed'`, `advance_status = 'pending_offline'`
- Increment `co_buys.slots_committed`
- If `slots_committed = slots_total`, update `co_buys.status` to `'locked'` and trigger admin notification
- Advance to Step 4

(No actual payment this sprint. The "pending_offline" status means Kushal collects the ₹5,000 via WhatsApp/bank transfer offline, same as reservations.)

#### Step 4 — Confirmation

Same pattern as Reserve Step 4:

```
✓ Slot {X} is yours.

Kushal will WhatsApp you at {phone} within 4 hours to take the ₹5,000 advance and
confirm your slot. The slot is held for 30 days while we wait for two more buyers.

[Receipt grid]
[Vertical timeline: Today → 30 days → 30+16 weeks]
[CTAs: View commitment / Share with potential co-buyer / Browse other plots]
```

The "Share with potential co-buyer" generates a WhatsApp deep-link with a pre-filled message about the plot and the open slots.

### 4. `/account/co-buys` — buyer's commitment dashboard

New tab in the existing `/account` sub-nav. Position between "Reservations" and "Activity".

Each commitment shown as a card:
- Plot thumbnail
- Plot title + location
- Slot label + acreage + price
- Status timeline (committed → locked → acquired → subdividing → titled → closed)
- Days to subdivision completion (if known)
- Action: View detail (`/account/co-buys/{id}`)
- Action: Withdraw (only if status is 'committed' and within 5-day grace window)

Detail page shows full status, expected timelines, anonymized co-buyer view, admin contact button.

### 5. `/admin/co-buys` — admin co-buy pipeline

New nav item in admin sidebar between "Reservations" and "Leads".

Table view:
- Plot title + location
- Status pill
- Slots committed (e.g., "2 of 3")
- Buyers (real names visible to admin)
- Days since first commitment
- Expected completion date
- Action: View detail

`/admin/co-buys/{id}` detail page:
- Full plot card
- 3 slots with full buyer details (name, phone, email, city, slot, advance status)
- Status timeline with admin actions to advance stages:
  - Mark Delight acquired (when status='locked')
  - Mark subdivision started
  - Update expected completion date
  - Mark subdividing complete (subdivision filed with revenue department)
  - Mark titled (each buyer has individual deed registered)
  - Mark closed
- Activity log of all status changes
- Admin notes field
- Withdrawal request approval (if any buyer has requested)

## Notification stubs

When status changes:
- `co_buys.status = 'locked'` (all 3 slots committed): admin gets notified, all 3 buyers get notified ("Your co-buy is fully committed; Delight acquires within 7 days")
- `co_buys.status = 'acquired'`: all 3 buyers notified ("Plot acquired; subdivision begins")
- `co_buys.status = 'subdividing'`: all 3 buyers notified weekly with progress
- `co_buys.status = 'titled'`: buyer notified individually when their deed is registered

For now, stub the notification sender at `lib/notifications/sender.ts` — function exists, logs to console, returns success. Sprint δ replaces with real WhatsApp + email.

## Test surface

Add these Playwright specs:

1. `tests/e2e/co-buy-discovery.spec.ts` — toggle "Co-buy ready" filter on /farmland, click into a co-buy-eligible plot, assert 3-slot picker appears in right rail, assert commitment counts render correctly

2. `tests/e2e/co-buy-commit.spec.ts` — buyer signs up, navigates to a co-buy-eligible plot, completes the 4-step commit flow, asserts row appears in `co_buy_commitments`, asserts slot count increments

3. `tests/e2e/co-buy-fills.spec.ts` — programmatically commit 3 buyers to slots A/B/C, assert co_buys.status moves from 'open' → 'committed' → 'locked', assert all 3 buyers see "fully committed" state in /account/co-buys

4. `tests/e2e/co-buy-anonymization.spec.ts` — buyer A views the plot, asserts they see "Slot B: Buyer X · Mysore" not "Slot B: Sunil Reddy · Mysore" (no PII leak)

5. `tests/e2e/co-buy-admin.spec.ts` — admin logs in, navigates to /admin/co-buys, sees pipeline table with real buyer names, advances a co-buy through stages

Run all against live Vercel preview after deploy.

## Seed data

Update the seed script to:
- Mark 4 of the 20 listings as `is_cobuy_eligible = true` (already done in earlier seeding — verify)
- Define `co_buy_config` JSONB for each (3 slots with realistic acreage + pricing)
- Create 4 corresponding `co_buys` rows
- Seed 1 of those co-buys with 1 commitment (for partial state testing)
- Seed 1 with 3 commitments (for fully-locked state testing)
- Seed 1 with status = 'subdividing' (for mid-subdivision state)
- Leave 1 in 'open' state with no commitments

Each seeded commitment has anonymized public labels generated from city + sequential letter.

## Acceptance criteria

1. `/farmland` "Co-buy ready" toggle filters listings correctly
2. Co-buy-eligible LDPs show the 3-slot picker in the right rail with live commitment counts
3. Buyer can commit to an open slot via `/plot/[slug]/co-buy` 4-step flow without crashing
4. PII never leaks to public — slot picker shows only anonymized labels for other buyers
5. Buyer sees their commitments in `/account/co-buys` with status timelines
6. When 3rd buyer commits, co-buy status moves to 'locked' and notification stubs fire
7. Admin can view all co-buys and advance stages from `/admin/co-buys`
8. Withdraw flow works for buyers within the 5-day grace window
9. All Playwright specs pass against live Vercel preview
10. No PII appears in the public co_buy_commitments_public view

## Commit

Slice this sprint into 4 commits:

1. **Slice 1**: Schema migrations + seed data + RLS + public view (`feat: co-buy schema + RLS + seed`)
2. **Slice 2**: LDP slot picker UI + listing card co-buy badge (`feat: co-buy slot picker on LDP and listings`)
3. **Slice 3**: Commit flow `/plot/[slug]/co-buy` 4 steps (`feat: co-buy 4-step commit flow`)
4. **Slice 4**: Buyer dashboard `/account/co-buys` + admin pipeline `/admin/co-buys` + Playwright specs (`feat: co-buy dashboards (buyer + admin) + tests`)

Push to main between slices so Kushal can preview each on Vercel.

## Constraints

- Do NOT integrate Razorpay (stub the payment, status='pending_offline')
- Do NOT integrate real WhatsApp (stub the notification sender)
- Do NOT build the urban 60×40 → 30×40 2-buyer variant this sprint (farmland 3-buyer first; urban is gated to month 4)
- Do NOT redesign anything visually beyond what's needed for these new surfaces
- Do NOT modify existing Reserve flow except to handle the case where a plot's co-buy is fully locked (in that case, the whole-plot reserve CTA hides)
- Mobile responsiveness: every new surface must work at 375px viewport. Slot picker on mobile is a stacked card view, not a 3-column grid

## Reference

- Product model details: `/docs/trueplots-project-document-v4.md` sections 3.2-3.4
- Verification checkpoint context: `/docs/04-trueplots-spec/03-trueplots-120-checkpoints-farmland.md` (referenced from the docs repo)
- Anonymization pattern (anti-PII-leak): inspired by Spinny's reservation flow which never exposes the plot owner's name to other buyers
- Legal structure (CIS-proof): see GLOSSARY.md "CIS" entry. The 3-buyer-advance with Delight-as-acquirer is the exact pattern engineered to stay outside SEBI CIS regulation. Don't break this — never pool buyer funds at any point in the flow.

## What comes after Sprint β

After this sprint lands, the next sprints in priority order:

- **Sprint γ — Admin completion**: verification queue (review submissions, approve/reject, assign verifier), reports (KPIs, deal flow, agent performance), settings (admin user management, agent management), lead detail editing, image upload to Supabase Storage
- **Sprint δ — Real integrations**: WhatsApp OTP via MSG91/Twilio/Aisensy, HubSpot CRM webhooks, Razorpay (if/when payments are taken in-app), Resend transactional email, PDF Verification Report generator
- **Sprint ε — Content + production deploy**: 4 more cornerstone SEO articles, sitemap, structured data, GA4, production domain swap to trueplots.in, Lighthouse pass

Don't start any of these until co-buying ships and Kushal verifies on the live preview.
