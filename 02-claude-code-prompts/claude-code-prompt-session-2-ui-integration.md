# Claude Code Prompt — TruePlots Build Session 2: UI Integration

Paste into Claude Code inside the existing TruePlots project directory. Session 1 foundation must be on `main`. The six Claude Design HTML output files must be placed in `/design-exports/` before starting this session.

## Context

You are continuing the TruePlots build. Session 1 (commit `e56f905`) shipped the foundation: Next.js 15 + React 19 + TypeScript, Tailwind with design tokens from `DESIGN_SYSTEM.md`, Fraunces/Inter/JetBrains Mono via `next/font`, 9-table Supabase schema with RLS, auth middleware gating `/admin/*`, login form, HubSpot stub, MDX pipeline, 14 routes build-passing.

This session takes the six Claude Design output files in `/design-exports/` and converts them into production React components wired to the Supabase data layer.

Read before writing any code:

* `README.md` — project orientation
* `DESIGN_SYSTEM.md` — design tokens, type scale, component rules (single source of truth for styling)
* `trueplots-project-document-v4.md` — product model, fractional flow, verification architecture, agent-inclusive marketplace model (READ THIS; v3 is deprecated)
* `/design-exports/*.html` — all six Claude Design outputs (these are the visual contract)

Do not deviate from the Claude Design output visually without documenting the reason in a `DESIGN_DEVIATIONS.md` file. The designs are locked. Your job is faithful translation to React + data, not redesign.

## Session scope

At the end of this session, a visitor can:

1. Land on the homepage at `/` and see the full designed homepage rendered from real data (featured plots come from Supabase, stats counters come from a queries module)
2. Browse listings at `/farmland` with working filters (district, budget, size, co-buy, verification score), see the three-column grid, and click into plot detail pages
3. Open a plot detail page at `/plot/[slug]` with all five tabs (Overview / Verification Report / Protection / Specs / Financing) rendering real data from Supabase
4. Start a reserve flow at `/plot/[slug]/reserve` with all four steps, persist progress in React state (not localStorage in production build — use URL state and Supabase draft record), and complete with a mock payment success (Razorpay integration is Session 4)
5. Log into `/admin` and see the admin dashboard shell with KPI cards pulling live Supabase counts, activity feed from a real `activity_log` table, and the sidebar navigation rendering all views (Listings table, Leads kanban, Verification Queue, Content, Reports, Settings) — views can be scaffolded with real layout but placeholder data, full CRUD is Session 3
6. Read a sample MDX article at `/guides/section-79a-b-karnataka-farmland-buyers-2026` using the article template, with TOC, callouts, inline CTAs, related guides, and author bio

## Out of scope for this session

* Razorpay integration (Session 4)
* WhatsApp OTP integration (Session 4 — stub with a text input + fake verify button that always succeeds)
* HubSpot webhook firing on real events (Session 4 — keep stub)
* Full admin CRUD flows — listings add/edit/delete, lead editing, verification workflow (Session 3)
* PDF Verification Report generator (Session 4)
* SEO meta optimization, sitemap, production deploy (Session 5)
* Agent landing page, agent application flow, agent dashboard, public agent profile pages, agent scorecard UI (all month 3 — not this session). **Note:** Listing-card and LDP *attribution* ("Listed by [Agent Name] · Verified by TruePlots") IS in scope this session — see "Agent attribution" cross-cutting section below.

Resist scope creep. Every hour spent on out-of-scope items is an hour not spent on the six pages above.

## Pages to build

### 1. Homepage (`/`)

Source file: `/design-exports/homepage.html`

Key implementation notes:

* Hero carousel: three variants, rotates on page load (not auto-advance). Use `useState` + random selection on mount. "240 PLOTS LIVE · KARNATAKA" chip reads from `SELECT COUNT(*) FROM listings WHERE status = 'published' AND state = 'KA'` — put this in `lib/queries/stats.ts`.
* Featured plots strip: 4 cards, pulls `SELECT * FROM listings WHERE is_featured = true AND status = 'published' ORDER BY featured_order LIMIT 4`. Survey-sketch thumbnail comes from `listings.thumbnail_url` or fallback SVG placeholder generator.
* "How It Works" 4-step: static, no data binding. Convert HTML directly to component.
* "Numbers That Matter" dark section: stats from `lib/queries/stats.ts` (`verified_count`, `rejected_count`, `rejection_rate`, `avg_verification_days`).
* Delight pullquote section: static content, move copy to `content/pullquotes.ts` for easy editing.
* FAQ panel: 6 questions. Static for now, move to CMS in Session 5. Use shadcn `Accordion`.
* Footer: full implementation. Newsletter subscribe POSTs to `/api/newsletter/subscribe` which writes to `newsletter_subscribers` table and fires a HubSpot stub call.

Route: `app/page.tsx` + component files in `components/home/`.

### 2. Listings (`/farmland`)

Source file: `/design-exports/listings.html`

Key implementation notes:

* URL-driven filter state. Every filter change updates the query string (`/farmland?district=mandya&budget=40L-1Cr&cobuy=true&sort=newest`). Use `useSearchParams` + `useRouter`. No client-side filter state that isn't also in the URL.
* Query construction: build Supabase query in `lib/queries/listings.ts` — takes a filter object, returns typed `Listing[]`. Handles pagination (20 per page).
* Top filter bar: District (multi-select with counts), Budget (range slider snapping to ₹10L steps from ₹20L to ₹5Cr), Size (range from 0.25ac to 20ac), Co-buy eligible (toggle), Sort (Newest / Price asc / Price desc / Verification score desc / Area desc).
* Active filter chips: dismissible, clearing a chip updates URL.
* Left sidebar: survey number search (text input, exact match), District checkboxes with live counts (SELECT district, COUNT(*) ... GROUP BY district WHERE status='published'), Land Category, Verification Score slider (100-120), Water Source, Road Access.
* Triple-banner carousel above grid: static three slides for now, move to CMS in Session 5.
* Grid: 3 columns desktop, 2 tablet, 1 mobile. Use `components/listings/ListingCard.tsx` — this component is reused on homepage featured strip and LDP "Similar plots" strip, so make it configurable with a `variant` prop (`default` | `compact` | `featured`).
* Inline service cards at positions 6 and 12 (interrupting the grid): these are static promo blocks. Hardcode for now, move to CMS Session 5.

Route: `app/farmland/page.tsx` + `components/listings/`.

### 3. Listing Detail Page — LDP (`/plot/[slug]`)

Source file: `/design-exports/ldp.html`

This is the strongest page in the product. Be careful with it.

Key implementation notes:

* Slug format: `{district}-{village}-{survey_no}` lowercased, hyphen-separated. Generated on listing insert, stored in `listings.slug`, unique indexed.
* Above-fold illustrated plot view + 6-thumbnail gallery: images from `listings.images` JSONB array. Each image has `{url, alt, label, type}` where type is `wide_view | tar_road | borewell | survey_pillar | aerial | location_map`. If an image type is missing, fall back to an SVG placeholder with the label.
* Sticky right rail price block: CSS `position: sticky; top: 80px`. Contains all CTAs: Reserve for ₹5,000 (links to `/plot/[slug]/reserve`), Book site visit (opens modal with calendar — Session 4, stub for now), WhatsApp share, Save, mini scorecard preview.
* Tab navigation: URL hash-based (`#overview`, `#verification`, `#protection`, `#specs`, `#financing`). Use `useEffect` to sync hash with active tab state. Tabs rendered as `<section>` blocks, active tab scrolled into view smoothly on change.
* Verification Report tab is the product moat. Render exactly as designed. Dark Forest Green hero card with "4 field inspections · 3 legal experts" in Fraunces display, verified date, verifier name (from `listings.verified_by_user_id` joined to `users.full_name`), "Valid for 90 days" chip. Five trust chips from `listings.verification_flags` (array of string tags). 10-category scorecard from `listings.verification_scores` (JSONB with `{ownership, title_chain, zoning, encumbrance, boundary, road, water, soil, environmental, neighbors}` each with `{score: number, notes: string}`). Findings from `listings.verification_findings` (array of `{title, description, severity}`). PDF download links to `listings.verification_report_pdf_url` (Session 4 generates this; for now link to a placeholder PDF).
* Overview tab: hand-written plot summary (`listings.summary_text`), 8-field key facts grid (from listings columns), "Why this plot is uncommon" cards (from `listings.highlights` JSONB array of `{title, description, icon}`), illustrated location map (static SVG per district — commission later, placeholder for now), distances grid (from `listings.distances` JSONB).
* Similar plots strip: 4 cards, query `SELECT * FROM listings WHERE district = $1 AND price BETWEEN $2*0.7 AND $2*1.3 AND id != $3 AND status = 'published' LIMIT 4`.
* Questions block at bottom: form POSTs to `/api/leads/question` which inserts into `leads` table with `source='ldp_question'` and fires HubSpot stub.

Route: `app/plot/[slug]/page.tsx` + `components/ldp/` including subfolders per tab.

### 4. Reserve flow (`/plot/[slug]/reserve`)

Source file: `/design-exports/reserve.html`

Key implementation notes:

* Step state is URL-driven, not localStorage. Route: `/plot/[slug]/reserve?step=1` through `step=4`. On Step 1 mount, create a `reservations` row with status `draft`, store the `reservation_id` in URL as `?rid=xxx&step=1`. Subsequent steps update the same row. This survives page refresh without the localStorage hack.
* Step 1 (Summary): read-only. Reserve guarantees block (4 bullet points, from `content/reserve-copy.ts`). "Continue to details →" updates URL to step=2.
* Step 2 (Buyer details): form with `react-hook-form` + zod schema. Fields: full_name, phone (+91 prefix, 10 digits, regex validated), email (optional), city. On phone blur, reveal OTP input. OTP verification: stub for now, call `/api/otp/verify` which always returns success in Session 2. Write validated data to `reservations.buyer_details` JSONB and advance to step 3.
* Step 3 (Payment): order summary, payment method radio (UPI / Card / Netbanking), terms checkbox. "Pay ₹5,000 securely" button: in Session 2, skip the actual Razorpay call and directly mark `reservations.status = 'confirmed'`, set `reservations.paid_at = now()`, advance to step 4. Session 4 replaces this with real Razorpay.
* Step 4 (Confirmation): success screen, receipt grid, vertical timeline, CTAs. "Book site visit" opens modal (stub — Session 4). "Share with co-buyer" generates a shareable link `/plot/[slug]?referred_by={buyer_phone_hash}` and copies to clipboard.
* On completion, send a confirmation email via `/api/emails/reservation-confirmation` (use Resend or Supabase's email service — make this a swappable adapter in `lib/email.ts`).
* Add this copy line on Step 4 that wasn't in the design: "Kushal will call you within 4 hours at [phone]. If you miss the call, we'll try again — no follow-ups, no spam." Place it below the receipt grid, above the timeline. This is a product-level promise, not just UI copy.

Route: `app/plot/[slug]/reserve/page.tsx` with step logic in `components/reserve/`.

### 5. Admin dashboard (`/admin`)

Source file: `/design-exports/admin.html`

Key implementation notes:

* Sidebar: darker than public pages (Ink Black `#0F1712`), Harvest Gold accent on active nav item, badges from live counts.
* Sidebar nav links: Dashboard (/admin), Listings (/admin/listings), Leads (/admin/leads), Verification Queue (/admin/verification), Content (/admin/content), Reports (/admin/reports), Settings (/admin/settings).
* Dashboard (`/admin`) view:
   * 4 KPI cards: pull from `lib/queries/admin-stats.ts`. Deltas calculated vs previous period (week or day as appropriate). Format: main number large in Fraunces, delta in Success Green with trend arrow.
   * Recent activity feed: read from `activity_log` table, last 24 hours, joined to users and listings for names. Color-coded pills per event type (RESERVE/VERIFY/CO-BUY/LEAD/PUBLISH/VISIT).
   * Upcoming this week sidebar: three sections (Site Visits, Verifications Due, Follow-ups). Each queries its own source table with a week-ahead filter.
* Listings view (`/admin/listings`): table with photo thumb, title, location, size, price, status pill, verification score, reservations count, actions column. Filters above table. In Session 2, table reads real data but row actions (edit/publish/unpublish) stub to console.log — CRUD is Session 3. Inline status pill click: stubbed, no state change yet.
* Leads view (`/admin/leads`): 5-column kanban. Read from `leads` table grouped by `status`. Cards draggable (use `@dnd-kit/core` — install this session). Dragging a card between columns updates `leads.status` via API. This is the one full CRUD flow to implement in Session 2 because it's simple and tests the drag-drop library.
* Verification Queue, Content, Reports, Settings views: scaffold with layout + header + "Coming in Session 3" empty state. Don't build yet.

Route: `app/admin/**/page.tsx` with shared layout at `app/admin/layout.tsx`.

### 6. SEO article template (`/guides/[slug]`)

Source file: `/design-exports/article.html`

Key implementation notes:

* MDX-rendered. Frontmatter schema (typed via zod): `{title, slug, category, published_date, author_id, reading_time, excerpt, related_guide_slugs}`.
* Narrow centered body (max 680px). Sticky TOC left sidebar 220px wide, highlights active section on scroll (use IntersectionObserver).
* Author block: KK avatar, name, role, location. Author data from `authors.ts` keyed by `author_id`.
* Callout components available in MDX: `<Callout variant="info|warning|amendment">`, `<Checklist>`, `<CTABand>`, `<SkipTheReading>` (the left sidebar callout box).
* Related guides strip: 3 cards from `related_guide_slugs` frontmatter.
* Port the Section 79A/B article (all text visible in the Claude Design output) as the seed MDX file at `content/guides/section-79a-b-karnataka-farmland-buyers-2026.mdx`. Author Kushal K., 9 min read, 02 April 2026.

Route: `app/guides/[slug]/page.tsx` + `components/article/`.

## Agent attribution (cross-cutting, required this session)

Per v4 strategic docs, TruePlots uses an agent-inclusive marketplace model. Delight Realty's 100+ agent network supplies most listings at launch; every listing is jointly verified by the listing agent and TruePlots' verification team. This session implements the minimum agent surface needed to support that model at launch — schema + listing-level attribution UI only. Agent-facing surfaces (landing page, dashboard, profile pages, scorecard) are month-3 work.

### Schema additions (new migration this session)

* New table `agents`:
  ```
  id uuid pk default gen_random_uuid(),
  full_name text not null,
  rera_number text,
  phone text,
  email text,
  status text not null default 'active', -- active | paused | removed
  created_at timestamptz default now(),
  updated_at timestamptz default now()
  ```
* New column on `listings`: `agent_id uuid null references agents(id) on delete set null`
  * Nullable because founder-sourced and Delight-direct listings will not have an agent.
* New column on `listings`: `listed_by_type text not null default 'agent'` — values `agent | founder | delight_direct` (for filtering and analytics).
* RLS on `agents`: admin users read/write all; public read for active status only (month-3 agent profile pages will use this).

### UI additions this session

1. **`ListingCard`** accepts optional joined `agent: { full_name }` via the Supabase query. When present, render one line below the title, before price: `Listed by {agent.full_name} · Verified by TruePlots` — Fraunces Italic 14px, Charcoal `#4A5247`, not a link this session. When `agent_id` is null, render `Verified by TruePlots` alone on that line.
2. **LDP right-rail price block** — below the Verified badge, add a line `Listed by {agent.full_name}` (not a link this session; month 3 links to `/agents/[id]`).
3. **Verified Report PDF cover** — PDF generator is Session 4, but add schema column `listings.agent_credit_on_pdf boolean not null default true` so Session 4 knows whether to credit the agent on the cover.

### Seed data additions

Append to `scripts/seed-session-2.ts`:

* 5 agents with placeholder Delight Realty names: `Ravi Kumar`, `Sunil Reddy`, `Priya K`, `Mohan Gowda`, `Lakshmi Devi` — all status `active`, dummy RERA numbers.
* Of the 12 seed listings: assign 10 to agents (roughly 2 per agent), leave 2 with `agent_id = null` and `listed_by_type = 'founder'` to test both code paths.

### Out of scope for agent work this session

* Public agent profile pages `/agents/[id]` — month 3
* Agent application flow `/join-as-agent` — month 3
* Admin agent management `/admin/agents` — month 3
* Agent scorecard UI — month 3+
* Agent dashboard (scoped-admin view for agents to see their listings/leads) — month 3

## Technical decisions for this session

### Component library discipline

Every reusable element goes in `components/ui/` (primitives: Button, Badge, Chip, Input, Select, Checkbox, Accordion, Tabs, Dialog) or `components/shared/` (domain: ListingCard, PlotThumbnail, VerificationBadge, ScoreBar, TrustChip, NumberedStep, Pullquote, NewsletterForm).

Do not inline-style anything beyond one-off layout tweaks. Every color, spacing, radius, shadow, font-size, font-weight must resolve to a token from `DESIGN_SYSTEM.md`. If a Claude Design output uses a value not in the design system, add it to `DESIGN_SYSTEM.md` first, then use it. Never hardcode.

### Image handling

* Listing images: stored in Supabase Storage bucket `listings-images`, referenced by URL. Use Next.js `<Image>` with `unoptimized={false}`. Configure Supabase Storage domain in `next.config.ts`.
* SVG illustrations (Karnataka map, plot polygons, district maps): store in `public/illustrations/` as inline SVG components in `components/illustrations/` for bundler optimization.
* Placeholder generation: when a listing has no images yet, generate a deterministic SVG survey-sketch from the listing's survey number (stable output per input, use a seeded random function). Put this in `lib/placeholder-image.ts`.

### Data layer conventions

* All Supabase queries live in `lib/queries/*.ts`, never inline in components.
* Every query function returns a typed result using types auto-generated by `supabase gen types typescript`.
* Server Components fetch data. Client Components receive data as props or use server actions.
* Mutations use Next.js Server Actions, not API routes, except for webhooks (`/api/hubspot/webhook`, `/api/newsletter/subscribe`).

### Type safety

* Zero `any`. If you need to escape hatch, use `unknown` and narrow explicitly.
* Every form schema is a zod object exported from `lib/schemas/*.ts`.
* Every API route / server action has request and response types.

### Performance

* No unnecessary client components. Default is Server Component; opt into Client only for interactivity (forms, tabs, kanban, filters).
* Images lazy-loaded except hero and first 2 rows of listings grid.
* Fonts: already configured via `next/font` in Session 1. Do not re-add font links in components.

### Testing

* For this session, smoke tests only. One Playwright test per page that loads the route and asserts the hero heading is present. Tests live in `tests/e2e/`. Don't block on full test coverage — Session 5 is for polish.

## Known technical risks

**Risk 1:** The Claude Design HTML uses Tailwind classes that don't resolve to our tokens.
The HTML outputs were generated against Tailwind's default palette. You will need to translate `bg-green-800` (or whatever) to `bg-forest-green` from our token map. Before writing any component, audit `/design-exports/*.html` for non-token color and spacing classes and build a translation table at the top of `DESIGN_DEVIATIONS.md`.

**Risk 2:** Reserve flow with URL-driven state is more complex than localStorage.
The benefit (survives refresh, shareable debug URLs, server-renderable) outweighs the cost. If you hit a blocker, document it and fall back to localStorage only for the in-progress form data, never for the step indicator.

**Risk 3:** The Verification Report tab has 10 scorecard bars with expand/collapse.
Each row expands to show underlying checkpoint notes (from `verification_scorecard_details` JSONB keyed by category). Don't render all collapsed content on initial load — use `useState` per row and lazy-render expanded content.

**Risk 4:** Admin kanban drag-drop between columns.
`@dnd-kit/core` works well but the reorder logic needs a stable sort key. Add a `leads.sort_order` integer column, default 0, update on drag. Don't use array index as key.

## Acceptance criteria for session end

Run `pnpm build` and `pnpm start`. Then manually verify:

1. [ ] Homepage at `/` renders with all sections from design, featured plots come from Supabase (seed 4 test listings)
2. [ ] Listings at `/farmland` renders grid, at least one filter works end-to-end (district filter), URL updates on filter change
3. [ ] LDP at `/plot/[any-seed-slug]` renders all tabs, Verification Report tab matches design pixel-close, scorecard bars expand
4. [ ] Reserve flow completes all 4 steps, writes to `reservations` table, URL state survives refresh
5. [ ] `/admin` login works, dashboard KPIs show real counts, activity feed has at least 3 seeded events
6. [ ] `/admin/leads` kanban renders, dragging a card between columns persists to database
7. [ ] `/guides/section-79a-b-karnataka-farmland-buyers-2026` renders the article with TOC, callouts, and related guides
8. [ ] `DESIGN_DEVIATIONS.md` exists and documents any visual choices that diverge from Claude Design outputs
9. [ ] Playwright smoke tests pass for all six page routes
10. [ ] Agent attribution renders on listing cards and LDP for listings with `agent_id`; renders `Verified by TruePlots` alone for null agent listings
11. [ ] `agents` table created with 5 seed rows; `listings.agent_id` column exists and is nullable; 10 of 12 seed listings linked to agents, 2 null
12. [ ] Commit message on merge: `feat: session-2 ui integration - homepage, listings, ldp, reserve, admin, article, agent-attribution`

## Seed data to create

Before testing, create a seed script at `scripts/seed-session-2.ts` that inserts:

* 1 admin user (matching credentials for local login)
* 4 verifier users (Kushal K., Ravi M., Priya S., Arun T.) — used for `verified_by_user_id`
* 12 listings across 5 districts (Mandya 4, Mysore 3, BLR Rural 2, Ramanagara 2, Tumkur 1), prices from ₹40L to ₹2.8Cr, 4 marked `is_featured=true`
* Each listing has full verification data (scorecard JSONB, findings, flags, 5 trust chips minimum)
* 8 leads across 5 pipeline stages (New, Contacted, Qualified, Site Visit, Closed)
* 6 activity log events dated within last 24 hours
* 3 upcoming site visits in next 7 days
* 2 verifications due this week
* 1 MDX article (79A/B seed file)
* 1 sample reservation in `confirmed` status

Seed data must be idempotent (re-runnable without duplicates) — use `upsert` on stable keys.

## Out-of-scope escape hatch

If you encounter a decision this prompt doesn't cover and can't resolve by reading the design exports or `DESIGN_SYSTEM.md`, add a line to `SESSION_2_QUESTIONS.md` and make a reasonable default choice documented inline. Don't block the session on ambiguity. The founder will review questions at end of session.

## End state

At session end, `main` branch should have:

* All six pages building and rendering with real or seed data
* Admin kanban as the one fully-CRUD flow proving the data layer works end-to-end
* A deployed preview on Vercel (trigger via `vercel --prod=false`) that the founder can open on phone and review
* `DESIGN_DEVIATIONS.md`, `SESSION_2_QUESTIONS.md`, and updated `README.md` with session notes

Commit as: `feat: session-2 ui integration` — rebase-merge to main, no squash (we want per-component commits visible).

Session 3 will pick up with admin CRUD (listings add/edit/publish flows, verification workflow, lead editing). Session 4 adds integrations (WhatsApp OTP, HubSpot webhooks, Razorpay, PDF gen). Session 5 is content + polish + production deploy.
