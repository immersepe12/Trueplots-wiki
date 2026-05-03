# Launch Sprint — Real inventory + lead-only flow

*This is the prompt to ship TruePlots to launch. Paste into Claude Code in the TruePlots repo. Run AFTER the digest 1829522191 bug is fixed (or alongside if Claude Code can isolate the changes — the new `/admin/listings/new` form isn't required for launch since this sprint seeds inventory directly).*

*Last updated: April 21, 2026.*

---

## Direction shift — read this first

The original 5-session plan assumed real payments via Razorpay, real WhatsApp OTP, real HubSpot. We're shipping launch without any of that. Buyer experience for V1 is:

1. Browse 9 real listings (7 Delight Eco Farms projects + 2 founder-direct Mandya plots — all dummy listings deleted)
2. See full detail pages with verification reports
3. On any "Reserve" or "Book site visit" or "Co-buy slot" CTA, a single modal opens that captures phone number + name + optional message
4. Submission lands in the admin panel as a lead, tagged with the source page and lead type
5. TruePlots team calls the buyer back within 4 hours

No payment in V1. No multi-step reserve. No WhatsApp OTP verification. The "₹5,000 reserve" mechanic is removed entirely from the UI — in V1, plots are held off-market when the team confirms the lead by phone.

Buyer auth (signup/login/account dashboard/favourites/saved plots/verification report page) all stays — those are buyer experience features that don't depend on payments.

## Part A — Wipe dummy data

The current Supabase has 20 dummy listings, 5 fictional agents, and various test reservations and leads from earlier verification work. Wipe them.

```sql
-- run via Supabase MCP
delete from co_buy_commitments;
delete from co_buys;
delete from favorites;
delete from reservations;
delete from leads;
delete from listing_images;
delete from listings;
delete from agents;
-- preserve users (especially admin), keep auth.users intact
-- keep the schema, just clear data rows
```

Verify by querying counts after — every table above should return 0 rows except `users`.

## Part B — Seed 9 real listings

All 9 listings are listed by TruePlots itself. Attribution displays as "Listed by TruePlots · Verified by TruePlots" — no individual agent attribution this round. The `agents` table can stay empty for V1.

Each listing needs:
- `id` (uuid)
- `title`
- `slug` (district-slug-village-slug-id format)
- `district`
- `village` / `locality`
- `state` = 'KA'
- `acreage_acres` (decimal)
- `price_total` (in paise — multiply by 100 for storage)
- `price_per_acre` or `price_per_sqft` derived
- `land_category` — agricultural / DC-converted / managed-farmland / etc.
- `summary_text` (3-4 sentence description)
- `highlights` (JSONB array of {title, description, icon})
- `verification_score_composite` (decimal 0-10)
- `verification_scorecard` (JSONB with 10 categories each having score + notes)
- `trust_chips` (array of strings)
- `is_cobuy_eligible` (bool)
- `co_buy_config` (JSONB if cobuy)
- `is_featured` (bool, mark 3 of 9 featured)
- `status` = 'published'
- `published_at` = now
- `images` (JSONB array — see imagery section below)
- `source` = 'delight' for the 7 Delight projects, 'founder_direct' for the 2 Mandya plots
- `agent_id` = null (TruePlots-listed)
- `listed_by_label` = 'TruePlots' (new column if not present — see schema additions)

### Schema additions (if not already present)

```sql
alter table listings add column if not exists listed_by_label text not null default 'TruePlots';
alter table listings add column if not exists source text not null default 'founder_direct';
-- 'delight', 'founder_direct', 'agent', 'partner'
```

The `listed_by_label` column is what gets displayed on cards and LDPs ("Listed by {listed_by_label} · Verified by TruePlots"). For V1, every listing has `listed_by_label = 'TruePlots'`.

### The 9 listings

#### 1. Vanam — Ayurvedic-themed managed farmland near Kanakapura Road

- **Slug:** `bangalore-rural-makalanda-vanam`
- **Title:** `Vanam — Ayurvedic-themed managed farmland, Makalanda`
- **District:** Bengaluru Rural
- **Village/locality:** Makalanda, near Kanakapura Road
- **Total project area:** 6 acres (gated community of 30 plots)
- **Plot sizes:** From 6,000 sq.ft
- **Pricing:** Starts from ₹30 lakhs (₹499/sq.ft for the 6,000 sq.ft entry plot)
- **Acreage on listing card:** 6 acres total / individual plots 0.14 acre+
- **Land category:** Managed farmland (DC-converted)
- **Summary:** "Vanam is a 6-acre gated managed-farmland community near Kanakapura Road, designed around Ayurvedic and spiritual plantations. Thirty individually-titled plots, starting from 6,000 sq.ft. Wellness amenities — meditation spaces, yoga zones, curated medicinal plantations — built into the community design."
- **Highlights:** Ayurvedic plantation curation; Wellness amenities (meditation, yoga); Just 30 plots in 6 acres; Strong rental potential as wellness retreat
- **Trust chips:** PTCL Clear, Non-Tank-Bed, DC-Converted, Clean Title, Road Access Verified
- **Co-buy eligible:** false (small plot sizes; full-plot purchases)
- **Featured:** true

#### 2. Ayana — Estate farmland in Sakleshpur (Western Ghats)

- **Slug:** `hassan-sakleshpur-ayana`
- **Title:** `Ayana — 25-acre estate farmland, Sakleshpur`
- **District:** Hassan
- **Village/locality:** Sakleshpur, Western Ghats
- **Total project area:** 25 acres (coffee + pepper plantation)
- **Plot sizes:** Price on request
- **Pricing:** Starts from price (display "Price on request — call us")
- **Land category:** Estate plantation farmland (coffee, pepper)
- **Summary:** "Ayana is a 25-acre coffee and pepper plantation in Sakleshpur, designed as a nature-immersive retreat inspired by Japanese principles of slow living. Silver oak canopy, robusta plantations, mountain microclimate. Held with full plantation operations — owners earn yield while owning the land."
- **Highlights:** Active coffee + pepper yield; Silver oak canopy; Western Ghats microclimate; Japanese-philosophy design
- **Trust chips:** PTCL Clear, Plantation-Active, Clean Title, Road Access Verified, Forest Boundary Verified
- **Co-buy eligible:** false
- **Featured:** false

#### 3. Canvas — Premium managed farmland near Lepakshi

- **Slug:** `sathya-sai-kallur-canvas`
- **Title:** `Canvas — 120-acre managed farmland community near Lepakshi`
- **District:** Sathya Sai (Andhra Pradesh — note: outside Karnataka, see geography note below)
- **Village/locality:** Kallur Village, Hindupura region
- **Total project area:** 120 acres (400+ plots)
- **Plot sizes:** From 5,500 sq.ft
- **Pricing:** Starts from price (display "Price on request — call us")
- **Land category:** Managed farmland (red soil)
- **Summary:** "Canvas is a 120-acre managed-farmland community spread across 400+ individually-titled plots near Lepakshi. Fertile red soil ideal for diverse plantation choices. Each plot starts at 5,500 sq.ft — an entry-level price point with long-term value potential in a rapidly-developing corridor."
- **Highlights:** 400+ plots; Red-soil suitability for diverse crops; Near Lepakshi heritage corridor; Sathya Sai district development zone
- **Trust chips:** PTCL Clear, Clean Title, Road Access Verified, Soil-Tested
- **Co-buy eligible:** false
- **Featured:** true

#### 4. Whistling Woods — Forest-estate farmland near Ballupet, Sakleshpur

- **Slug:** `hassan-ballupet-whistling-woods`
- **Title:** `Whistling Woods — 150-acre forest estate, Sakleshpur`
- **District:** Hassan
- **Village/locality:** Ballupet, Sakleshpur
- **Total project area:** 150 acres (coffee + cardamom + pepper plantations)
- **Plot sizes:** Price on request
- **Pricing:** Starts from price (display "Price on request — call us")
- **Land category:** Estate plantation (coffee + cardamom + pepper)
- **Summary:** "Whistling Woods is a 150-acre forest estate near Ballupet, Sakleshpur. Mature coffee, cardamom, and pepper plantations under a dense forest canopy. The largest of Delight's plantation holdings — designed for buyers who want plantation-scale ownership with operational management included."
- **Highlights:** Largest plantation in our portfolio; Coffee + cardamom + pepper diversification; Mature plantations (not greenfield); Misty Western Ghats climate
- **Trust chips:** PTCL Clear, Plantation-Active, Clean Title, Forest Boundary Verified
- **Co-buy eligible:** false
- **Featured:** false

#### 5. Rhythm of Soul (ROS) — Premium eco-living farmland, Sakleshpur

- **Slug:** `hassan-sakleshpur-rhythm-of-soul`
- **Title:** `Rhythm of Soul — 50-acre eco-living farmland, Sakleshpur`
- **District:** Hassan
- **Village/locality:** Sakleshpur
- **Total project area:** 50 acres / 156 plots
- **Plot sizes:** From 6,000 sq.ft
- **Pricing:** Starts from price (display "Price on request — call us")
- **Land category:** Managed farmland (coffee plantation ecosystem)
- **Summary:** "Rhythm of Soul is a 50-acre coffee plantation ecosystem with 156 individually-titled plots starting from 6,000 sq.ft. Built around the idea of living in rhythm with nature — flexible for farmhouse construction, weekend retreat, or long-term holding. Coffee yield rights included with each plot."
- **Highlights:** Coffee yield rights per plot; 156 individual titles; Flexible farmhouse construction; Sakleshpur-corridor appreciation
- **Trust chips:** PTCL Clear, DC-Converted, Plantation-Active, Clean Title, Road Access Verified
- **Co-buy eligible:** false
- **Featured:** true

#### 6. Bellevuee — Sustainable farmland community, Kanakapura Road

- **Slug:** `bangalore-rural-kanakapura-bellevuee`
- **Title:** `Bellevuee — 27-acre sustainable farmland community, Kanakapura Road`
- **District:** Bengaluru Rural
- **Village/locality:** Kanakapura Road
- **Total project area:** 27 acres
- **Plot sizes:** Price on request
- **Pricing:** Starts from price (display "Price on request — call us")
- **Land category:** Managed farmland (coconut + silver oak + teak)
- **Summary:** "Bellevuee is a 27-acre sustainable farmland community on Kanakapura Road, anchored by mature coconut, silver oak, and teak plantations. Self-sustaining farming model — farming infrastructure, water management, and crop operations included. Designed for buyers who want to step into an established plantation, not start from scratch."
- **Highlights:** Mature coconut + silver oak + teak; Self-sustaining farming model; Kanakapura corridor appreciation; Operational management included
- **Trust chips:** PTCL Clear, DC-Converted, Plantation-Active, Clean Title, Road Access Verified
- **Co-buy eligible:** false
- **Featured:** false

#### 7. Arinaa Country Farms — Build-your-farmhouse community, Kanakapura

- **Slug:** `bangalore-rural-kanakapura-arinaa-country-farms`
- **Title:** `Arinaa Country Farms — Build-your-farmhouse community, Kanakapura`
- **District:** Bengaluru Rural
- **Village/locality:** Kanakapura Road
- **Total project area:** Price on request (multi-acre community)
- **Plot sizes:** Price on request
- **Pricing:** Starts from price (display "Price on request — call us")
- **Land category:** Managed farmland with farmhouse-build option
- **Summary:** "Arinaa Country Farms combines individually-titled farmland with custom farmhouse construction. Eco-friendly building methods, panchayat-approved designs, milestone payments. Ownership of land + a farmhouse built to your specifications, all coordinated through Delight's design and construction team."
- **Highlights:** Land + farmhouse package; Eco-friendly construction; Panchayat-approved design; End-to-end project management
- **Trust chips:** PTCL Clear, DC-Converted, Construction-Approved, Clean Title, Road Access Verified
- **Co-buy eligible:** false
- **Featured:** false

#### 8. Mandya Plot A — 1 acre 4 guntas, near Mysore-Bangalore Highway

- **Slug:** `mandya-near-highway-44-guntas`
- **Title:** `1-acre 4-gunta parcel, near Mysore-Bangalore Highway, Mandya`
- **District:** Mandya
- **Village/locality:** Approximately 5.6 km from Mysore-Bangalore Highway, 8.6 km from Mandya bus stand
- **Total area:** 1 acre 4 guntas (44 guntas)
- **Pricing:** ₹1.5 lakhs per gunta = **₹66 lakhs total**
- **Per-acre rate:** ₹60 lakhs (44 guntas × ₹1.5L = ₹66L; 1 acre = 40 guntas)
- **Land category:** Agricultural (DC-conversion ready)
- **Summary:** "A 1-acre-4-gunta parcel in Mandya district, 5.6 km from the Mysore-Bangalore Highway and 8.6 km from Mandya town. Direct road access, level terrain, ideal for farmhouse construction or DC-conversion to layout. Sourced and verified directly by TruePlots' founding team."
- **Highlights:** 5.6 km from Mysore-Bangalore Highway; 8.6 km from Mandya town; Direct tar-road access; Level terrain
- **Trust chips:** PTCL Clear, Non-Tank-Bed, Clean Title, Road Access Verified
- **Co-buy eligible:** true
- **Co-buy config:**
  ```json
  {
    "slots": [
      { "id": "A", "label": "Slice A — 22 guntas (north)", "guntas": 22, "acres": 0.55, "price": 3300000, "position": "north" },
      { "id": "B", "label": "Slice B — 22 guntas (south)", "guntas": 22, "acres": 0.55, "price": 3300000, "position": "south" }
    ],
    "lead_only": true,
    "advance_per_slot": 0,
    "subdivision_estimated_weeks": 12,
    "total_acres": 1.1,
    "total_guntas": 44,
    "total_price": 6600000
  }
  ```
- **Featured:** true

#### 9. Mandya Plot B — 10.5 acres, 2 km from Mysore-Bangalore Highway

- **Slug:** `mandya-flyover-exit-10-5-acres`
- **Title:** `10.5-acre parcel, 2 km from Mandya flyover exit, Mysore-Bangalore Highway`
- **District:** Mandya
- **Village/locality:** Approximately 2 km from the Mandya flyover exit on Mysore-Bangalore Highway
- **Total area:** 10.5 acres
- **Pricing:** ₹50 lakhs per acre = **₹5.25 crores total**
- **Land category:** Agricultural (large parcel, ideal for fractional or layout development)
- **Summary:** "A 10.5-acre parcel just 2 km from the Mandya flyover exit on the Mysore-Bangalore Highway. The closest large parcel to highway access in this corridor we've seen in the last six months. Available as a single-buyer purchase or as a 5-buyer fractional split, with each buyer receiving an individually-titled 2.1-acre slice."
- **Highlights:** Just 2 km from Mysore-Bangalore Highway; 10.5 acres in one parcel; Fractional split available (5 buyers); Layout-development potential
- **Trust chips:** PTCL Clear, Non-Tank-Bed, Clean Title, Road Access Verified, Highway-Adjacent
- **Co-buy eligible:** true
- **Co-buy config:**
  ```json
  {
    "slots": [
      { "id": "A", "label": "Slice A — 2.1 acres (north-east)", "acres": 2.1, "price": 10500000, "position": "north-east" },
      { "id": "B", "label": "Slice B — 2.1 acres (east)", "acres": 2.1, "price": 10500000, "position": "east" },
      { "id": "C", "label": "Slice C — 2.1 acres (centre)", "acres": 2.1, "price": 10500000, "position": "centre" },
      { "id": "D", "label": "Slice D — 2.1 acres (west)", "acres": 2.1, "price": 10500000, "position": "west" },
      { "id": "E", "label": "Slice E — 2.1 acres (south-west)", "acres": 2.1, "price": 10500000, "position": "south-west" }
    ],
    "lead_only": true,
    "advance_per_slot": 0,
    "subdivision_estimated_weeks": 16,
    "total_acres": 10.5,
    "total_price": 52500000
  }
  ```
- **Featured:** false

### Verification scores for all 9

Each listing has a high verification composite (these are real Delight projects with established legal cleanliness, plus founder-sourced Mandya plots that Kushal personally vetted). Suggested:

- Vanam, Bellevuee, Arinaa: 9.4-9.6 (Delight's home corridor, established projects)
- Ayana, Whistling Woods, Rhythm of Soul: 9.2-9.4 (active plantations, more remote)
- Canvas: 9.0-9.3 (cross-border into Andhra; less common in TruePlots' core corridor)
- Mandya Plot A: 9.2 (founder-sourced, simple title)
- Mandya Plot B: 9.4 (founder-sourced, large parcel, premium location)

Generate the 10-category scorecard data deterministically per listing — composite at the listing's target value, individual category scores varying within ±0.4 of composite.

### Imagery

For each Delight project, scrape the hero image and 3-4 gallery images from the corresponding `delightecofarms.com/farmlands/{name}.html` page. Save to `/public/plot-images/delight/{project-slug}/`. Reference in `listings.images` JSONB.

For the 2 Mandya plots, use existing satellite imagery (`/public/plot-images/mandya.jpg`) plus 1-2 generic farmland photographs from `/public/plot-images/` if available. If satellite imagery alone, use 4-6 different crops/zoom levels.

If scraping fails on any project, fall back to satellite imagery for that listing too — the existing `lib/utils/plot-image.ts` district-based fallback should work.

## Part C — Replace multi-step reserve flow with single-modal lead capture

The existing `/plot/[slug]/reserve` 4-step flow goes away entirely. In its place: a single modal that opens from any "Reserve" / "Book site visit" / "Express interest" CTA across the site.

### New component: `<LeadCaptureModal />`

Renders as a centred dialog over the page. Props:
- `listingId` (uuid, required when opened from an LDP/listing context, optional otherwise)
- `sourceType` (enum, see source_type list below)
- `sourcePage` (string, current URL — auto-captured)
- `coBuySlot` (string, optional — passed when opened from a co-buy slot picker)
- `intentLabel` (string — e.g., "Reserve", "Book site visit", "Express interest in Slice A")

Modal content:

```
{intentLabel}
We'll WhatsApp you within 4 hours

[Name (optional)]
[Phone (+91 prefix, 10 digits)] *
[Optional message — anything you want us to know]

By submitting, you agree to be contacted by TruePlots. We never share your number with sellers.

[ Submit ]   [ Cancel ]
```

On submit:
- POST `/api/leads` with payload:
  ```json
  {
    "name": string | null,
    "phone": string,
    "message": string | null,
    "listing_id": uuid | null,
    "source_type": string,
    "source_page": string,
    "co_buy_slot": string | null
  }
  ```
- Server: insert into `leads` table with status='new'
- Server response: 201 { id }
- Client: replace modal content with confirmation:
  ```
  ✓ Thanks, {name or 'we'll be in touch'}.
  Kushal will WhatsApp you at {phone} within 4 hours.
  
  [ Done ] [ Browse more plots ]
  ```

### `source_type` enum

```sql
create type lead_source_type as enum (
  'homepage_hero',
  'homepage_co_buy_card',
  'homepage_featured_card',
  'listing_card',
  'ldp_reserve_button',
  'ldp_book_site_visit',
  'ldp_question_form',
  'ldp_co_buy_slot',
  'plot_card_save',  -- when not authed
  'newsletter_footer',
  'newsletter_verified_only_alerts_page',
  'contact_form',
  'list_a_plot_owner_form',
  'list_a_plot_agent_form',
  'services_request_quote',
  'how_we_verify_callback',
  'financing_inquiry',
  'urban_waitlist'
);
```

Add to `leads` table:

```sql
alter table leads add column if not exists source_type lead_source_type;
alter table leads add column if not exists source_page text;
alter table leads add column if not exists co_buy_slot text;
alter table leads add column if not exists message text;
create index leads_source_type_idx on leads(source_type);
create index leads_listing_idx on leads(listing_id);
```

### Wire every CTA on the site to open the modal

| Location | CTA text | Source type | Listing context |
|---|---|---|---|
| Homepage hero | "Show 240 plots" | navigates to /farmland (no modal) | — |
| Homepage hero "Verifying right now" card | clickable | navigates to LDP | — |
| Homepage four-pillar cards | "See our 120 checkpoints →" / "How co-buying works →" / etc | navigate to content pages (no modal) | — |
| Homepage featured plots strip | clicking card | navigates to LDP | — |
| Listings page card | clicking card | navigates to LDP | — |
| Listings page heart | toggles favourite (login-gated) — opens login modal not lead modal | — | — |
| LDP "Reserve for ₹5,000" button (right rail) | rename to **"Request callback"** — opens lead modal | `ldp_reserve_button` | listing_id |
| LDP "Book site visit" button | opens lead modal | `ldp_book_site_visit` | listing_id |
| LDP "Express interest in Slice X" buttons (in co-buy slot picker) | opens lead modal with `co_buy_slot` | `ldp_co_buy_slot` | listing_id, slot |
| LDP question form (bottom) | submit goes to `/api/leads` directly (no modal) | `ldp_question_form` | listing_id |
| LDP "WhatsApp" button | opens WhatsApp deep-link to TruePlots number with pre-filled context — not a lead capture | — | — |
| Footer newsletter form | submits email to existing `/api/newsletter/subscribe` — not a lead | — | — |
| Verified-only alerts page | newsletter form | `newsletter_verified_only_alerts_page` | — |
| Contact page form | submit | `contact_form` | — |
| List a plot — Owner form | submit | `list_a_plot_owner_form` | — |
| List a plot — Agent path | submit | `list_a_plot_agent_form` | — |
| Services page "Request a quote" | opens lead modal | `services_request_quote` | — |
| How we verify "See full 120-point PDF" | opens lead modal (since PDF download isn't built) | `how_we_verify_callback` | — |
| Financing page | "Check eligibility" CTA | opens lead modal | `financing_inquiry` |
| Urban sites stub page | newsletter form | `urban_waitlist` | — |

The `<LeadCaptureModal />` is the workhorse component — every callback CTA across the site routes through it. The trigger button is a simple wrapper that opens the modal with the right props.

### Delete old reserve infrastructure

- Delete `/plot/[slug]/reserve/page.tsx` and the entire 4-step folder structure (`step-1.tsx`, `step-2.tsx`, etc.)
- Delete `/api/reservations/*` endpoints if they exist
- Delete the `reservations` table — or alternatively, alias it to leads. Cleaner to drop the table since the data model is just `leads` now.
- Delete `/admin/reservations/*` admin views — they're replaced by `/admin/leads`

If buyer auth is preserved (Sprint α work), the buyer's `/account/reservations` tab also goes away. Replace with `/account/leads` showing the lead history they've submitted (when authed). Or hide that tab entirely if it's confusing for V1 — buyers don't need to see their own lead submissions, the admin sees them.

## Part D — Co-buying flow simplified to lead-capture

The Sprint β co-buying flow design assumed real ₹5,000 advance commitments. With the launch direction shift, that's gone. Co-buying becomes:

- LDP for cobuy-eligible listings shows the slot picker as designed (3 slots for farmland, 2 or 5 depending on the listing's `co_buy_config`)
- Each slot shows: position, acreage, price, status (`open` / `interest` / `committed_pending_call`)
- Clicking "Express interest in Slice X" opens the lead capture modal with `co_buy_slot = 'X'` and `source_type = 'ldp_co_buy_slot'`
- Server records the lead, status = `new`
- Admin sees the lead in `/admin/leads` filtered by listing + slot
- Admin manually changes the slot's status as they confirm interest by phone — no buyer-facing slot reservation in V1

This means the `co_buys` and `co_buy_commitments` tables are not needed for V1. Keep the schema if it was already created in a prior sprint, but gate it with a feature flag or just don't query it.

For V1 LDP slot picker UI, derive slot status from leads:
- `open` if no lead exists with `co_buy_slot = 'X'` for this listing
- `interest_received` if at least one lead exists for that slot

Display:
```
Slot A — 22 guntas · ₹33 L     [ Express interest ]
Slot B — 22 guntas · ₹33 L     [ Interest received — call in progress ]
```

## Part E — Admin enhancements

### `/admin/leads` becomes the central lead view

Replace the existing kanban with a richer view:

**List view (default):**

| Buyer | Phone | Listing | Source | Co-buy slot | Status | Created |
|---|---|---|---|---|---|---|
| Ramesh K | +91 98876 10001 | Vanam | LDP Reserve | — | New | 2h ago |
| (anonymous) | +91 98876 10002 | Mandya 10.5 ac | LDP Co-buy | C | New | 4h ago |
| Sunil R | +91 98876 10003 | — | Newsletter | — | New | 6h ago |

Filters at top:
- Status (New / Contacted / Qualified / Site visit / Closed-won / Closed-lost / Spam)
- Source type (multi-select with counts)
- Listing (search)
- Date range (last 24h / 7d / 30d / all)

Each row clickable → opens `/admin/leads/{id}` detail panel (slide-in from right).

**Detail panel:**
- All buyer fields
- Linked listing card (if applicable)
- Source page (clickable to view)
- Co-buy slot context (if applicable)
- Quick action buttons:
  - **WhatsApp** (deep-link with pre-filled context)
  - **Call** (tel: link)
  - **Mark as contacted** (status='contacted')
  - **Mark as qualified** (status='qualified')
  - **Mark closed-won / closed-lost**
  - **Mark as spam** (hides from default views)
- Notes textarea (admin-only)
- Activity log (status changes, notes added)

### Dashboard KPI updates

The existing 4 KPI cards on `/admin`:
- Active listings → 9 (was 12 dummy + 8 = 20)
- New leads (7d) → live count from leads table
- In verification → keep (placeholder until verification queue ships)
- Reservations held → REPLACE with **"Hot leads"** = count of leads with status='qualified' or 'site_visit' in last 7 days

### Admin sidebar simplification

Old:
- Dashboard / Listings / Reservations / Leads / Verification / Content / Reports / Settings

New (V1):
- Dashboard
- Listings
- Leads (badge: count of new leads)
- Verification (badge: 0 — placeholder)
- Settings

Remove: Reservations (gone), Content (Sprint ε), Reports (Sprint ε)

## Part F — Strategic doc updates

After this launch sprint ships, update the strategic docs in `/docs/`:

- `trueplots-project-document-v4.md` — note the V1 launch model (no payments, lead-only), defer Razorpay/HubSpot/WhatsApp OTP integrations to V2
- `trueplots-gtm-plan-v4.md` — update Phase 1 (Months 0-4) to reflect lead-capture-only buyer flow, with the team manually qualifying every lead by phone before any commercial commitment
- `trueplots-project-pitch-v4.md` — update the "Where we are" section to reflect 9 real listings (7 Delight + 2 founder-direct), no payment infrastructure in V1

Bump these to `v4.1` (point revision since the strategic positioning is unchanged, just the V1 implementation differs).

These doc changes are out of scope for Claude Code in this sprint — flag them in the commit message as "doc updates required, see launch-sprint.md Part F" and let the founder handle the doc edits via Cowork.

## Part G — Testing

Add Playwright specs:

1. `tests/e2e/lead-capture-flow.spec.ts` — visit each lead-capture trigger CTA (across homepage, /farmland, every LDP, contact, services, financing, list-a-plot, etc.); for each, click the CTA, fill the modal with phone "9999999999" + message "test", submit, assert confirmation appears, assert lead row exists in DB with the correct `source_type` and `source_page`

2. `tests/e2e/co-buy-slot-interest.spec.ts` — visit Mandya Plot B LDP, click "Express interest in Slice C", submit modal, assert lead row has `co_buy_slot = 'C'` and `listing_id` matching

3. `tests/e2e/admin-lead-management.spec.ts` — admin logs in, visits `/admin/leads`, filters by source_type, opens lead detail, marks as contacted, asserts status persists

4. `tests/e2e/no-old-reservation-routes.spec.ts` — assert that `/plot/{slug}/reserve` returns 404 (route deleted), `/account/reservations` no longer exists

5. Update existing tests:
   - `reserve-resolves.spec.ts` — delete (route removed)
   - `all-plots-resolve.spec.ts` — keep, just verify all 9 LDPs resolve
   - `mobile-smoke.spec.ts` — update list of routes to test (remove reserve, add lead-capture modal triggers)
   - `auth-role-redirect.spec.ts` — keep
   - `favorites-toggle.spec.ts` — keep
   - `verification-report.spec.ts` — keep, update to test against new 9 slugs

All Playwright specs run against live Vercel preview after deploy.

## Part H — Mobile responsiveness

The lead capture modal must work on 375px:
- Modal goes full-width on mobile, centred on desktop
- Form fields full-width with `min-h-12` touch targets
- Submit button full-width
- Confirmation state full-width

Co-buy slot picker on mobile:
- 3-slot or 5-slot row becomes vertical stack on `<768px`
- Each slot card is full-width

LDP right rail "Request callback" CTA on mobile:
- Sticky bottom bar pattern (already covered in mobile responsiveness sprint)

## Acceptance criteria

1. Database has exactly 9 listings, all with `listed_by_label = 'TruePlots'`, all status='published'
2. Database has zero rows in `agents`, `co_buys`, `co_buy_commitments`, `reservations` (or those tables are dropped)
3. Homepage shows 3 featured listings: Vanam, Canvas, and Mandya Plot A
4. `/farmland` shows all 9 listings
5. Every LDP renders without 404 (test all 9 slugs)
6. Every LDP "Request callback" CTA opens the lead capture modal
7. Co-buy slot pickers render on Mandya Plot A (2 slots) and Mandya Plot B (5 slots) only
8. Modal submission lands in `leads` table with full source attribution
9. `/admin/leads` shows all leads with source filter
10. Admin can change lead status and changes persist
11. `/plot/{slug}/reserve` returns 404 (old reserve flow gone)
12. `/account/reservations` no longer exists in account sub-nav
13. Verification report page still works for all 9 listings
14. Buyer signup/login still works (Sprint α retained)
15. Favourites still work (Sprint α retained)
16. Header still shows "List a plot" CTA in top right; clicking goes to `/list-a-plot` (existing content page)
17. Mobile responsive at 375px
18. All Playwright specs pass against live Vercel preview

## Commit strategy

Slice this into 4 commits:

1. **Slice 1 — Schema and seed**: schema additions (`listed_by_label`, `source`, `source_type` enum, `co_buy_slot` column, `message` column on leads), wipe data, seed 9 listings with deterministic verification scores. (`feat: launch seed — 9 real listings (7 Delight + 2 founder-direct)`)

2. **Slice 2 — Lead capture modal + API**: build `<LeadCaptureModal />` component, build `/api/leads` POST endpoint, wire all CTAs across the site to use the modal. (`feat: lead capture modal + source attribution`)

3. **Slice 3 — Remove reserve flow**: delete `/plot/[slug]/reserve`, delete reservations table and related views, simplify admin sidebar, repoint LDP "Request callback" to lead modal. (`feat: remove reserve flow, lead-only model for V1`)

4. **Slice 4 — Admin leads upgrade + tests**: rebuild `/admin/leads` with rich list + filters + detail panel, replace KPI for "Reservations held" with "Hot leads", Playwright specs. (`feat: admin leads dashboard + Playwright suite for lead-only V1`)

Push between slices. Founder reviews on Vercel preview between slices.

## Constraints

- Do NOT integrate Razorpay (no payments in V1)
- Do NOT integrate real WhatsApp (lead-only; team calls back from their phones, no in-app messaging)
- Do NOT integrate HubSpot (lead data stays in Supabase; admin works directly with the leads table; HubSpot sync is V2)
- Do NOT delete buyer auth (Sprint α work stays)
- Do NOT delete favourites (Sprint α work stays)
- Do NOT delete verification report page (Sprint α work stays)
- Do NOT delete co-buy schema (gate with feature flag if not used; V2 may revive it)
- Do NOT change the design system, colour palette, or typography
- Mobile responsive is mandatory — lead modal and co-buy slot picker both need 375px verification

## What this sprint enables

After this lands, the founder can:

- Send the public URL to friends, prospective investors, and (cautiously) a small initial buyer cohort
- Let buyers browse 9 real listings, read full verification reports, save plots to favourites
- Capture leads from every meaningful surface with full source attribution
- Manage leads in admin: phone, source, listing context, status workflow
- Iterate copy, images, and listing detail from real-world feedback before adding payment infrastructure in V2

V2 priorities (after launch validation):
- Real Razorpay for ₹5,000 reserve mechanic
- Real WhatsApp Business API for OTP + automated buyer comms
- HubSpot CRM sync for lead lifecycle
- PDF Verification Report generator
- Production domain swap (.vercel.app → trueplots.in)
- Lighthouse + Core Web Vitals optimization
- More cornerstone SEO articles
- Agent landing page + agent dashboard (per v4 strategic plan)

---

Paste this into Claude Code. Run after the digest 1829522191 fix lands. Reply with the deploy URL after each slice.
