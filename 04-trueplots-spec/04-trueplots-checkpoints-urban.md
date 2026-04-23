# TruePlots Urban Site — 80-Point Verification Checklist

*Bangalore-specific (BBMP/BDA/BMRDA). Structured for SOP implementation. Grouped into 9 public-facing categories.*

---

## Public framing

"Every TruePlots urban site listing clears an 80-point legal and physical verification before publication. Here are the nine categories we check. Full report included with every listing, downloadable after registered interest."

**Tier structure:**
- **TruePlots Urban Premium (A-Khata, 80/80 clean)** — default for MVP launch
- **TruePlots Urban Verified (A-Khata, ≤3 minor flags)** — minor resolvable issues disclosed
- **TruePlots Urban Conditional** — flagged with resolution pathway. **B-Khata plots EXCLUDED from MVP** per project brief (home loan constraint).

---

## Category 1 — Title Chain & Ownership (12 points)

1. Current sale deed in seller's name, registered
2. Mother deed (original allotment / first title) traced
3. Chain of title reconstructed from mother deed
4. Every intermediate sale / gift / partition / will registered
5. Seller is sole owner OR all co-owners identified and signing
6. Any POA registered and unrevoked
7. Seller Aadhaar-PAN match
8. No minor-seller issue
9. Original BDA allotment / layout release certificate (if first-sale)
10. Any inheritance-based transfer backed by legal heir certificate
11. Family tree for jointly-owned property verified
12. Seller residency status (NRI sellers need Form 15CA/CB)

## Category 2 — Khata Status (10 points)

*The load-bearing category for Bangalore urban plots.*

13. **A-Khata verified** (BBMP 2025 e-Khata system; B-Khata excluded from MVP per brief)
14. Latest khata extract obtained (within 90 days)
15. Khata matches sale deed details
16. Khata bifurcation history (if any) clean
17. No pending khata bifurcation application
18. Khata holder name matches seller
19. Property tax paid up to current assessment year
20. Property tax receipts match khata holder
21. e-Khata QR code valid and BBMP portal confirms
22. If inside BBMP ward: ward office confirmation of A-Khata

## Category 3 — Layout Approval (10 points)

*Which authority approved the layout and is that approval legally valid today.*

23. Approving authority identified: BDA / BMRDA / BBMP / BIAPPA / Panchayat
24. Approved layout plan on file
25. Release certificate / possession certificate from authority
26. Sanctioned layout plan matches physical layout on ground
27. Road widths in plan match ground reality
28. Park/civic amenity land preserved per approved plan
29. Allotment letter or sale by authority (if BDA-allotted)
30. Layout conversion order present (if agricultural converted to residential)
31. Akrama-Sakrama status NOT stayed for this survey number (post-July 2025 SC stay — only pre-existing regularized)
32. CFC / Completion Certificate for layout development (if developer-sold)

## Category 4 — CDP Zoning & Land Use (10 points)

33. CDP zone designation (residential / commercial / industrial / green)
34. Zone permits residential construction
35. No transport-buffer zone overlap (NH / SH / metro)
36. No airport-obstruction zone (Hebbal / Devanahalli / Yelahanka belt)
37. No lake/tank buffer zone overlap (NGT 30/50/75m rule)
38. No rajakaluve (storm water drain) overlap within plot
39. Master Plan 2031 (or current Karnataka plan) zoning matches
40. HAL/Defence airspace restrictions checked (if in Jakkur / Yelahanka corridor)
41. Metro Phase 2A/2B/3 alignment impact checked
42. Peripheral Ring Road / STRR alignment impact checked

## Category 5 — Encumbrance & Liens (6 points)

43. Encumbrance Certificate 30-year search from Kaveri
44. CERSAI search for registered mortgages
45. No pending bank loan / mortgage
46. No court attachment
47. No income-tax department attachment
48. No pending stamp duty / registration arrears

## Category 6 — BBMP & Utility Compliance (8 points)

49. BBMP property tax paid
50. Electricity meter / BESCOM connection status
51. BWSSB water connection eligibility confirmed
52. Storm water drain (rajakaluve) not on plot
53. Sewerage line proximity for future construction
54. Sanctioned building plan (if any existing structure)
55. OC / CC for existing structure (if any)
56. BBMP ward-level permissions for compound wall construction

## Category 7 — Physical Site Verification (10 points)

*Surveyor or field team on-ground.*

57. Site visit with georeferenced photographs
58. All four boundaries walked and GPS-tagged
59. Plot dimensions match approved layout (e.g., 30×40 actual vs claimed)
60. Frontage and depth measured and match plan
61. Corner plot / intermediate status confirmed
62. Facing (N/E/S/W) verified via compass
63. Road width in front of plot measured
64. Boundary markers / compound wall present
65. Level vs adjacent plots (depression or elevation noted)
66. Soil type for construction suitability (observational)

## Category 8 — Neighborhood & Access (8 points)

67. Main road distance and type
68. School proximity (km)
69. Hospital proximity (km)
70. Public transport (bus stop / metro station) distance
71. Shopping / market proximity
72. Surrounding land use observed (residential / commercial / mixed / industrial)
73. Walkability score (subjective, 1–5)
74. Reputed-developer proximity (brand-halo signal)

## Category 9 — Litigation & Disputes (6 points)

75. Pending court cases on property (eCourts + Kaveri search)
76. BBMP / BDA notices on property
77. Family disputes affecting ownership
78. Stay orders or injunctions
79. Neighbor boundary dispute flags
80. Encroachment claims against plot

---

## Ops implementation notes

### Automation breakdown

- **~30 points automatable** via Bhoomi (where applicable), CERSAI, eCourts, Kaveri scrape, BBMP e-Khata portal, BDA portal: Categories 2, 5, 9 partial
- **~30 points require document review**: Categories 1, 3, 6
- **~15 points require site visit**: Category 7, parts of 8
- **~5 points require BBMP / ward office visit**: Category 2 (deep verification), Category 3 (approval authenticity)

### Estimated cost per verification

- Premium (all 80): ₹6,000–9,000 internal cost
- Standard (60 core points): ₹3,500–5,000

### Report output format

Same as farmland: green/yellow/red dot per category (9 categories) + summary + downloadable full report post-registration.

---

## Comparison: farmland 120 vs urban 80

| Dimension | Farmland (120) | Urban (80) |
|---|---|---|
| Zoning complexity | High (79A/79B, PTCL, tank bed, forest) | Medium (CDP zone, rajakaluve, buffer zones) |
| Boundary verification | Harder (village land, imprecise records) | Easier (layout-approved, clear dimensions) |
| Water source checks | Critical (10 points) | Minimal (BWSSB eligibility only) |
| Access checks | Critical (10 points) | Lighter (8 points, mostly neighborhood) |
| Khata/patta | Gram panchayat / zilla | BBMP A-Khata — harder and more specific |
| Automation potential | ~37% | ~37% |

**Why urban has fewer points:** urban plots sit inside structured regulatory regimes (BBMP, BDA, approved layouts) with better-digitized records. Farmland operates in a messier revenue-department regime with more ways to fail diligence.
