# Handoff prompt for a new Claude Code session

*Kushal is starting a fresh Claude Code chat. This is the prompt to paste at the top of that chat so Claude Code has full context before doing any work. After this, paste the next sprint prompt (`sprint-beta-co-buying.md` is staged in the same folder).*

*Last updated: April 21, 2026.*

---

## Paste everything below into the new Claude Code chat as your first message

---

# TruePlots — orientation for this session

You are picking up an in-progress project. Read this carefully before writing any code.

## What TruePlots is

TruePlots is a verified plots marketplace for South India with a built-in fractional facilitation layer. Every listing is legally verified by a 120-point checklist before buyers see it. Plots too large for a single buyer can be jointly purchased by three buyers (two for urban 60×40 splits) — Delight Eco Farms acquires the parcel with its own balance-sheet capital, TruePlots handles legal subdivision, and each buyer receives an individually-titled parcel.

Two categories are in scope: farmland (hero, launching now) and urban residential sites (secondary, conditional on a three-gate check at month 4). Supply comes primarily from Delight Realty's 100+ trusted real estate agent network (via the Eshwar partnership). Every listing is jointly verified by the listing agent and TruePlots' verification team before going live.

Founder: Kushal (`kushal@exar.fit`). Co-founder: brother (operates Delight Eco Farms). Partner: Eshwar (Delight Realty agent network).

## Where the canonical docs live

The TruePlots repo is at https://github.com/immersepe12/Trueplots.in (working directory you are in).

The strategic docs live in two places — same content in both:

1. **In this repo**, at `/docs/`:
   - `trueplots-project-document-v4.md` (master strategy)
   - `trueplots-gtm-plan-v4.md` (12-month go-to-market)
   - `trueplots-project-pitch-v4.md` (external pitch)
2. **Separate dedicated docs repo** at https://github.com/immersepe12/Trueplots-wiki — has the same v4 docs plus `AGENTS.md`, `GLOSSARY.md`, `CHANGELOG.md`, plus all the supporting research and product specs. If you can clone or read it, do so before starting strategic work.

Read these in order:
1. `/docs/trueplots-project-document-v4.md` — sections 1, 3, 5, 6, 11 (executive summary, product, competition, positioning, risks)
2. `/docs/trueplots-gtm-plan-v4.md` — sections 1, 2, 3, 5, 6 (start position, goal, framework, phase 1, phase 2)
3. The Trueplots-wiki repo's `AGENTS.md` and `GLOSSARY.md` if you can access them

Do NOT skip the docs read. Strategic decisions are encoded there. India-specific terms (PTCL, 79A/B, A-Khata, BBMP, RERA, CIS) appear throughout — do not guess at their meanings, read the glossary.

## Decisions already locked — do not re-litigate

- Brand: TruePlots, Class 36 trademark filed, domain secured
- Positioning: "Access-First" — "Own premium farmland from ₹40 lakh" is the hero. Verification is infrastructure, not the headline.
- Business model: Facilitator, not developer. Customer funds never pool. CIS-proof.
- Scope: Farmland-first. Urban sites secondary, gated month 4.
- Urban launch rule: A-Khata only. B-Khata excluded at launch.
- Moat: Operational stack + agent network, not marketplace UI.
- Agent-inclusive model: agents are first-class platform participants. Listing card and LDP show "Listed by [Agent] · Verified by TruePlots" attribution. Full agent surfaces (landing page, profile pages, dashboard, scorecard) are month 3, not now.
- Three-layer verification framing: badge ("120-point verified") + LDP detail ("48 documents, 12 database checks, 4 field inspections, 3 legal experts") + 10-category scorecard with trust chips
- Spinny is a UX/service-layer model, NOT a business-model model. TruePlots does not buy and hold inventory.

## Stack

- Next.js 15.1, React 19, TypeScript strict mode
- Tailwind with design system tokens (Forest Green `#1F3D2E`, Paper White `#FAFAF7`, Harvest Gold `#C9A341`, Ink Black `#0F1712`, Charcoal `#4A5247`, Success Green for verification states, Alert Red for findings)
- Fonts: Fraunces (display headings), Inter (body), JetBrains Mono (data) — already loaded via `next/font` in Session 1
- Supabase (Postgres + Auth + Storage + RLS)
- Auth: Supabase Auth with role-based access. Roles: `buyer` (default), `admin`, `agent`, `verifier`. The `handle_new_user` trigger sets new signups to `buyer`.
- Deployed to Vercel at `https://trueplots-in.vercel.app/`
- MDX for content articles
- shadcn/ui primitives where applicable; otherwise hand-rolled Tailwind components

## What's been built so far (5 sessions shipped)

**Session 1 — Foundation** (commit `e56f905`, shipped earlier): Next.js scaffold, Tailwind tokens, fonts, Supabase schema (9 tables + RLS), auth middleware, login form, MDX pipeline, HubSpot stub.

**Session 2 — UI integration**: Six pages built end-to-end — homepage, /farmland (listings), /plot/[slug] (LDP with 5 tabs including the Verification Report), /plot/[slug]/reserve (4-step flow), /admin (dashboard + read-only listings + leads kanban with drag-drop), /guides/[slug] (article template). 12 seed listings + 5 seed agents + 8 seed leads.

**Session 2 cleanup**: All 404s eliminated on public surfaces. Built /co-buying, /services, /how-we-verify, /financing, /about, /contact, /privacy, /terms, /list-a-plot, /verified-only-alerts as real content pages. Coming-Soon stubs for /urban, /faq, /methodology, etc. District filter pages /farmland/{district}. Added 8 more seed listings (total 20). Real photographs via picsum (later swapped to satellite imagery via Esri World Imagery in `/public/plot-images/`).

**LDP slug fix** (commit `5a59d55`): Replaced fixture-only LDP rendering with a real Supabase adapter at `lib/queries/ldp-plot.ts`. Backfilled missing slugs.

**Session 3-lite** (admin CRUD + reserve fix): Reserve route 404 fixed via Supabase query. Payment removed from Step 3 — booking is now offline (`payment_status = 'pending_offline'`). Admin listings table got CRUD UI shell (action column with view/edit/delete icons, status filter pills, search, "+ New listing" CTA). Admin /reservations view added. Sidebar updated.

**Sprint α** (commit `d0b891d` + `97abbdd` + `1f6dae6` + later `91caf0e`, `f28cd47`): Buyer auth + dashboard + favourites + verification report page. Critical bug fixed: Session 1's `handle_new_user` trigger was auto-promoting EVERY signup to admin. Now defaults to buyer. Added `favorites` table + RLS, `/account/saved`, `/account/reservations`, `/account/activity` (stub), `/account/settings`. Heart icon on listing cards interactive, login-gated. `/plot/[slug]/verification-report` full 120-checkpoint page with sticky category nav and per-category breakdown. `reservations.buyer_user_id` FK + phone-match linking on signup so anonymous reservations attach to new accounts.

## Outstanding bug — fix this BEFORE starting Sprint β

**Symptom:** Multiple routes throw a server-side exception with Digest `1829522191` when the visitor is in a specific state:

| Route | Triggers when |
|---|---|
| `/signup` | User is already authenticated |
| `/login` | User is already authenticated |
| `/admin/listings/new` | Logged-in admin clicks "+ New listing" |
| `/admin/listings/[id]/edit` | Logged-in admin clicks any edit pencil |

Same digest across all four = shared root cause. The previous Claude Code session shipped error boundaries (`app/global-error.tsx` and `app/(public)/error.tsx` plus existing `app/(admin)/admin/listings/error.tsx`) so the actual error should now surface inline instead of the opaque Vercel placeholder. Schema was verified clean — `favorites` table and `reservations.buyer_user_id` are deployed.

### Step 1 — verify

1. Log in as admin (`kushal@exar.fit` — ask Kushal for the password)
2. Visit `/signup` → expected: redirect to `/admin` because middleware now does role-aware redirect for authed users hitting login/signup
3. If it still throws: screenshot the inline error message that the new error boundary should display, capture the full stack trace from Vercel logs (`vercel logs trueplots-in.vercel.app | grep -A 30 "1829522191"`)
4. Visit `/admin/listings/new` and `/admin/listings/[id]/edit` — same exercise

### Step 2 — diagnose

Likely root causes for this pattern:

- A Server Component returns `redirect(...)` from inside a try/catch — `redirect()` works by throwing the special `NEXT_REDIRECT` error, and a generic catch swallows it, then the next line runs against undefined data
- `cookies()` or `headers()` is called at module top level instead of inside a request scope
- A missing `SUPABASE_SERVICE_ROLE_KEY` env var on Vercel preventing the auth helper from reading user role server-side (the anon key is RLS-restricted)
- A Server Action runs without proper request context

Check Vercel env vars first. Then trace the request through `requireRole()` or whatever the role-check helper is called.

### Step 3 — fix and verify

Fix at the source. Then verify by:
1. Hitting all four routes signed out → forms render
2. Hitting all four routes signed in as admin → /signup and /login redirect to /admin; /admin/listings/new and /[id]/edit render the form
3. Hitting all four routes signed in as buyer → /signup and /login redirect to /account; /admin/* redirects to /account

Add Playwright tests covering all role × route combinations.

Commit as: `fix: digest 1829522191 server exception on auth-redirect routes (root cause: <fill in actual cause>)`

## Workflow conventions

- Slice large sprints into commits-per-slice and push between slices so the founder can preview on Vercel between landings
- Use Supabase MCP directly to apply migrations and seed data when possible
- Add Playwright E2E tests for every new user-facing path; run against live Vercel preview before declaring done (status code alone is insufficient — Next.js `notFound()` returns 200 with the 404 page, so check page title or h1 contents)
- Don't introduce new dependencies without need; prefer rolling primitives in Tailwind
- Don't redesign anything visually unless explicitly asked; the design system is locked
- When you ship something, write a tight summary of what changed + a test list. Don't bury bugs in success reports.
- The founder reviews via the live Vercel preview, not local. Make sure your verification runs against `https://trueplots-in.vercel.app/`, not localhost.

## Response style

The founder is Kushal — moves fast, has built startups before, dislikes preamble and hedging. Skip pleasantries. Write tight commit messages. Surface real issues bluntly once. Don't over-apologize. Don't ask permission for obvious next steps. Make calls and document them.

## What's next

After the digest 1829522191 fix lands and verifies, the next sprint is **Sprint β — Co-buying flow**. The co-buying mechanic is TruePlots' moat — without it, the product is just "verified 99acres". The Sprint β prompt is in a separate file (`sprint-beta-co-buying.md` in the docs folder) — Kushal will paste it after this fix verifies.

## Don't

- Don't run `npx skills add` or any other tool that creates artifacts in the repo without checking what it'll add — last session accidentally committed 215 files of skills-tool junk that needed manual cleanup
- Don't `git add -A` blindly — review the staged file list before committing
- Don't trust your own diff. Verify against the live Vercel preview, not local
- Don't extrapolate from a single test case — when the spec mentions "every plot", click 5+ different plots, not just the first one
- Don't add new features mid-sprint. Stay in scope. Document creep in a TODO file if it surfaces, do not silently expand
