# Spinny UI/UX Analysis from Screenshots — TruePlots Takeaway Plan

*Based on 30 screenshots captured April 19, 2026. Corrects earlier wireframe spec (file 07) where screenshot evidence differs from text research.*

---

## What the screenshots revealed vs what text research suggested

### 15 UI/UX patterns that only became visible with screenshots

| # | Pattern | What text research said | What screenshots show |
|---|---|---|---|
| 1 | **Hero is photo-first, not copy-first** | Assumed hero has descriptive sub-copy | Hero is ~2/3 above-fold photograph with single-word headline ("the master"), 7-word subtitle, ONE CTA |
| 2 | **Hero has buy/sell duality** | Not evident | Two hero variants: buy (blue car, "View all cars") and sell (yellow car, "Sell your car"). Likely toggle or rotation |
| 3 | **A separate Sachin Tendulkar hero variant exists** | Treated as TV campaign only | Screenshots 14-15 show a distinct homepage with Sachin, ancient architecture background, "zero down payment options" pink CTA, "Check eligibility" — a financing-first homepage variant |
| 4 | **4 promises, named consistently** | Knew there were trust guarantees | Exactly 4 pillars with fixed naming: **200-Points Inspection / Warranty Included / 5-Day Money Back / Fixed Price Assurance** — repeated verbatim across homepage, listings page, and LDP |
| 5 | **"1573 parts evaluated by 5 automotive experts" is the LDP claim** | Assumed 200-point was the consistent claim | LDP quality report actually says "1573 parts evaluated by 5 automotive experts" — a more granular claim. "200-point inspection" stays at badge level; "1573 parts / 5 experts" is the detailed-page framing |
| 6 | **Quality report shows NUMERICAL SCORES per category** | Assumed pass/fail dots | Actual format: 5 categories each with /10 score + Excellent/Good label. Core systems 9.6 Excellent, Supporting systems 9.2 Excellent, Interiors 9.5 Good, Exteriors 8.5 Good, Wear & tear 8.5 Good |
| 7 | **Trust chips inline: "Meter not tampered / Non-flooded / Core structure intact"** | Not visible in text research | Three green-check chips above the score grid — direct trust attacks against known fraud patterns |
| 8 | **LDP uses TABS not long scroll** | Assumed long-scroll with accordions | Tab navigation: Overview / Report / Spinny Benefits / Features & Specs / Finance. Content chunked into 5 named views |
| 9 | **Sticky right-side CTA block on LDP** | Implied but not detailed | Price + "BOOK NOW 100% refundable" + "FREE TEST DRIVE" remain fixed on right as user scrolls through tabs |
| 10 | **"100% refundable" is embedded IN the CTA button** | Assumed separate trust signal | Purple "BOOK NOW" button has "100% refundable" right below the CTA text — trust claim is ON the button itself |
| 11 | **Reserve amount is ₹5,000, not ₹50K or ₹10K** | Assumed higher per research | Cart page shows "Reserve this car for ₹5,000" — surprisingly low-friction hold amount |
| 12 | **Service categories = Loan / Buyback / FASTag / Challan** | Not evident from research | Homepage has 4 service cards beyond the purchase: Loan (finance), Buyback (resale), FASTag (toll), Challan (fines). Captures post-purchase retention |
| 13 | **Per-card micro-tags** | Generic card spec assumed | Every listing card has a hand-written single-line distinguishing tag: "Premium variant · 1 more reason to buy" / "Highly affordable & reliable" / "High quality, less driven" / "Award winner" / "4-year warranty" / "2 new tyres" — unique per listing |
| 14 | **Stats banner: concrete numbers displayed** | Not evident | "Insights That Drive Us" shows: **4.8/5 rating, 35% customers via referral, >70% conversion post test-drive, 32% women customers**. These are proof-metrics shown as hero stats |
| 15 | **Inline service banners INSIDE listings grid** | Assumed sidebar | Orange "Pre-approved loans / Same day delivery / No Cost EMI ₹1 lakh" + Purple "Buyback Guaranteed resale assurance 12/24/36 months" — embedded AS grid items among car cards, not sidebar |

### Additional granular observations

- **"Spinny benefits" purple-card strip appears INSIDE the listings page** — trust reinforcement mid-browse, not just homepage
- **Tripe-banner carousel at top of listings page**: "3-year warranty on Assured+ cars god promise" + "CAPITAL Financing made possible for every car buyer" + "Home comfort Buy comforting"
- **"god promise"** — regional Indian phrase (Indian English colloquialism). Very on-brand.
- **Inventory count prominent** — "889 Used cars in Bangalore" heading. Builds scale perception.
- **Secondary sticky filter bar** below main nav: Price Range / Make and Model / Year / Fuel / KM Driven / Body Type / Transmission — quick-access below main header
- **Cars across India cards** show both hubs AND cars: "11 hubs · 1300+ cars" (Delhi), "7 hubs · 880+ cars" (Bangalore). Different visual color per city (yellow, purple, green, dark purple)
- **Spinny MAX brand tile** appears in Popular Brands — positioned as a brand alongside Hyundai, Maruti, Tata. Premium tier positioning strategy
- **#myspinny** hashtag — Instagram-style video testimonials. "Over 2 Lakh Spinny Love Stories" as the counter
- **Spinny Buzz = press wall** — Financial Express, Economic Times, AFAQS, Dainik Bhaskar logos with thumbnail coverage. Credibility anchor
- **FAQ appears on LDP AND homepage** — same structure, different answers (test drive, loan, money back, inspection, process)
- **"Managed by PureRide Technologies Private Limited"** footer disclaimer — legal entity visibility
- **WhatsApp/X/Facebook/Email share icons** directly in LDP right-block — referral as primary pathway (backs up the 35% referral stat)
- **Service commitment line on LDP**: "Next service due after 12 months or 10,000 km (whichever comes first post delivery)" — post-purchase SLA explicit
- **₹4,000 RC transfer facilitation line item** in checkout — itemized, not bundled
- **FASTag + fuel "was ₹6,700, now Included"** — free upgrade signalling, very Indian D2C pattern
- **"Reservation will end in 3 days"** — honest time pressure, not aggressive countdown

---

## Corrections to `07-trueplots-page-specs.md`

Based on screenshot evidence, the following spec items need updating:

### Homepage (file 07 Section 1)

- **CORRECT:** Hero is photo-dominant, headline short. My spec had too much copy.
- **ADD:** Buy/Sell hero toggle (two states) — applicable to TruePlots too (buyer-journey vs seller-journey)
- **CORRECT:** Service grid should have 4 adjacent service cards below hero: For TruePlots these should be **Verify / Register / Convert / Construct** (mirrors Spinny's Loan / Buyback / FASTag / Challan pattern — post-purchase retention categories)
- **ADD:** Stats banner — TruePlots equivalent: "120-point verification / X deals closed / Y% title-defect-free / Z% fractional deals via referral"
- **ADD:** Press coverage wall — TruePlots Buzz with logos from coverage we secure
- **ADD:** Video testimonial grid — "Over N Happy Plot Owners" with #TruePlots hashtag

### Listings page (file 07 Section 2)

- **CORRECT:** Inventory count in header ("X Verified Plots in Karnataka")
- **ADD:** Triple-banner carousel at top — "12-month title protection" + "TruePlots Capital financing" + "Joint-buying from ₹40L"
- **ADD:** Inline Spinny-benefits equivalent strip — 4 purple cards with TruePlots pillars after ~6 rows: **7-day title-defect refund / 120-point verification / 12-month title protection / Fixed pricing assurance**
- **CORRECT:** Inline service cards within grid (NOT sidebar): "Pre-approved plot loan" (orange) + "Joint buy from ₹40L" (purple) — embedded as grid items among listings
- **ADD:** Per-card micro-tags — mandate hand-written 3-5-word distinguishing line per listing. Examples: "Corner plot · Mango grove" / "Low PTCL risk, clean chain" / "Premium BDA A-Khata" / "Lake frontage · Bore water"
- **ADD:** Lead capture embedded mid-listings — "Let us help you find the right plot" with mobile + callback

### Listing detail page (file 07 Section 3)

- **CORRECT:** LDP uses TABS, not long-scroll: **Overview / Verification Report / TruePlots Protection / Specifications & Features / Financing**
- **CORRECT:** Sticky right-side CTA block — Price, EMI, "BOOK SITE VISIT 100% refundable", "RESERVE PLOT ₹5,000" remain visible as user scrolls tabs
- **CORRECT:** Trust copy ON the CTA button — "BOOK SITE VISIT 100% refundable" (mirror Spinny's "BOOK NOW 100% refundable" pattern)
- **ADD:** Trust chips above verification score: "PTCL clear · Non-encumbered · 79A/79B compliant"
- **CORRECT:** Verification report shows **numerical score per category**, not just dots. 10 categories each scored out of 10 with "Clean/Minor-flag/Resolved" label. Example: Ownership 10/10 Clean, Revenue Records 9.8 Clean, Zoning 9.5 Clean, Boundary 10/10 Clean, etc.
- **ADD:** "Reasons to buy" hand-written bullets — unique per plot. Example: "Premium corner plot · More morning sun" / "Pre-approved for 75% plot loan" / "5 min from upcoming metro"
- **ADD:** "Share with a friend" WhatsApp-first row in price block — referral UX at highest-intent moment
- **ADD:** Service commitment line: "Khata transfer guaranteed within 45 days post registration"
- **ADD:** FAQ at bottom of LDP (separate from homepage FAQ) — plot-specific questions

### Cart / Reserve flow (NEW — was not in file 07)

- **Reserve for ₹5,000** (not ₹50K) — match Spinny's low-friction hold
- **3-step stepper:** Plot selected → Site visit preferences → Payment
- **Passive loan opt-in** — "Interested in plot loan?" checkbox (not forced)
- **Two site-visit options:** "Request at Plot Location" / "At TruePlots Office" — big button choice
- **Itemized price breakdown:**
  - Plot price: ₹X,XX,XXX
  - Registration facilitation: ₹15,000
  - Verification premium (already paid): included
  - Final amount: ₹X,XX,XXX
- **"Reservation will end in 3 days"** — honest time pressure
- **"100% refundable"** footer line

---

## The critical pattern I missed: "1573 parts / 5 experts" granularity

Text research showed "200-point inspection" as Spinny's headline trust artifact. Screenshots show something more sophisticated:

- **Marketing badge level:** "200-Points Inspection" — round, memorable, repeated everywhere
- **LDP detail level:** "1573 parts evaluated by 5 automotive experts" — granular, human-expert-framed
- **Score-visible level:** 5 category scores /10 + specific trust chips (Meter not tampered, Non-flooded, Core structure intact)

**Implication for TruePlots:** The "120-point verification" I specced is the badge level. TruePlots needs THREE layers of granularity:

1. **Badge:** "120-point verification" (memorable, repeated)
2. **LDP detail:** "48 documents reviewed · 12 database cross-checks · 4 field verifications · 3 legal experts" (specific, human-anchored)
3. **Score-visible:** 10 category scores /10 + trust chips (PTCL clear · Non-encumbered · 79A/79B compliant · Boundary matches KGIS · Title chain intact)

This three-layer structure needs to be built into the product spec. I've updated the analysis accordingly.

---

## Revised TruePlots Takeaway Plan — 15 build priorities

Re-ranked based on screenshot evidence. Priorities marked ⭐ changed position from earlier plan.

### Tier 1 — Launch essentials (months 1–3)

1. **Three-layer verification framing** ⭐ (new)
   - Badge: "120-point verification"
   - LDP detail: "48 documents / 12 database checks / 4 field verifications / 3 legal experts"
   - Score-visible: 10 category scores /10 + trust chips

2. **Photo-first homepage hero** ⭐ (revised)
   - Single-word or short-phrase headline over dominant photograph
   - Buy/Sell hero duality toggle
   - Single primary CTA

3. **Four pillar promises named consistently**
   - 120-Point Verification / 12-Month Title Protection / 7-Day Title-Defect Refund / Fixed Price Assurance
   - Repeat verbatim across homepage, listings, LDP

4. **Fixed pricing + "Why this price?" explainer next to verification score**
   - Direct Spinny copy: price and verification reinforce each other

5. **Trust copy EMBEDDED in CTA buttons** ⭐ (new)
   - "BOOK SITE VISIT 100% refundable"
   - "RESERVE PLOT ₹5,000 refundable"
   - Trust claim is ON the button, not next to it

6. **Sticky right-side CTA block on LDP** ⭐ (new)
   - Price / EMI / 2 CTAs / social share row — fixed as user scrolls tabs

7. **LDP uses tab navigation, not long-scroll** ⭐ (revised)
   - Overview / Verification Report / TruePlots Protection / Specifications & Features / Financing

8. **₹5,000 refundable reserve to hold plot for 3 days** ⭐ (new — lower than earlier spec)
   - Low-friction hold + honest 3-day countdown

### Tier 2 — v1.5 (months 4–6)

9. **Per-listing hand-written micro-tag** ⭐ (new)
   - Every listing card has a 3-5 word distinguishing line
   - Operational: verification team adds the tag during listing intake
   - Examples: "Corner plot · Mango grove" / "Low PTCL risk · Clean chain" / "Lake frontage · Bore water"

10. **Stats banner with concrete proof numbers** ⭐ (new)
    - "X verified plots · Y% title-defect-free · 35% buyers via referral · 4.8/5 rating" style
    - Wait until we have real numbers (minimum 50 deals) before deploying

11. **Inline benefits strip inside listings page**
    - Purple-card reinforcement mid-browse — trust signals don't stay on homepage

12. **Inline service cards within listings grid**
    - "Pre-approved plot loan" (orange) + "Joint buy from ₹40L" (purple) — embedded among listings

13. **WhatsApp-first share row on LDP price block** ⭐ (new)
    - Single-click WhatsApp share is the highest-converting referral UX in India

### Tier 3 — v2 (months 6–12)

14. **4 post-purchase service cards on homepage**
    - Verify / Register / Convert / Construct — mirror Spinny's Loan/Buyback/FASTag/Challan retention pattern

15. **#TruePlots video testimonial grid** ⭐ (new)
    - Instagram-style square cards with real buyer stories
    - "Over N happy plot owners" counter
    - Wait until we have 50+ video-consenting buyers

---

## Specific anti-patterns to AVOID (observed in Spinny but wrong for TruePlots)

Most of Spinny's patterns translate. Three do NOT:

1. **Spinny's "god promise" regional colloquialism in banners** — too Hindi-belt; TruePlots' Karnataka audience is English-preferred + Kannada occasional. Don't copy the tone.

2. **Sachin Tendulkar celebrity anchor** — Spinny paid $50M+ post-Series E. TruePlots pre-traction cannot afford this and doesn't need it.

3. **"Spinny MAX" luxury tier as a standalone brand** appearing in Popular Brands — Spinny built this post-Truebil acquisition. TruePlots should NOT launch a separate "TruePlots Premium" brand in v1; keep it as a tier inside one brand.

---

## What Spinny does that TruePlots has NO equivalent for (plot-market differences)

- **No "body type" for plots** — plots don't have Hatchback/Sedan categories. Our equivalent: "Urban site / Farmland / Villa-plot" and "A-Khata / BDA / BMRDA / Converted agri"
- **No "KM driven"** — plots aren't consumed. Our equivalent: "Year of approval / First sale vs resale"
- **No "Fuel type"** — plots don't burn fuel. No substitute needed
- **No color/variant analog** — plots aren't SKUs in that sense. Our equivalent micro-tags do the differentiation work
- **No "similar cars" auto-algorithm** works exactly — plots need human curation ("similar plots" should be same taluk + similar size + similar zoning, not pure ML)

---

## Operational implications

The screenshots reveal Spinny's **operational depth** — per-car micro-tags, "Reasons to buy" hand-written bullets, 1573-parts inspection reports, expert-signed reports — that text research didn't surface.

**Implication:** TruePlots' moat isn't just verification volume; it's **the human-operational layer** that makes every listing feel hand-curated:

- Hand-written per-plot micro-tag (5-15 per listing per week at scale)
- Per-plot "Reasons to buy" (3-5 bullets, unique)
- Per-plot service commitment line
- Per-plot FAQ pre-populated with plot-specific answers

This requires a verification + editorial team structure from day one, not a pure-tech team. Budget for 2-3 editorial-ops hires alongside the 3-4 verification ops hires.

This matches the Spinny model: their "200-points" is tech, but their "1573 parts / 5 experts" and micro-copy is human-operational. TruePlots should plan similarly.

---

## Single most important screenshot

**[23-ldp-report-tab-quality-scores.png](02-spinny-screenshots/23-ldp-report-tab-quality-scores.png)** — the LDP Report tab with "1573 parts evaluated by 5 automotive experts" heading + 5 category scores + "Meter not tampered / Non-flooded / Core structure intact" trust chips + "View full report" CTA.

This single screen embodies Spinny's trust architecture at its most sophisticated. Every design decision on the TruePlots LDP should reference this screen. If TruePlots' verification report visualization is less granular, less scored, less human-signed than this, we haven't done the job.

---

## Summary: 3 most important changes to earlier wireframe spec

1. **LDP is tab-based with sticky right CTA** — not long-scroll. Five tabs. Price block stays fixed.
2. **Verification has three granularity layers** — badge (120-points) / LDP detail (48 documents / 12 database checks / 4 field verifications / 3 legal experts) / score-visible (10 category scores + trust chips).
3. **Per-listing human micro-copy** is an operational moat — budget editorial-ops headcount from day one.
