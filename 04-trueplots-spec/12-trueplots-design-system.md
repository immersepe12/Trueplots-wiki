# TruePlots Design System v1

*Consolidated design spec derived from screenshot analysis. Single source of truth for designers and frontend engineers. Supersedes/complements [file 07 page specs](07-trueplots-page-specs.md) and [file 05 trust guarantees](05-trueplots-trust-guarantees.md).*

**Date:** 2026-04-19. Based on 30 Spinny screenshots + farmland/urban research.

---

## 0. Design principles

1. **Trust is visible, not stated.** Every trust claim must be backed by a specific, scored, sourced artifact on-screen. "Verified" alone is marketing fluff. "120/120 clean · PTCL clear · 79A/B compliant" is trust.
2. **Photo-first, copy-second.** Dominant photography > decorative illustration > long copy.
3. **Price and verification live together.** Every price on-screen has a verification score next to it, with a "Why this price?" explainer one click away.
4. **Trust copy lives on buttons, not next to them.** "BOOK SITE VISIT · 100% refundable" is one element.
5. **Every listing feels hand-curated.** Per-plot micro-tag + "Reasons to buy" + service commitment — operational moat, not tech moat.
6. **Low-friction holds, honest countdowns.** ₹5,000 reserve · "ends in 3 days" — not ₹50K hold and aggressive pressure.

---

## 1. Brand identity

### Tone
Confident, direct, grown-up. The register of a trusted family lawyer or a good financial advisor. Avoid:
- Eco-spiritual register (the Swasya/Sanctity Ferme lane) — no "sacred land," no "commune with nature"
- Transactional budget-portal register — no "best deals guaranteed"
- Hindi-belt colloquialisms — Spinny uses "god promise" in Hindi-belt campaigns; TruePlots' South Indian audience is English-preferred + Kannada-occasional

### Voice examples

✅ "Every plot. Every document. Every time."
✅ "120 checks passed. Zero surprises at registration."
✅ "Own it truly — with individual title, even when you buy together."

❌ "Discover your dream farmland at unbelievable prices!"
❌ "Live the life you deserve with sacred earth."
❌ "Guaranteed Love" (Spinny's line — wrong register for plot anxiety)

### Color system

| Role | Hex | Usage |
|---|---|---|
| **Primary — Earthy Green** | `#3D6B4A` | TruePlots Verified badge, primary CTAs, brand marks |
| **Primary action — Terracotta Red** | `#C44F37` | Reserve Plot / high-intent CTAs only |
| **Secondary — Warm Clay** | `#C4916E` | Accents, category tags, trust chips |
| **Deep text** | `#1A1F1B` | Body copy, headlines |
| **Muted text** | `#5F6B62` | Meta text, captions, specifications |
| **Background neutral** | `#FAF7F2` | Page background (warm off-white) |
| **Surface white** | `#FFFFFF` | Cards, tab panels |
| **Trust chip green** | `#E8F0EA` / text `#2D5238` | "PTCL clear" style chips |
| **Warning amber** | `#D4941F` | Minor flags on verification |
| **Critical red** | `#8B2323` | Unresolved flags (rare — should be "rejected from listing" most of the time) |

Do not use:
- Pink/red gradient pairings (Spinny/Swiggy territory)
- Aggressive corporate blue (MagicBricks/99acres territory)
- Eco-green saturated (Swasya territory)

### Typography

- **Headline:** Modern sans-serif with slight personality. Candidates: Söhne, Aeonik, Inter (if budget tight)
- **Body:** Readable sans-serif. Inter or similar
- **Numbers/scores:** Tabular-figure variant for scorecards ("9.6", "120/120")

Type scale:
- H1 hero: 72-96px desktop / 48-60px mobile
- H2 section: 40-48px / 32-36px
- H3 subsection: 28-32px / 24-28px
- Body large: 18-20px
- Body: 16px
- Caption: 14px
- Micro: 12px

### Photography direction

- Real plots, real conditions — dust, rough roads, borewell pipes visible in farmland; construction-in-progress plots visible in urban
- NO stock farmhouse imagery
- NO aerial helicopter-perspective lifestyle shots of families walking through golden wheat
- Do include drone overheads of actual TruePlots inventory, ground-level boundary walking videos, document-on-desk compositions

---

## 2. Component library — the core components

### 2.1 Verification Badge

Three tiers, consistent visual system.

```
┌─────────────────────────┐
│  🔒 TruePlots Verified  │  ← Primary green on all "Verified" tier
│       120/120 Clean     │
└─────────────────────────┘
```

| Tier | Label | When applied |
|---|---|---|
| **Premium** | "TruePlots Verified · Premium" | 120/120 clean farmland or 80/80 clean urban, zero flags |
| **Verified** | "TruePlots Verified" | ≤3 minor resolved flags |
| **Conditional** | "TruePlots Verified · Conditional" | Flagged with resolution pathway disclosed (amber trim, not red) |

Placement: bottom-left of listing card photos (subtle); next to price on LDP (prominent).

### 2.2 Trust Chips

Green-check chips for verified attributes. Row layout above the verification scorecard on LDP.

```
[✓ PTCL clear]  [✓ Non-encumbered]  [✓ 79A/B compliant]  [✓ KGIS boundary match]  [✓ Title chain intact]
```

Max 5 chips per row. Tap/hover shows 1-sentence explanation.

### 2.3 Scorecard (the centerpiece of the Verification Report tab)

```
120-point verification
48 documents reviewed · 12 database cross-checks · 4 field verifications · 3 legal experts

┌──────────────────────────────────────────────────────────────────┐
│  Category                            Score    Label              │
├──────────────────────────────────────────────────────────────────┤
│  Ownership & Title Chain             10/10    Clean              │
│  Revenue Records & Mutation          9.8/10   Clean              │
│  Zoning & Land Use                   9.5/10   Clean              │
│  Boundary & Survey                   10/10    Clean              │
│  Encumbrance & Liens                 10/10    Clean              │
│  Road Access & Approach              9.0/10   Clean              │
│  Water Source (farmland)             8.5/10   Good               │
│  Litigation & Disputes               10/10    Clean              │
│  Physical Site Verification          9.5/10   Clean              │
│  Tax & Compliance                    10/10    Clean              │
└──────────────────────────────────────────────────────────────────┘

[View full report]   Next recheck: at registration (open milestone)
```

Mirrors Spinny screenshot 23. Numerical scores + text label per category. "View full report" is open — not email-gated.

### 2.4 Price Block (sticky right-side on LDP)

```
┌─────────────────────────────────────┐
│  1,200 sqft · A-Khata · BDA         │
│  📍 Kanakapura Rd, Bangalore         │
│                                     │
│  ⭐ Low PTCL risk · Clean chain      │ ← hand-written micro-tag
│                                     │
│  ₹45.5 Lakh                         │ ← H2 size
│  + Registration & stamp duty        │ ← small caption
│  or ₹32,000/m · Calculate EMI →     │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  BOOK SITE VISIT              │  │ ← Primary green
│  │  100% refundable              │  │ ← trust copy ON button
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  RESERVE PLOT ₹5,000          │  │ ← Terracotta red
│  │  refundable · hold 3 days     │  │ ← trust copy ON button
│  └───────────────────────────────┘  │
│                                     │
│  Share:  📱  𝕏  f  ✉                │ ← WhatsApp-first
└─────────────────────────────────────┘
```

Sticky on scroll. Stays visible as user moves through the 5 tabs.

### 2.5 Listing Card

Desktop grid card:

```
┌──────────────────────────────────────┐
│ [Photo — drone aerial or ground]      │
│                               [badge] │
├──────────────────────────────────────┤
│ ₹45.5 Lakh    EMI from ₹32K/m        │
│ 30×40 BDA plot · Kanakapura Rd       │
│ 1,200 sqft · A-Khata · N-facing      │
│ ⭐ Corner plot · Morning sun          │  ← hand-written
│ 🔒 TruePlots Verified 80/80          │
│ 🤝 Join 2 others — from ₹15L share   │  ← if fractional-eligible
└──────────────────────────────────────┘
```

Per-card micro-tag (the ⭐ line) is the editorial-ops-authored distinguishing line. Budget editorial-ops headcount for this.

### 2.6 Reserve/Checkout UI

```
 ✓ Plot selected  —  ● Site visit preferences  —  ○ Payment

Reserve this plot for ₹5,000
and find out if it's your perfect fit

┌──────────────────────────┐   ┌──────────────────────────────┐
│ 🏦 Interested in plot    │   │ [photo] 30×40 BDA plot       │
│    loan?          [  ]   │   │ Kanakapura Rd                 │
│ Get financed at competi- │   │ ₹45.5 Lakh  EMI ₹32K/m       │
│ tive rates. Learn more → │   │                               │
└──────────────────────────┘   │ ✓ Booking amount    ₹5,000   │
                               │   Reservation ends in 3 days  │
┌──────────────────────────┐   │                               │
│ Where would you prefer   │   │ Price breakdown               │
│ to visit?                │   │ Plot price          ₹45,50,000│
│                          │   │ Registration facilitation +  │
│ [AT PLOT LOCATION]       │   │   ₹15,000                     │
│ [AT TRUEPLOTS OFFICE]    │   │ Verification (paid)  Included │
└──────────────────────────┘   │ ─────────────────────────────│
                               │ Final amount       ₹45,65,000 │
                               │                               │
                               │   100% refundable             │
                               └──────────────────────────────┘
```

Direct translation of Spinny's cart UI (screenshot 30).

### 2.7 Four-pillar promise cards (homepage + repeated on listings page mid-scroll)

```
┌──────────────┬──────────────┬──────────────┬──────────────┐
│ [icon+photo] │ [icon+photo] │ [icon+photo] │ [icon+photo] │
│              │              │              │              │
│ 120-Point    │ 12-Month     │ 7-Day        │ Fixed        │
│ Verification │ Title        │ Refund       │ Price        │
│              │ Protection   │ Window       │ Assurance    │
│              │              │              │              │
│ Every plot.  │ Defect       │ Title-defect │ Price meets  │
│ Every doc.   │ indemnity    │ refund post- │ verification │
│ Every time.  │ up to 50%    │ registration │ — no haggle  │
└──────────────┴──────────────┴──────────────┴──────────────┘

            [ Browse verified plots ]  ← center CTA
```

### 2.8 Stats banner (deploy post-50 deals)

```
Insights that drive us

┌──────────┬──────────┬──────────┬──────────┐
│  [icon]  │  [icon]  │  [icon]  │  [icon]  │
│  4.8/5   │  35%     │  >70%    │  Zero    │
│          │          │          │          │
│ Average  │ Buyers   │ Close    │ Title-   │
│ rating   │ via      │ post     │ defect   │
│          │ referral │ site     │ claims   │
│          │          │ visit    │          │
└──────────┴──────────┴──────────┴──────────┘
```

Only deploy real numbers. Don't fake proof.

---

## 3. Content patterns (what editorial ops produces)

These are the operational moats. Per-listing, every time. Budget 2-3 editorial-ops headcount alongside the 3-4 verification-ops.

### 3.1 Per-plot micro-tag (on listing card)
3-5 words. Unique per plot. Examples:
- "Corner plot · Morning sun"
- "5 min from metro station"
- "Low PTCL risk · Clean chain"
- "Lake frontage · Bore water"
- "Converted · Layout approved"
- "Mango grove · Caretaker in place"

### 3.2 "Reasons to buy" (on LDP Overview tab)
3-5 bullets. Unique per plot. Examples:
- "Premium corner plot — better sunlight and ventilation"
- "Pre-approved for 75% plot loan with HDFC"
- "5-minute drive from upcoming Kanakapura metro"
- "Mother deed from 1987, unbroken chain for 40 years"
- "Existing borewell with 2,000 GPH verified yield"

### 3.3 Service commitment line (on LDP)
One sentence, concrete, time-bound. Examples:
- "Khata transfer guaranteed within 45 days post registration"
- "Verification report re-validated 6 months pre-registration"
- "Next legal recheck at registration milestone"

### 3.4 Plot-specific FAQ (on LDP)
4-6 pre-populated Q&A. Editorial ops writes these for each listing based on plot characteristics. Examples:
- "Can I build a 2,400 sqft farmhouse on this plot?" → "Yes — the plot is 1 acre converted to residential with panchayat NOC obtainable for up to 3,000 sqft farmhouse construction."
- "Is there a water source for construction?" → "The plot has an existing borewell verified at 2,000 GPH. BWSSB water connection is available 500m away."

---

## 4. Page templates — see file 07

Complete wireframes for:
- Homepage ([§1 of file 07](07-trueplots-page-specs.md))
- Listings / search ([§2](07-trueplots-page-specs.md))
- Listing detail page with tabs ([§3](07-trueplots-page-specs.md))
- Verification methodology ([§4](07-trueplots-page-specs.md))
- Fractional buyer flow ([§5](07-trueplots-page-specs.md))
- Financing ([§6](07-trueplots-page-specs.md))
- Services ([§7](07-trueplots-page-specs.md))
- Cart / Reserve (added in Section 2.6 above)

File 07 is now updated with screenshot-validated specs.

---

## 5. What not to do

See [`09-what-does-not-translate.md`](09-what-does-not-translate.md) for the full list. Design-specific anti-patterns:

1. ❌ Long-scroll LDP — use tabs
2. ❌ Trust claim NEXT TO CTA — put it ON the CTA button
3. ❌ High reserve amounts (₹50K+) — use ₹5,000 to match low-friction psychology
4. ❌ Generic "Verified" badge without score — always show numerical score
5. ❌ Pass/fail dots on verification categories — use /10 numerical scores
6. ❌ Stock farmhouse photography — use real plot conditions
7. ❌ Hindi-belt colloquialisms ("god promise") — keep South Indian register
8. ❌ Aggressive countdown timers — honest "ends in 3 days" is enough
9. ❌ Celebrity endorsement pre-traction — wait until post-500 deals
10. ❌ Price-as-hook hero ("best prices guaranteed") — lead with trust, not price
11. ❌ Sidebar CTAs for loan/fractional — embed AS grid items in listings
12. ❌ Gated "full verification report" (email required) — keep open on page
13. ❌ Single CTA in hero — use single primary + single secondary max
14. ❌ Auto-generated "similar plots" via pure ML — human-curated same-taluk + same-zoning
15. ❌ Skippable editorial-ops function — budget the headcount; this is the moat

---

## 6. Component build order (engineering)

For the month 1-3 MVP:

**Week 1-2: atoms**
- Verification Badge (3 tiers)
- Trust Chip component
- Per-plot micro-tag component
- CTA button variants (with trust copy slot)

**Week 3-4: molecules**
- Listing Card (with all the card spec)
- Price Block (sticky behavior on desktop, floating on mobile)
- Scorecard (10 categories, numerical, with labels)
- Four-pillar promise cards

**Week 5-6: organisms**
- Homepage hero with Buy/Sell duality
- Listings grid with inline cards + service banners + lead capture
- Tab component for LDP

**Week 7-8: pages**
- Homepage
- Listings page
- Listing detail page with 5 tabs
- Reserve/Checkout 3-step flow

**Week 9-12: finishing**
- Mobile responsive polish
- Sticky behaviors (price block, mobile floating CTA, secondary nav)
- Empty states, loading skeletons
- Content management for per-plot micro-tags, reasons-to-buy, plot-specific FAQ (editorial-ops CMS)

---

## 7. Operational prerequisite — editorial ops team

Non-negotiable: **the design system assumes 2-3 editorial-ops hires from day one**, not month 6. The design depends on per-listing human content that cannot be AI-generated at adequate quality:
- Per-plot micro-tags
- "Reasons to buy" bullets
- Service commitment lines
- Plot-specific FAQ

Without this team, every listing looks generic and the trust-through-curation advantage collapses. If the hiring plan doesn't include editorial ops, the design system needs to be re-specced with generic content defaults — but that means giving up the moat.

**This is the single biggest operational implication of adopting the Spinny pattern.**

---

## Version history

- **v1 (2026-04-19):** First consolidated design system, post-screenshot analysis. Based on 30 Spinny screenshots + earlier text research.
