# TruePlots Trust Guarantees — Spec

*Translation of Spinny's trust architecture (money-back, warranty, fixed pricing, certification) to TruePlots. Each guarantee has a feasibility flag.*

---

## 1. Money-Back / Cooling-Off Guarantee

### Spinny's version
5-day, ≤300km, no-questions-asked. Excludes damage, modifications, external repairs. Refund in 7–9 business days.

### TruePlots proposal

**Feasibility: MEDIUM — feasible with narrow scope and timing constraints.**

**Proposed: 7-Day Title-Defect Refund Window**

- **Trigger window:** 7 days from registration date (NOT from booking/token)
- **Conditions for refund eligibility:**
  - A material title defect is discovered that was present at time of TruePlots verification but not disclosed in the report
  - Buyer has not initiated mutation (khata transfer) at revenue/BBMP office
  - Buyer has not started any construction, fencing, or improvement
  - Buyer has not re-listed or re-transacted the property
- **Refund scope:**
  - TruePlots' coordination fee (₹50K–1L per buyer) — 100% refund
  - TruePlots' verification fee — 100% refund
  - TruePlots commitment to assist with seller-side refund of sale price, but NOT itself guarantee seller's refund (property law limits TruePlots' enforcement rights)
- **What this is NOT:** this is not a "you changed your mind" window. That's infeasible — stamp duty, registration, and title transfer are irreversible.

**Why 7 days (not 5):** Bangalore buyer response times are slower than Mumbai/Delhi. Most buyers review title documents in days 3-5 post-registration.

**Why title-defect-only:** TruePlots cannot refund for buyer's remorse once registration is complete. Karnataka stamp duty and registration fees are already ~7.6%+2% paid to govt and non-refundable. A broader window creates false expectations and reputational liability.

### How to communicate
- On every listing: "TruePlots 7-Day Title-Defect Protection"
- On homepage: "Buy with a 7-day title-defect refund window. If we missed something, you get your coordination and verification fees back."
- In inspection report: explicit list of what IS and ISN'T covered

---

## 2. Warranty / Title Indemnity

### Spinny's version
1-year no-questions-asked warranty on mechanical components; up to 3 years on Assured+. Claims via app.

### TruePlots proposal

**Feasibility: MEDIUM-HIGH — feasible via title indemnity insurance market.**

**Proposed: 12-Month Title Indemnity (Standard) / 60-Month Title Indemnity (Premium)**

### Structure

Partner with a title insurance provider (India market: HDFC Ergo, ICICI Lombard, Tata AIG experimenting; also specialized providers like Old Republic globally that could enter). TruePlots embeds the indemnity in the transaction.

**Standard (12-month, bundled with TruePlots Verified):**
- Covers: title defects discovered post-registration that were not disclosed in TruePlots verification report
- Cap: 50% of property value
- Exclusions: zoning/land-use changes introduced by government post-purchase, regulatory shifts (e.g., 79A/79B reversal), buyer-caused issues, construction defects
- Premium: absorbed by TruePlots (internal cost ~₹5K-10K per deal)

**Premium (60-month, paid SKU at ₹25K-75K per buyer):**
- Covers: title defects for 5 years
- Cap: 75% of property value
- Exclusions: same as standard
- Optional upsell — target 15-25% attach rate

### Why title indemnity, not warranty

A used car has a finite service life and well-understood failure modes. A plot's defects are legal, not mechanical. The right analog to Spinny's warranty is a **title indemnity**, not a traditional warranty.

### What this is NOT

- Not protection against buyer's poor construction decisions
- Not protection against market-driven price decline
- Not protection against government acquisition (which has its own compensation regime)
- Not protection against tax-law changes (IT treatment of agri income, etc.)

### Communication
- On listing: "12-month TruePlots Title Protection included"
- Premium SKU: "Extend to 5 years — TruePlots Plus"
- In verification report: clear scope + exclusions

---

## 3. Fixed Pricing / No Haggle

### Spinny's version
All prices fixed; no negotiation. Tied to 200-point inspection (inspection justifies the price). "If a price is negotiable, it's not the right price."

### TruePlots proposal

**Feasibility: HIGH — directly copyable and strategically critical.**

**Proposed: TruePlots Fixed-Pricing Assurance**

### Structure

- Every TruePlots listing has a single published price
- No buyer-side negotiation accepted on TruePlots listings
- Price is derived from:
  1. Comparable recent transactions in the locality (from Kaveri SRO data where accessible; broker network data otherwise)
  2. The 120-point verification report (a plot with 3 minor flags can't fetch the same premium as a 120-clean plot)
- **Seller sets the price; TruePlots reviews for reasonability; if seller insists on a price TruePlots considers unjustified, TruePlots declines to list**

### Critical design: tie price to verification visibly

Just as Spinny shows the 200-point report next to the price, TruePlots shows:
- **Price:** ₹45 lakh
- **Verification status:** 120/120 clean (or: 117/120 — 3 minor flags visible)
- **Comparable median (TruePlots-observed):** ₹42–48 lakh for similar plots in this locality
- **Why this price:** [1-2 lines on what justifies it — view, frontage, water yield, etc.]

This makes the price defensible and pre-empts negotiation conversations.

### Why this works for plots (despite industry norm of negotiation)

The Bangalore plot market is broker-mediated and negotiation-driven by default. TruePlots breaks this by:
1. Publishing more information than any broker will share (full verification report visible)
2. Being transparent about comparable transaction data
3. Positioning the fixed price as a PROMISE ("no one else negotiated a better deal; you're seeing the real number")

This is Spinny's clever move applied to plots.

### What to avoid

Do NOT negotiate with brokers on seller-side price reductions. This breaks the "fixed price" promise. If a plot is overpriced, TruePlots should:
- Decline to list
- OR list with a clearly disclosed "Seller premium" flag: "This plot is priced 8% above TruePlots-observed comparable median"

---

## 4. Certified Condition / TruePlots Verified Badge

### Spinny's version
"Spinny Assured" badge (+Plus, +Budget tiers). Marketing line: "Any used car can get certified. It takes perfection to be Spinny Assured."

### TruePlots proposal

**Feasibility: HIGH — copyable with brand/visual design.**

**Proposed tiering:**

| Tier | Farmland | Urban | Trust guarantees |
|---|---|---|---|
| **TruePlots Verified Premium** | 120/120 clean | 80/80 clean | 7-day title-defect refund + 12-month standard indemnity + 5-yr indemnity available as SKU |
| **TruePlots Verified** | ≤3 minor flags | ≤3 minor flags | 7-day refund + 12-month standard indemnity |
| **TruePlots Verified Conditional** | Flagged with resolution path | Flagged with resolution path | 7-day refund + 12-month indemnity scoped to cleared issues only |

### Visual design direction

- **Badge icon:** seal-like, authoritative but not corporate. Earthy green + white for farmland; muted blue + white for urban. (Differentiate from Swasya's eco-spiritual green or MagicBricks' aggressive red.)
- **Marketing line candidates:**
  - "Any plot can be listed. Only TruePlots-verified ones are ready to buy."
  - "Verified doesn't mean 'looked at.' It means 120 checks passed."
  - "Every plot. Every document. Every time."

### Where the badge appears

- Listing card (top-right corner)
- Listing detail page (prominent, next to price)
- Verification report (cover page)
- All marketing creative
- Founder's social posts when sharing individual listings

### What the badge is NOT

- Not a marketing-grade self-cert like 99acres/MagicBricks "Verified Owner"
- Not a blanket claim — it's a specific score (e.g., "120/120" or "117/120 — 3 minor flags")
- Not a substitute for buyer's own lawyer review (this disclaimer matters; publish it prominently to avoid legal exposure)

---

## 5. Buyback Guarantee

### Spinny's version
Spinny Buyback — guaranteed future resale value for 6–18 month ownership windows (premium SKU).

### TruePlots proposal

**Feasibility: LOW — conflicts with TruePlots' no-inventory facilitator model.**

**Recommendation: do NOT offer in v1.**

A buyback guarantee requires TruePlots to either:
- Hold capital to repurchase at guaranteed price (balance-sheet heavy, contradicts facilitator model), OR
- Partner with an institutional buyer willing to take plot inventory at pre-committed prices (market doesn't exist at TruePlots' scale; would need to develop)

Defer to v3+ or a "TruePlots Resale Assist" service that finds a buyer on commission (not a guarantee) for owners wanting to exit.

---

## Summary: what to ship when

| Guarantee | v1 (launch) | v1.5 (6-month) | v2 (12-month) |
|---|---|---|---|
| **Fixed pricing** | Yes — launch feature | — | — |
| **TruePlots Verified badge + tiering** | Yes | Refine tier boundaries | — |
| **7-day title-defect refund** | Yes — narrow scope | Expand communication | — |
| **12-month standard title indemnity** | Yes — partner in place by launch | — | — |
| **60-month premium title indemnity SKU** | — | Launch | Validate attach rate |
| **Buyback guarantee** | No | No | Reconsider if market matures |
