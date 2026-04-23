# GLOSSARY — TruePlots terms

*Definitions of every domain-specific term used in the strategic docs. Read this before the v4 docs if you are not familiar with Indian real estate, Karnataka land law, or the TruePlots product architecture. Terms are grouped by domain and alphabetical within each group.*

*Last updated: April 21, 2026.*

---

## Regulatory and legal terms (Karnataka)

**79A / 79B (Sections 79A and 79B, Karnataka Land Reforms Act, 1961)** — Provisions that restrict who can purchase agricultural land in Karnataka. 79A limits buyers by non-agricultural income ceiling; 79B restricts purchases by non-agriculturists. Status as of April 2026: repealed by the 2020 amendment but politically contested. Restoration would reduce addressable farmland buyer pool by roughly 70%. Monitored monthly. Reference: `00-current/trueplots-project-document-v4.md` Section 5.5.

**A-Khata** — A property registration certificate issued by BBMP (Bangalore) for plots that comply with all approved plans, zoning, and building by-laws. Eligible for mainstream home loans, building plan sanction, and full property rights. TruePlots lists only A-Khata plots at urban launch.

**B-Khata** — A property registration certificate issued for plots that do NOT meet BBMP's approved-plan or by-law requirements. Construction and financing restrictions apply; most mainstream banks decline home loans on B-Khata properties. Excluded from TruePlots launch inventory because the financing constraint breaks fractional affordability at ₹40-80L ticket sizes.

**BBMP (Bruhat Bengaluru Mahanagara Palike)** — Municipal corporation for Bangalore. Governs property tax, khata, building plan approvals, and layout compliance inside Bangalore city limits.

**BDA (Bangalore Development Authority)** — Planning authority for Bangalore. Approves layouts, issues layout sanctions, and manages certain residential plot inventory (BDA layouts).

**BMRDA (Bangalore Metropolitan Region Development Authority)** — Planning authority for the Bangalore metropolitan region outside BBMP limits. Approves peripheral layouts. Many BMRDA-approved layout developers have "stuck inventory" (plots priced above what single buyers can afford) that TruePlots targets for urban-fractional deals.

**CDP (Comprehensive Development Plan)** — Zoning and land-use master plan for a region. Bangalore's CDP dictates which plots can be used for residential, commercial, agricultural, green-belt, or mixed use. A plot that violates CDP zoning is unsellable for its intended purpose.

**CERSAI (Central Registry of Securitisation Asset Reconstruction and Security Interest of India)** — Central registry that records encumbrances on immovable property across India. Part of TruePlots' 120-point verification: every listing is checked against CERSAI to confirm no outstanding liens.

**CIS (Collective Investment Scheme)** — A SEBI-regulated investment structure. Pooling customer funds to buy assets often triggers CIS regulation, which is heavy and restrictive. TruePlots' 3-buyer advance structure is specifically designed to stay OUTSIDE CIS: customer funds never pool; Delight's own capital acquires each plot; customers buy their slice directly from Delight. Growpital (farmland investment startup) was shut down by SEBI in 2024 for operating as an unregistered CIS — TruePlots is engineered around that exact failure mode.

**DC conversion (Deputy Commissioner conversion)** — The legal process to convert agricultural land to non-agricultural use in Karnataka. Required before building on agricultural land. A "DC-converted" plot has already completed this process. "Conversion pending" means the process is in progress. Not all TruePlots farmland is DC-converted — some is marketed as agricultural (for farming use) and some as DC-converted (for residential/farmhouse use).

**E-Khata** — An electronic property tax certificate issued by panchayats and some municipal bodies. Different from BBMP A-Khata. Used in panchayat areas and for agricultural/converted land in parts of Karnataka.

**Encumbrance Certificate (EC)** — A legal certificate listing all transactions registered against a property for a specified period. TruePlots pulls EC from Karnataka's EC portal as part of 120-point verification.

**Kaveri (Kaveri Online Services)** — Karnataka's online portal for property registration. Sale deeds, khata transfers, and encumbrance searches happen via Kaveri.

**KGIS (Karnataka Geographic Information System)** — State GIS portal providing cadastral maps, survey boundaries, and land classification data. Used by TruePlots for boundary verification during farmland diligence.

**PTCL Act (Prevention of Transfer of Certain Lands Act, 1978)** — Karnataka law that protects certain landholdings (typically granted to Scheduled Castes or Scheduled Tribes) from transfer to non-eligible buyers. A PTCL-tainted plot can be reclaimed by the original grantee's descendants decades after sale. One of the most common "hidden" farmland title failures — fresh buyers often do not know to check. Part of TruePlots' 120-point verification.

**RERA (Real Estate Regulatory Authority)** — Statutory body under the Real Estate (Regulation and Development) Act, 2016. Regulates real estate projects and brokers. Farmland is explicitly outside RERA. Urban plotted developments over 500 sqm or over 8 units fall under RERA. **Facilitator-vs-promoter classification** is critical for TruePlots' urban model: as facilitator, TruePlots has lower compliance burden; as promoter, full RERA-project obligations apply. Kushal is obtaining a written memo from Karnataka RERA specialist counsel before urban launch (Gate 2 at month 4).

**RTC (Record of Rights, Tenancy and Crops / "Pahani")** — Karnataka's basic land record document. Issued by the revenue department. Lists current owner, land classification, crop history, and rights. Part of farmland verification.

---

## Product and business model terms

**120-point verification** — TruePlots' proprietary farmland verification checklist. Covers ownership, title chain, zoning, encumbrance, boundary, road access, water, soil, environmental, and neighbor checks. Each checkpoint produces a pass/fail/note. Composite score out of 120 becomes the listing's verification score. Full checklist: `04-trueplots-spec/03-trueplots-120-checkpoints-farmland.md`. Urban sites have a parallel ~80-point checklist.

**3-buyer advance (3BA)** — Core fractional mechanic for farmland. A plot too large for a single buyer is listed as fractional-eligible. Three buyers commit small advances on specific slices. Once all three commit, Delight's capital acquires the whole plot. TruePlots executes subdivision (revenue department for farmland; BBMP for urban). Final sale deeds go from Delight to each buyer at the published per-slice price. Each buyer ends up with an individually-titled parcel. Urban 60×40 splits use a 2-buyer variant.

**Access-First positioning** — TruePlots' selected positioning (from three options evaluated in `03-research/06-positioning-options.md`). Hero message emphasizes access ("Own premium farmland from ₹40 lakh") with verification as infrastructure. Contrast with "Verification-First" (hero emphasizes 120-point checklist) and "Fractional-First" (hero emphasizes co-buying).

**Agent-inclusive model (v4)** — Strategic pivot from April 2026. Real estate agents are now first-class platform participants instead of being excluded (NoBroker's bet) or unorganized (99acres/MagicBricks). Delight Realty (Eshwar) brings a 100+ trusted agent network to TruePlots at launch. Every listing is jointly verified by the listing agent and TruePlots' verification team. Premium listings move to tripartite exclusive selling agreements (owner + TruePlots + agent).

**Delight Eco Farms** — The parent company. Karnataka farmland operator since 2020. 140+ acres under management across four districts. Provides plot acquisition capital, farmland subdivision expertise, sub-registrar relationships, BBMP-side experience from layout development. Equity investor in TruePlots. Kushal's brother is the operator. Sometimes abbreviated "Delight Farms" or just "Delight" in context.

**Delight Realty** — A separate Delight entity. Real estate agent network founded by Eshwar (partner). Brings 100+ trusted agents as TruePlots' launch supply engine. Distinct from Delight Eco Farms (the parent company) — they share a naming lineage but are different operating entities.

**Fractional-eligible** — A listing flag indicating the plot can be split and sold to multiple buyers (3 for farmland, 2 for urban 60×40 splits). Sellers can choose to list as fractional-eligible or whole-plot-only.

**Individually-titled** — Each buyer in a fractional deal receives a separate legal title in their own name, not a shared title or co-ownership. This is achieved via legal subdivision and individual registration. Critically differentiates TruePlots from fractional-investment startups where customers hold shares in an SPV rather than direct property title.

**Stuck-inventory thesis** — The observation that many Karnataka plots are priced 2-4x the largest buyer segment's budget, creating multi-year inventory stagnation. Farmland example: a ₹1.5Cr 7-acre plot stays unsold for 18 months when four ₹40L buyers would split it. Urban example: a ₹1.5Cr 60×40 A-Khata site stays unsold when two ₹75L buyers could split into two 30×40s with individual khatas. TruePlots solves this via fractional facilitation.

**Tripartite exclusive listing** — Commercial arrangement for premium plots. Three parties sign: plot owner, TruePlots, listing agent. In exchange for exclusive selling rights, TruePlots commits marketing resources (priority placement, dedicated content, paid promotion). Higher combined commission than non-exclusive listings. Reserved for top inventory. Commercial terms TBD pending Eshwar meeting #2.

**Trust chips** — Short, verified trust markers displayed on listings (e.g., PTCL Clear, Non-Tank-Bed, DC-Converted, Clean Title, Road Access Verified, Borewell Assured, Forest Boundary Verified). Each trust chip maps to a specific verification checkpoint with supporting evidence in the Verified Report PDF.

**Verification score (composite)** — Score out of 10.0 representing the plot's overall verification result. Calculated as the mean of 10 category scores (Ownership, Title Chain, Zoning, Encumbrance, Boundary, Road, Water, Soil, Environmental, Neighbors). 9.5+ is "excellent"; 8.5-9.4 is "good with acceptable notes"; below 7.5 typically fails publication.

**Verified Report** — The downloadable PDF issued with every TruePlots listing. Cover credits TruePlots + listing agent + verifier name. Contents include the 120-checkpoint results, category scorecard, findings and notes, supporting documents list, and 90-day validity window.

---

## Market and competitive terms

**Affinity channel** — Warm-network acquisition. The founder's 5000+ personal and professional contact network is the primary buyer source for fractional pilot deals. "Affinity CAC" tracks the cost per deal from affinity outreach. Used as a validation signal: if affinity channel cannot deliver repeatable fractional closes, product redesign is triggered before scaling to paid.

**CAC (Customer Acquisition Cost)** — Cost per closed buyer. Tracked by channel (affinity, referral, SEO, paid). TruePlots month-4 gate targets fractional-buyer CAC under ₹25K on affinity channel.

**CIS-proof** — A transaction structure specifically designed to stay outside SEBI's Collective Investment Scheme classification. TruePlots' 3-buyer-advance model is CIS-proof because customer funds never pool and Delight's balance sheet is the acquisition vehicle.

**Facilitator vs promoter (RERA)** — Two possible classifications under RERA. Facilitator = marketplace / broker role (lighter compliance). Promoter = developer / builder role (full RERA-project obligations including escrow, quarterly reporting, delivery guarantees). TruePlots intends to operate as facilitator. Counsel memo in progress to confirm classification before urban launch.

**Fast-follow threat** — A competitor with the capability, capital, and velocity to replicate TruePlots' offering within 1-2 quarters. Primary fast-follow threat identified: **NoBroker** for urban sites (venture-backed, ~$300M+ raised, 6,768 Bangalore plot listings, paid verification upsell already live). Secondary: **Farmland Bazaar** for farmland (emerging aggregator, ~90-day replication risk if they add verification).

**Moat-flip threshold** — The deal count at which TruePlots' category position becomes difficult to dislodge even if a fast-follower enters. Farmland: 30+ clean fractional deals by month 12. Urban: 20+ fractional deals by month 9 (compressed due to NoBroker velocity).

**TAM (Total Addressable Market)** — Total market size for TruePlots' target segments. Key sensitivity: a 79A/B restoration in Karnataka collapses farmland TAM by roughly 70%.

---

## Product architecture terms

**LDP (Listing Detail Page)** — The detail page for a single plot. Contains plot gallery, key facts, 5 tabs (Overview, Verification Report, Protection, Specs & Features, Financing), reserve CTA, similar plots strip. URL format: `/plot/{district}-{village}-{survey_no}` lowercased, hyphen-separated.

**Reserve flow** — The 4-step buyer commitment flow. Step 1: summary. Step 2: buyer details + OTP. Step 3: ₹5,000 payment. Step 4: confirmation. URL-driven state via `?rid={uuid}&step={n}`. Drafts persist in the `reservations` table so refreshes don't lose progress. Reserve is 100% refundable for 5 days; plot is held off-market during that window.

**Session 1/2/3/4/5** — The 5-session build plan for the application code. Session 1 shipped April 2026: foundation (Next.js, Supabase schema, auth, design system). Session 2 shipped: UI integration across 6 pages + agent attribution + seed data. Session 3 planned: admin CRUD. Session 4 planned: real integrations (WhatsApp OTP, HubSpot, Razorpay, PDF generator). Session 5 planned: SEO content + polish + production deploy.

---

## Domain abbreviations used in docs

| Abbreviation | Full term |
|---|---|
| BBMP | Bruhat Bengaluru Mahanagara Palike |
| BDA | Bangalore Development Authority |
| BMRDA | Bangalore Metropolitan Region Development Authority |
| CAC | Customer Acquisition Cost |
| CDP | Comprehensive Development Plan |
| CERSAI | Central Registry of Securitisation Asset Reconstruction and Security Interest of India |
| CIS | Collective Investment Scheme |
| EC | Encumbrance Certificate |
| GTM | Go-to-Market |
| HNI | High Net-worth Individual |
| KGIS | Karnataka Geographic Information System |
| KPI | Key Performance Indicator |
| LDP | Listing Detail Page |
| LTC | Listing-to-Close ratio (agent performance metric) |
| MSG91 / Twilio / Gupshup / Aisensy | WhatsApp Business API providers |
| NBFC | Non-Banking Financial Company |
| NoBroker | Venture-backed Indian real estate marketplace, primary urban-site fast-follow threat |
| PTCL | Prevention of Transfer of Certain Lands Act, 1978 |
| RERA | Real Estate Regulatory Authority |
| RTC | Record of Rights, Tenancy and Crops (also "Pahani") |
| SEBI | Securities and Exchange Board of India |
| SEO | Search Engine Optimization |
| SLA | Service Level Agreement |
| SPV | Special Purpose Vehicle |
| TAM | Total Addressable Market |
| TBD | To Be Determined |
| TM | Trademark |
| USP | Unique Selling Proposition |
| YC | Y Combinator (not affiliated with TruePlots) |

---

*Document version: 1.0 — April 21, 2026. Update when new domain-specific terms enter the strategic docs.*
