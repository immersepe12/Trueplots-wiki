# TruePlots Page-Level Spec

*Page-by-page wireframe description. Each page references Spinny's equivalent. Fractional flow has no Spinny parallel — designed from first principles.*

> **⚠️ UPDATED 2026-04-19 post-screenshot analysis.** Screenshots captured from Spinny revealed several patterns that the text-research-only first pass missed. Key corrections are flagged inline as **[UPDATED]** blocks. Full derivation in [`11-spinny-ui-ux-analysis.md`](11-spinny-ui-ux-analysis.md). Clean consolidated design system at [`12-trueplots-design-system.md`](12-trueplots-design-system.md).

---

## 1. Homepage (/)

### Spinny reference
Title tag: "Buy and Sell Used Cars with Guaranteed Love." Homepage hero is **photo-first** ("the master / India's most-trusted car home" with dominant car photograph + single CTA). Buy/Sell hero duality (two variants). CTA pink (#ed264f). Trust signals repeated inline across listings AND LDP.

### TruePlots spec

**[UPDATED] Hero section (above fold):**
- **Layout:** Photo-dominant (~60-70% of above-fold is the photograph). Text overlays are short.
- **H1:** Short, punchy headline — 2-4 words max. Candidates: "own it truly" / "every plot, verified" / "the trust layer" — A/B test for emotional winner. Avoid the longer "Own plots you'll actually trust" headline from earlier draft.
- **Sub:** One line, 7-12 words. "India's most-trusted plots marketplace" or similar.
- **Primary CTA:** Single CTA only. "View all plots" (earthy green primary button).
- **Hero duality:** Two hero variants with toggle — **Buy** (farmland or urban plot photograph, "View all plots" CTA) and **Sell** (owner photographed on their plot, "List your plot" CTA). Mirror Spinny's buy/sell hero pattern.
- **Visual direction:** single dominant photograph per hero variant. Real plot with real conditions. NO split-screens, NO blueprint overlays, NO stock farmhouse imagery.

**[UPDATED] Secondary sticky filter bar below main nav** (mirrors Spinny's pattern in screenshot 14/15):
- Quick-access filter dropdowns: Price Range / Make (Taluk) / Year of approval / Zoning / Size / Facing / Verification tier — collapse when scrolling, sticky on scroll-up

**Below fold, in order:**
1. **Four-pillar promises** (named consistently, matches Spinny's 4-card benefits pattern in screenshot 03). Replace earlier "trust strip" concept:
   - **120-Point Verification** — every listing legally + physically checked
   - **12-Month Title Protection** — defect indemnity included
   - **7-Day Refund Window** — title-defect refund post-registration
   - **Fixed Price Assurance** — no haggle; price matches verification
   Four cards, each with an icon, photograph, title, one-line description. CTA "Browse plots" center.
2. **Quick search** — tabs [Farmland | Urban plots] + location + budget + size → search
3. **Recently viewed plots** (if logged in) — 4-6 cards carousel
4. **How TruePlots Works** — 3-step visual (mirrors Spinny's 3-illustration pattern in screenshot 05): **Choose** (20,000+ verified plots) → **Site visit** (at your time) → **Own** (registration + individual khata)
5. **Featured plots** — tabs [Best for you | Newly added]
6. **Explore by category** — Urban site / Farmland / Villa plot / BDA / BMRDA / BBMP / A-Khata (body-type-equivalent)
7. **Popular locations** — grid of 12 locations (Kanakapura 40+ plots, Devanahalli 25+, etc.)
8. **[NEW] Plots across South India** — city cards with counts: "Bangalore: X verified plots · 0 disputes" / "Mysore: Y verified plots" (mirrors Spinny's "Cars across India" in screenshot 09)
9. **[NEW] Explore More — 4 adjacent-service cards** (mirrors Spinny's Loan/Buyback/FASTag/Challan in screenshot 10): **Verify** (standalone verification on any plot) / **Register** (stamp duty + Kaveri) / **Convert** (agri→residential) / **Construct** (farmhouse/home design)
10. **[NEW] TruePlots Buzz** — press coverage wall with media logos (YourStory, Inc42, ET, Moneycontrol) as TruePlots gains coverage (mirrors Spinny Buzz pattern in screenshot 11). Gate until first coverage secured.
11. **[NEW] "Insights That Drive Us" stats banner** — concrete proof numbers only (display when real; don't fake): "4.X/5 rating / Y% buyers via referral / Z% close post-site-visit / N plots verified" (mirrors screenshot 12). **Wait until post-50 deals to deploy.**
12. **[NEW] "Over N TruePlots Stories"** — Instagram-style video testimonial grid with #TruePlots hashtag (mirrors Spinny Love Stories in screenshot 13). Gate until 20+ video-consented buyers.
13. **Fractional callout** — "Can't afford it alone? Buy with 2–3 other verified buyers. Each gets individual title." → "Learn about joint-buying"
14. **Trust logos** — bank partners (HDFC, ICICI, Axis logos) + press logos
15. **FAQ** — 6-8 common questions (test drive, loan, money back, inspection, process, fractional) — matches Spinny's FAQ pattern in screenshot 13/29
16. **Footer** — standard + "Managed by [entity name]" disclaimer (mirrors Spinny's PureRide disclaimer pattern)

### Where it differs from Spinny
- Spinny's hero is brand-emotional ("the master"). TruePlots' hero lands on "trust" because plot buyers' emotional load is anxiety about fraud, not joy.
- Fractional callout has no Spinny parallel (Spinny doesn't do fractional).
- Press-coverage wall and stats banner should be gated until real numbers exist — don't fake proof.
- The Sachin Tendulkar hero variant Spinny deploys (screenshot 14) is out of scope for TruePlots v1 — celebrity endorsement requires post-traction capital (see [09-what-does-not-translate.md](09-what-does-not-translate.md)).

---

## 2. Search / Listings page (/plots, /farmland)

### Spinny reference
Left sidebar filters; card grid; sort dropdown; "Customized Quick Filters" at top. Cards show year, KMs, price, "Spinny Assured" badge, EMI-starts-from.

### TruePlots spec

**Layout:** Left sidebar filters (25%) + main card grid (75%) on desktop. Collapsed drawer filters on mobile.

**Filters (left sidebar):**
- **Type:** Farmland / Urban plot (tab at top)
- **Location:** Taluk / Locality multi-select + radius
- **Budget:** slider ₹10L–₹5Cr
- **Size:** slider (sqft for urban, acres for farmland)
- **Approval/classification:** A-Khata / BDA / BMRDA / BBMP / Agricultural / Converted / Layout-approved
- **Facing:** N/E/S/W (urban)
- **Road width:** >20ft / >30ft / >40ft
- **Corner plot** (urban) / **Road frontage** (farmland)
- **Water source** (farmland): Borewell / Open well / Lake proximity
- **Verification tier:** Premium / Verified / Conditional
- **Fractional-eligible:** Yes/No
- **Drive-time from Bangalore:** <1hr / 1–2hr / 2–3hr (farmland)

**Sort:**
- Recommended (default; TruePlots algorithmic score)
- Price low-high
- Price high-low
- Recently added
- Verification score (120/120 first)
- Closest to Bangalore

**[UPDATED] Card design (each listing) — with per-plot hand-written micro-tag:**
```
[Photo — primary image with subtle verification badge bottom-left]
[Price] ₹45.5L  |  [EMI] From ₹32,000/mo
[Title row] 30×40 BDA plot — Kanakapura Rd
[Specs line] 1,200 sqft · A-Khata · North facing · 40ft road
[Micro-tag — HAND-WRITTEN per plot by editorial ops] "Corner plot · Morning sun · 5 min from metro"
[Verification] TruePlots Verified 80/80 · [tier badge] Premium
[Fractional flag if eligible] 🤝 Join 2 others — your share from ₹15L
[CTA row] View details · Book site visit
```

### [NEW] Inline content inside the listings grid (per screenshots 17, 19)
- After ~6 rows of cards: **Spinny-benefits-style strip** — 4 purple cards with TruePlots pillars (7-day refund / 120-point verification / 12-month title protection / Fixed pricing)
- After ~12 rows of cards: **inline service cards** as grid items (not sidebar) — **Orange card** "Pre-approved plot loan · Same-day decision · No impact on credit score" + **Purple card** "Joint buy from ₹40L · Individual title · Verified co-buyers"
- After ~18 rows: **Lead capture form** — "Let us help you find the right plot. Share mobile; we'll call back in 24 hours"

### [NEW] Top-of-listings triple-banner carousel (per screenshot 16)
Three rotating banners above the grid:
- "12-month title protection included on every verified plot"
- "TruePlots Capital — financing made possible for every plot buyer"
- "Joint buying · 2-4 verified buyers · individual titles"

### Where it differs from Spinny
- No "KMs driven" equivalent — replaced by "Year of approval" and "Verification tier"
- Fractional eligibility flag on card (Spinny has no parallel)
- "Drive-time from Bangalore" — unique to plots where commute/weekend-use matters
- **[UPDATED] Per-plot micro-tag is operationally unique to plots** — Spinny has same pattern on cars; TruePlots must hire editorial ops headcount to author these

---

## 3. Listing detail page (/plot/[id])

### Spinny reference
Tab-based layout (Overview / Report / Spinny Benefits / Features & Specs / Finance). Sticky right-side price block. Trust copy embedded IN CTA button ("BOOK NOW 100% refundable"). Quality report shows "1573 parts evaluated by 5 automotive experts" + 5 category scores /10 + trust chips ("Meter not tampered / Non-flooded / Core structure intact"). Reserve amount ₹5,000.

### TruePlots spec — MAJOR REWRITE post-screenshots

**[UPDATED] Above-fold layout (desktop):**
- **Left ~60%:** Photo gallery + thumbnail strip below + "Click to view drone walkthrough" badge top-right (farmland) / "Click to view 360° site tour" (urban)
- **Right ~40% — STICKY on scroll:** Price block stays fixed visible as user moves through tabs
  - Year/size chips top (e.g. "1,200 sqft · A-Khata · BDA · North facing")
  - "Site visit available at: [location]" icon row
  - Verification micro-tag: "Low PTCL risk, clean 30-yr chain"
  - Price: ₹45.5 Lakh (large, bold)
  - "+ Registration & stamp duty" small subtext
  - "or ₹32,000/m Starting EMI · Calculate your EMI" (secondary)
  - **Two primary CTAs stacked:**
    - Purple "BOOK SITE VISIT · 100% refundable" (trust copy on button)
    - Red "RESERVE PLOT ₹5,000" (low-friction hold)
  - "Share with a friend" row: WhatsApp / X / Facebook / Email icons

**[UPDATED] Body uses TAB navigation (not long-scroll):**

Tabs in order: **Overview · Verification Report · TruePlots Protection · Specifications & Features · Financing**

---

### Tab 1: Overview (default)

- **"Reasons to buy"** — 3-5 hand-written bullet points by editorial ops, unique per plot. Examples: "Corner plot · Morning sun exposure" / "5 min drive from upcoming metro station" / "Clean 30-year title chain, no PTCL risk" / "Pre-approved for 75% plot loan from HDFC"
- **Plot Overview** — structured specs grid (Survey number, Approval authority, Khata type, Facing, Size, Frontage, Road width, etc.)
- **Location block** — embedded map (Google + KGIS overlay), plot boundary drawn, key amenities pinned
- **Fractional flag** (if eligible) — "Available for joint purchase by 2-4 buyers. Learn how it works →"
- **Service commitment line** — "Khata transfer guaranteed within 45 days post registration"

### [UPDATED] Tab 2: Verification Report — THE key tab

Mirror Spinny's quality-report format (see screenshot 23):

- **Header:** "120-point verification · 48 documents reviewed · 12 database cross-checks · 4 field verifications · 3 legal experts signed off"
- **Trust chips row (green checkmarks):** "PTCL clear · Non-encumbered · 79A/79B compliant · Boundary matches KGIS · Title chain intact"
- **Score grid — 10 categories each with /10 score + Clean/Minor/Resolved label**:
  - Ownership & Title Chain: 10/10 Clean
  - Revenue Records & Mutation: 9.8/10 Clean
  - Zoning & Land Use: 9.5/10 Clean
  - Boundary & Survey: 10/10 Clean
  - Encumbrance & Liens: 10/10 Clean
  - Road Access & Approach: 9.0/10 Clean
  - Water Source (farmland only): 8.5/10 Good
  - Litigation & Disputes: 10/10 Clean
  - Physical Site: 9.5/10 Clean
  - Tax & Compliance: 10/10 Clean
- **"View full report" CTA** — NOT gated, open on page (like Spinny's transparency)
- **Service commitment:** "Next legal recheck at 12 months or registration milestone (whichever earlier)"

### Tab 3: TruePlots Protection

Mirror Spinny's "Spinny Benefits" tab (screenshot 24):
- **Badges row:** 120-point verified · 12-month title protection · 7-day refund · Fixed price · Registration support · Khata transfer
- **Protection plans section** — expandable cards:
  - **Title indemnity (bundled)** — 12-month coverage up to 50% property value, ₹0
  - **Extended title protection** — 60-month coverage up to 75% property value, ₹25K-75K per buyer
  - **Construction protection** — partner insurance for buyers building, quote on request

### Tab 4: Specifications & Features

Mirror Spinny's Features tab (screenshot 25):
- **Top features** grouped by category: Location & Access / Legal & Approvals / Physical Features / Utilities
- Checkmarked items (e.g. "Corner plot", "North facing", "40ft road frontage", "A-Khata approved", "Borewell with 2000 GPH yield", "Electricity connection ready")
- "View all specifications" expand link

### Tab 5: Financing

Mirror Spinny's Finance tab (screenshot 26):
- EMI calculator with sliders: Loan Amount / Down Payment / Duration
- Output panel: Principal, Total Interest, Total Amount
- "Check Eligibility" CTA → pre-approval flow (soft credit pull)
- Disclaimer: "Applicable rate subject to bank credit profile. Loan approval at sole discretion of partner bank."
- Partner bank logos

---

### Below tabs (always visible):
1. **Similar plots** — 4 cards, same location/size/zoning (curated, not ML)
2. **Explore More** — contextual links: "Plots in Kanakapura 40-60L" / "Joint-buying in Mandya" / "BDA plots under ₹1Cr"
3. **TruePlots Stories** — video testimonial row (once we have content)
4. **FAQ specific to this plot** — 4-6 pre-populated answers by editorial ops

### Mobile-specific
- Sticky floating CTA bar at bottom: "BOOK SITE VISIT 100% refundable" + WhatsApp icon
- Tab navigation converts to horizontal scrollable tabs
- Photo gallery swipeable
- Score grid collapses to single-card scroll

---

## 4. Verification Methodology page (/how-we-verify)

### Spinny reference
Spinny's /spinny-assured and /how-it-works pages — category explainer + trust guarantees.

### TruePlots spec

**Hero:**
- "We check 120 things before you see a farmland listing. Here's the list."
- Sub-copy: "Most marketplaces show you a photograph and a phone number. We do the legal and physical homework first."

**Body:**
- **Section 1:** The 10 categories (farmland) — each category: title, icon, 2-sentence description, "Sample checks include..." 3–4 bullet points
- **Section 2:** Urban version (tab toggle): 9 categories for urban plots
- **Section 3:** "What we DON'T do" — honest disclaimer
  - We're not a substitute for your lawyer's final review
  - We don't guarantee future appreciation
  - We can't predict regulatory changes (e.g., 79A/79B reversal)
  - We don't verify seller creditworthiness (that's your bank's job)
- **Section 4:** "Who does the verification" — team composition, experience (mirror Spinny's ex-Audi/BMW framing — "Our verification leads are ex-revenue-department officers with 10+ years of Karnataka land record experience")
- **Section 5:** "What happens when we find a problem" — 3 outcomes: reject, flag, resolve-before-listing
- **Section 6:** Downloadable sample verification report (PDF) — lets buyers see what they'd get

**CTA footer:** "Browse verified plots" + "Talk to a verification specialist"

---

## 5. Fractional buyer flow (/joint-buying, /plot/[id]/join-pool)

### Spinny reference
None — designed from first principles.

### TruePlots spec

**Entry points:**
1. Fractional flag on listing card → "Join pool" CTA
2. /joint-buying landing page (SEO target: "how to jointly buy farmland Karnataka")
3. Homepage fractional callout

**Landing page (/joint-buying):**

- **Hero:** "Own ₹1.5Cr farmland for ₹40L. Legally. With individual title."
- **Sub:** "Join 2-3 other verified buyers. We handle the subdivision, legal structuring, and individual khata for each owner."
- **How it works:** 5-step visual
  1. Get verified (short onboarding — budget + intent + timeline)
  2. Join a pool (ongoing pools for plots that other buyers have expressed interest in, OR create your own)
  3. Agree on subdivision (we propose; all buyers approve)
  4. Register jointly (escrow-based; each buyer pays their share directly)
  5. Individual titles (subdivision completed over 3-6 months; each buyer gets own khata)
- **Case study:** "Ravi and 3 friends bought a 7-acre Kanakapura plot together — here's how" (case study style)
- **FAQ:** 15 common questions (co-owner conflicts, exit, taxation, construction rights, what if one buyer pulls out)
- **CTA:** "Browse fractional-eligible plots" or "Get on the waitlist"

**Join pool flow (from listing page):**

Step 1 — Express interest
- Form: budget share, intent (hold / build / resale), construction timeline, exit horizon, co-buyer preferences (any friends/family? willing to pool with strangers?)
- Soft commitment — no payment yet

Step 2 — Pool status
- "This pool currently has 1 other verified buyer. Need 2 more to proceed."
- Estimated pool-formation time based on historical data

Step 3 — Compatibility check
- Once pool has 3-4 buyers, TruePlots runs compatibility check: timelines, intents, construction plans
- If compatibility issue, show to all buyers and let group decide

Step 4 — Subdivision plan approval
- TruePlots + surveyor propose subdivision
- All buyers review and approve/request changes
- Once approved, refundable ₹50K deposit per buyer to lock

Step 5 — Escrow + registration
- Each buyer's funds enter escrow
- Joint registered sale deed executed
- Each buyer receives co-ownership interest

Step 6 — Subdivision execution (3-6 months)
- Partition deed → phodi → mutation → individual khatas
- Progress tracker visible to each buyer

Step 7 — Individual titles issued
- Each buyer receives own khata
- Pool is dissolved; buyers are now independent plot owners

### Critical UX notes
- **Transparency throughout** — every buyer sees every other buyer's basic info (name, intent, timeline) before committing. No surprises.
- **One buyer's pullout pre-registration** — remaining buyers can wait for a replacement OR exit with refund
- **One buyer's pullout post-registration** — handled via partition-deed terms; typically requires remaining buyers to buy out the exiting buyer at fair value (pre-defined in pre-purchase agreement)

---

## 6. Financing / EMI page (/financing)

### Spinny reference
/used-car-loan-emi-calculator + Spinny Capital blog

### TruePlots spec

**Hero:**
- "Check plot loan eligibility in 3 minutes. No impact on your credit score."
- Pre-approval form directly embedded

**Body:**
- EMI calculator (primary tool)
- Partner bank logos (trust signal)
- Loan-to-value guide (why plot loans are 60-75% LTV, not 100%)
- B-Khata warning: "We don't list B-Khata plots because they can't get mainstream home loans. [Why]"
- Agri-loan pathway: "Buying farmland? Here's how agricultural-income buyers can access NABARD-channel loans"
- FAQ: 15 common plot loan questions

---

## 7. Services page (/services)

### Spinny reference
/how-it-works (Spinny's service layer explainer)

### TruePlots spec

**Top-level services:**
1. **Verification** — every listing included; standalone for external plots at ₹15-20K
2. **Registration** — stamp duty advisory + Kaveri booking + document drafting at ₹15-25K
3. **Khata transfer** — post-registration, ₹5-15K
4. **Land conversion** — for agricultural-to-residential at ₹25-75K + govt fees
5. **Fractional coordination** — joint buying + subdivision + individual khata at ₹40-75K per buyer
6. **Construction services** — architect + GC referrals with margin (varies)
7. **Title indemnity (extended)** — 60-month premium SKU at ₹25-75K per buyer

Each service has a dedicated sub-page with: what's included, timeline, pricing, FAQ, CTA.

---

## Navigation structure

**Primary nav:**
- Buy → [Farmland | Urban plots | Joint buying]
- Services
- How we verify
- Financing
- About
- Login / Sign up (top-right)

**Footer:**
- Company (About, Team, Press, Careers)
- Buy (Farmland, Urban plots, Joint buying, Services, Financing)
- Legal (T&C, Privacy, RERA disclosures, Complaint handling)
- Resources (Blog, Glossary, Legal guide, Case studies)
- Contact (WhatsApp, phone, email, office address)

---

## Mobile-first considerations

- Sticky floating CTA bar on all listing pages: "Book Site Visit" + "WhatsApp us"
- WhatsApp-first lead capture matches South Indian buyer behavior (brief §11.2)
- Pre-approval flow fully mobile-optimized
- Photo gallery swipeable, 360° walkthrough touch-friendly
- Collapsible accordions for verification detail, specs, FAQs

---

## Design language notes

- **Primary color:** earthy green (TruePlots verified badge) — distinguishes from Spinny's pink/red, from Swasya's eco-spiritual green, from MagicBricks' aggressive red
- **Secondary color:** warm clay/terracotta — plot/land association without being eco-kitsch
- **Typography:** confident, direct, grown-up (per brief §9.3). Avoid aspirational flourish and transactional budget-portal feel.
- **Photography:** real plots with real conditions. NO stock farmhouse imagery.
- **Icons:** functional and clear. Avoid ornamental or lifestyle-aspirational.
