# Service Layer Mapping — Spinny → TruePlots

*Every Spinny post-purchase service mapped to a TruePlots equivalent. Flagged where translation fails.*

---

## Mapping table

| Spinny service | TruePlots equivalent | Translation | Priority |
|---|---|---|---|
| Home test drive (car to buyer's home) | **Guided site visit** (buyer to plot, with TruePlots field ops) | Inverted — buyer goes to plot, not plot to buyer. Physically impossible to bring a plot. | v1 (launch) |
| Remote test drive alternative | **Drone/ground video walkthrough** — for NRI or out-of-town buyers | Adds — no Spinny parallel. Especially useful for farmland. | v1 (launch) |
| Free doorstep evaluation (for sellers) | **On-site verification visit** (TruePlots surveyor + documents inspection at plot or seller's location) | Direct analog. TruePlots team visits to inspect. | v1 (launch) |
| RC transfer | **Registration + khata transfer** services | Direct analog. Heavier paperwork for plots (BBMP khata, mutation, Kaveri). | v1 (launch) |
| 1-year warranty (mechanical) | **12-month title indemnity** (standard, bundled) | Translated. Mechanical doesn't apply; title defects is the plot analog. | v1.5 (month 3-4) |
| Extended warranty (up to 3 years) | **60-month title indemnity** (premium SKU, paid add-on) | Translated. Partner with title insurer. | v2 (month 6-9) |
| 5-day money-back guarantee | **7-day title-defect refund window** | Translated with narrower scope — only title-defect refund, not buyer remorse. | v1 (launch) |
| Insurance integration | **Construction insurance** (for buyers building on plot) + **title insurance** (separate SKU) | Partially translated. Plots don't need vehicle insurance. | v2+ |
| Post-purchase customer service | **Post-registration support** — dedicated RM, construction guidance, renovation/fencing support | Direct analog. | v1 (launch) |
| Spinny Buyback (guaranteed resale value) | **TruePlots Resale Assist** (brokerage service, NOT guarantee) | Modified — cannot guarantee buyback without inventory capital. | v2+ |
| Insurance renewal reminder | **Khata renewal + property tax reminder** | Direct analog. | v1.5 |
| Service scheduling | **Ongoing maintenance coordination** (caretaker, fencing, plantation) for farmland | Translated to farmland-specific. | v1.5 |
| Spinny Max (luxury tier) | **TruePlots Premium** — high-touch white-glove service for ₹2Cr+ deals | Translated. | v2 (month 6+) |
| Accessories marketplace | **Construction / interior / landscaping partnerships** | Translated to plot-relevant. | v2+ |

---

## Service-layer flow per deal (farmland, whole-plot)

### Pre-registration
1. Buyer discovers listing
2. Verification report downloaded
3. Site visit booked
4. Field team arranges access with seller
5. Site visit conducted; buyer sees plot, boundaries, documents
6. Buyer decides to proceed
7. Token deposit (₹50K refundable) — plot is locked for 14 days

### Registration
8. Stamp duty paid by buyer
9. TruePlots coordinates Kaveri booking
10. Documents drafted and reviewed
11. Final legal review by partnered lawyer
12. Registration executed at sub-registrar
13. 7-day title-defect window begins

### Post-registration (30–90 days)
14. Khata transfer / mutation filed
15. Updated khata / patta issued
16. Property tax assessment transferred
17. Electricity connection transfer (if applicable)
18. Access road / easement documentation finalized
19. 12-month title indemnity begins

### Post-purchase (months 1–12)
20. Construction planning (if buyer wants to build) — architect + GC referral
21. Farmhouse permissions (if applicable) — panchayat NOC
22. Caretaker engagement (if farmland)
23. Plantation / fencing / borewell partners
24. Ongoing property tax filing reminders

---

## Service-layer flow per deal (urban, whole-plot)

Same as farmland but:
- BBMP khata transfer (not gram panchayat)
- Construction plan approval from BBMP (not panchayat)
- Home loan integration more structured (mainstream banks accept A-Khata)
- Shorter service tail (urban plots don't have borewell / plantation / caretaker needs)

---

## Service-layer flow per deal (fractional, 3-buyer)

Significantly more complex:

### Pre-registration
1. Each buyer discovers fractional-eligible listing
2. Each buyer does verification report review
3. Group of 3-4 forms (either organically or matched by TruePlots)
4. Compatibility check among buyers
5. Subdivision plan proposed (TruePlots + surveyor)
6. All buyers approve subdivision plan
7. ₹50K refundable deposit from each buyer
8. Pre-purchase agreement signed by all buyers
9. Joint site visit

### Registration (joint)
10. Joint registered sale deed executed
11. All buyers pay their share of stamp duty + registration
12. Plot jointly owned (tenants in common) temporarily

### Subdivision execution (months 1–6)
13. Partition deed drafted (per pre-purchase agreement)
14. Partition deed registered
15. Phodi (physical measurement) by surveyor
16. 11E sketch prepared
17. Submitted to Assistant Director of Land Records
18. New hissa numbers issued
19. Individual RTCs / khatas issued per buyer

### Post-subdivision (ongoing)
20. Each buyer now operates independently
21. Individual construction planning, farmhouse permissions (if applicable)
22. Individual maintenance
23. TruePlots 12-month title indemnity per buyer
24. Exit/resale coordination if needed

**Service revenue per fractional deal** amplifies ~3-4× vs whole-plot: 3-4× registration services, 3-4× construction coordination, 3-4× title indemnity. Lesson from Spinny's Assured+ tier: the premium-service tier has much better economics than the base tier.

---

## What doesn't translate at all

### Spinny's test-drive-at-home (literally)
Not applicable to plots. Buyer must visit.

### Spinny's RTO-to-RTO RC transfer (fast pipeline)
Land registration is state-specific, revenue-department-driven, and 3-6× slower than RC transfer. TruePlots cannot promise Spinny-speed registration — 4-8 week timeline is realistic.

### Spinny's fast-purchase decision cycle
Cars: test drive → decide → buy in days. Plots: site visit → diligence → decide → buy in 4-8 weeks minimum. TruePlots cannot compress this without shortchanging verification.

### Spinny's high-frequency buyer (average customer buys every 3-5 years)
Plot buyers buy once in a decade or lifetime. LTV per customer is high but transaction volume per customer is low. This changes marketing economics — TruePlots cannot depend on repeat transactions; must lean on referrals + new buyer acquisition continuously.

### Spinny's inventory purchase model
TruePlots does NOT buy inventory. Facilitator-only. Do not copy Spinny's full-stack buy/refurbish/sell model. Any internal proposal to "acquire a few farmland parcels as captive supply" contradicts the TruePlots model and must be rejected.

---

## Service tier structure (mirrors Spinny Assured / Plus / Budget)

| Service tier | Offered to | Inclusions | Pricing model |
|---|---|---|---|
| **TruePlots Verified** (default) | Every listing | 120-point verification + 7-day refund + 12-month title indemnity + site visit + registration + khata transfer | Transaction fee 1.5-2.5% + service fees per SKU |
| **TruePlots Premium** | Deals ₹75L+; opt-in | All of Verified + 60-month title indemnity + deep title search + dedicated RM + post-purchase construction package | Premium coordination fee + ongoing monthly retainer option |
| **TruePlots Fractional** | Joint-buying deals | All of Verified + buyer matching + subdivision planning + partition legal templates + individual khata execution + per-buyer title indemnity | ₹40-75K per buyer coordination fee + standard transaction fee |

---

## Build priorities

**Month 1-3 (MVP):**
- Site visit booking + field ops coordination
- Basic verification ops (120 points)
- Registration services
- Khata transfer services
- Standard title indemnity partnership (1 provider)
- Post-registration RM touchpoints

**Month 4-6 (v1.5):**
- Drone/video walkthrough
- Construction + farmhouse permission referrals
- Fractional coordination ops
- Premium title indemnity (paid SKU)
- Ongoing maintenance partner network

**Month 7-12 (v2):**
- Premium tier ("TruePlots Premium")
- B-Khata → A-Khata conversion service
- Resale assist brokerage
- Specialized construction / interior partnerships
- Agri-specific farmland services (plantation, caretaker, agri-tourism)
