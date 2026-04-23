# TruePlots Loan Integration Spec

*Based on Spinny's financing architecture (Spinny Capital brand + dynamic partner matching + soft pre-approval + inline EMI). Adapted for the distinctive realities of plot financing in India.*

---

## Reality check: plot financing is harder than car financing

| Factor | Car loan (Spinny) | Plot loan (TruePlots) |
|---|---|---|
| Collateral | Vehicle (registered) | Land title (if A-Khata clear) |
| Typical LTV | Up to 100% | 60–75% standard for plots; lower for agri |
| Tenure | 1–7 years | 10–15 years typical for plot loan |
| Interest rate | 11–20% | 8.5–11% for plot loan (cheaper than used car) |
| Document depth | Moderate (KYC + income + DL) | Heavy (KYC + income + full title chain + encumbrance) |
| Pre-approval speed | Minutes | Hours to days |
| Sanction-to-disbursal | Same day feasible | 2–6 weeks typical |
| B-Khata plots | N/A | **Disqualified from mainstream banks** (critical constraint) |
| Fractional deals | N/A | Each co-buyer needs own loan — 3× processing |

**Implication:** TruePlots cannot promise Spinny-speed loan processing. What TruePlots CAN do is Spinny-quality loan UX with realistic timelines disclosed upfront.

---

## Partner bank strategy

### Tier 1 — Premium plot-loan partners (launch priority)

| Bank | Why | Contact strategy |
|---|---|---|
| **HDFC Bank** | Market leader, strong home/plot loan product, best plot-loan UX | Build via enterprise partnership team; leverage Spinny Capital playbook |
| **ICICI Bank** | Strong plot loan product, ~11.25% starting; recently digital-forward | Partner pitch via retail banking |
| **Axis Bank** | Competitive rates on plot; aggressive digital partnerships | Pitch via digital partnership channel |
| **Kotak Mahindra** | Plot loan specialists; historical partnerships with proptech | Pitch via retail partnerships |

### Tier 2 — Farmland-specialist financing (month 4+)

Farmland buyers face additional complications because plot loans typically require converted/layout-approved land, not pure agricultural. Options:

| Channel | Why | Constraint |
|---|---|---|
| **NABARD-refinanced channels** | Available for agricultural purchase with agricultural-income buyer | Only if buyer is agriculturist |
| **Karnataka Gramin Bank** | Agri-focused regional rural bank | Smaller ticket sizes |
| **State Bank of India (Agri-Gold)** | Accepts agricultural land as collateral | Documentation-heavy |
| **Canara Bank (Farmland loan)** | Karnataka-based, agri-friendly | Limited digital journey |

### Tier 3 — NBFCs for edge cases (month 6+)

For non-salaried buyers, fractional deals with unconventional income profiles, or complex title situations. Possible partners: Bajaj Finance, Tata Capital, Chola, Muthoot Homefin. Higher rates (12–14%), faster decisions, more flexible income verification.

### Unified brand: "TruePlots Capital"

Mirror Spinny Capital. Single front-door; specific partner matched per buyer profile. Protects against buyer confusion ("why is my loan from Bank X when I started with Bank Y?") and gives TruePlots the lever to renegotiate partner rates over time.

---

## Buyer-facing loan flow

### Step 0 — Homepage anchor

- "EMI starts from ₹X/month" shown on every listing card (price anchoring)
- Homepage CTA: "Check loan eligibility in 3 minutes — no credit score impact"

### Step 1 — Soft pre-approval (before plot shortlist)

**Inputs (short form — under 2 minutes):**
- Name, mobile, email, city
- Employment type (salaried / self-employed / business / agricultural)
- Gross monthly income bracket
- Existing EMI bracket (none / <30% income / 30–50% / >50%)
- Age
- Preferred loan amount bracket
- Preferred tenure

**Output:**
- Soft eligibility verdict (₹X–Y lakh, indicative rate)
- Eligibility-by-bank (if multiple partners say yes, show top 2)
- Saved to buyer profile — persists across listing browsing

**What this does NOT do:**
- Does not impact credit score (soft pull only)
- Does not lock rate
- Does not guarantee sanction

### Step 2 — Listing browse with personalized EMI

Once pre-approved, every listing card shows:
- "Your estimated EMI: ₹X/month (at your pre-approved rate)"
- "Eligibility: 78% of this plot's price via HDFC Home Loan"

This personalization is powerful. Spinny does similar. Dramatic conversion uplift.

### Step 3 — Full application on plot shortlist

When buyer selects a plot and proceeds to "Book Site Visit" or "Reserve Plot":

**Documents requested (upload flow):**
- Aadhaar + PAN
- Address proof (utility bill or registered rental / own-home)
- Income proof: salaried (last 3 months bank statement + payslips + Form 16 / Employment letter); self-employed (last 2 years ITR + bank statement + business registration); agricultural (land ownership + last 2 years agri-income declaration + bank statement)
- Existing loan statements (if any)
- KYC for co-applicants (if fractional — each co-buyer submits)

**Parallel to documents:** TruePlots' verification report is shared with the lender (speeds bank-side due diligence)

### Step 4 — Sanction and registration

- Bank sanctions loan within 5–14 days (realistic for Bangalore plots)
- Buyer pays stamp duty + registration + TruePlots coordination fee from own funds
- Bank disburses loan directly to seller at registration
- TruePlots coordinates the 3-way handshake (bank + buyer + seller + TruePlots)

### Step 5 — Post-registration

- EMI schedule visible in TruePlots buyer account
- Link to bank's own loan management
- Mutation / khata transfer coordination with bank hypothecation

---

## EMI calculator design

**Inputs:**
- Loan amount (pre-filled from plot price × LTV%)
- Interest rate (pre-filled from soft pre-approval)
- Tenure (slider: 5 / 10 / 15 / 20 years)
- Down payment amount (pre-filled as plot price minus loan amount)

**Outputs:**
- Monthly EMI
- Total interest paid over tenure
- Total amount payable
- Chart: EMI breakup (principal vs interest) over time
- "Affordability:" shown as % of declared monthly income (cap at 50%)

**Placement:**
- Standalone page: /loan-emi-calculator
- Inline on every listing detail page (sidebar on desktop; sticky accordion on mobile)
- Fractional listings show: "Your share EMI: ₹X | Total plot EMI: ₹Y"

---

## Critical constraint: B-Khata exclusion

**The binding constraint.** B-Khata plots cannot get mainstream home loans from HDFC, ICICI, Axis, Kotak, SBI. This is a hard-and-fast rule.

**Implications for TruePlots:**
1. **MVP inventory restricted to A-Khata only** (per project brief Section 5.X.6)
2. Loan partner conversations must cover: "what's your policy on B-Khata plots?" If a partner says "we don't do B-Khata at all," that partner works for TruePlots' MVP scope.
3. Longer-term: TruePlots can build a **B-Khata → A-Khata conversion service** (charge ₹50K-1.5L per conversion) as a separate SKU that makes stuck B-Khata inventory financeable. This is a supply-side unlock no incumbent offers.
4. Farmland has a parallel constraint: unconverted agricultural land can't get mainstream plot loans either. Only agriculturist-income buyers can get NABARD-channel agri loans. This is why fractional farmland at ₹40L ticket is hard — the buyer segment least likely to qualify for agri-loans is exactly the segment TruePlots targets.

**Important implication for fractional deals:**
- Each co-buyer's financing is processed SEPARATELY — 3 buyers = 3 loan applications
- This is 3× the processing time and bank-side overhead
- TruePlots' coordination fee should reflect this (brief suggests ₹25–75K per buyer; this analysis recommends ₹40–75K)

---

## Pre-approval UX details

Mirror Spinny's "check in minutes without affecting credit score" language precisely. This is the single highest-conversion pattern in the buyer journey.

**Copy for the CTA button:**
- "Check your loan eligibility — 3 minutes, no credit score impact"

**Copy for the eligibility result page:**
- "You're pre-approved for up to ₹X lakh at Y% starting rate"
- "Based on HDFC Home Loan guidelines. Rate is indicative; final sanction depends on full documentation."
- Secondary CTA: "Browse plots you can afford"

This channels the buyer from financial curiosity into inventory browsing — exactly Spinny's funnel.

---

## Build priorities for month 1–6

**Month 1–2:**
- Launch EMI calculator (standalone + listing inline)
- Soft pre-approval form with eligibility estimator (initially: single partner — HDFC or Axis whoever closes first)

**Month 3–4:**
- Full document upload + application flow
- TruePlots verification report auto-shared with lender (speeds bank due diligence — major conversion lift)

**Month 5–6:**
- Multi-bank partner matching (dynamic best-deal)
- Personalized EMI on listing cards (post pre-approval)
- Farmland agri-loan pathway (NABARD-channel partner)

**Month 7+:**
- B-Khata → A-Khata conversion service (separate SKU)
- Sachet / alternative credit products for fractional co-buyers who don't qualify for mainstream
