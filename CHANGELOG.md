# CHANGELOG — TruePlots strategic docs

*Version history of the source-of-truth strategic documents. Read this to understand why current decisions look the way they do and what was considered but rejected. Each entry records the trigger for the version bump, what changed, and what carried over unchanged.*

*Format: reverse chronological (newest first).*

---

## v4.0 — April 21, 2026 — Agent-inclusive model

**Trigger:** Meeting with Eshwar (founder, Delight Realty). Decision to bring Delight Realty's 100+ trusted real estate agent network onto TruePlots as a first-class part of the marketplace architecture.

**What changed:**

- Platform model expanded from verified-plots-only to verified-plots + verified-agents. Every listing is jointly verified by the listing agent and TruePlots.
- Supply-side thesis upgraded: launch-day listings target raised from 50+ founder-sourced to 100-200 agent-sourced via Delight Realty's network.
- Competitive positioning sharpened around "organize the existing system, don't fight it" — TruePlots sits between horizontal portals (99acres, MagicBricks) that have volume without trust, and NoBroker which removes agents entirely. Different buyer fit.
- Moat composition updated: Delight's 100-agent network added as a supply-side defensibility layer that competitors cannot replicate by writing checks (six years of local trust-building is the input).
- Business model restructured: 1% agent commission on their own listings (baseline); premium plots use tripartite exclusive selling agreements with higher combined margin. Exact splits TBD pending Eshwar meeting #2.
- New hire: Agent Success Lead added at month 2 (between Land Ops Lead and SEO/Content Lead). Non-optional given 20+ agent onboarding target by month 2.
- Budget revised from ₹68-103L (v3) to ₹79-117L to cover the new Agent Success Lead and expanded legal work.
- Launch-day UI scope expanded to include "Listed by [Agent Name] · Verified by TruePlots" attribution on listing cards and LDPs. Full agent-facing surfaces (landing page, dashboard, profile pages, scorecard) are month 3 work.
- Risks section: added partnership risk (Eshwar terms pending) and agent quality risk (title-defect liability on agent-listed plots).

**What carried over unchanged:**

- Product model (3-buyer advance fractional, individual titling, Delight's capital acquires)
- 120-point verification checklist (farmland) and ~80-point urban checklist
- Design system and brand identity (Forest Green, Harvest Gold, Paper White; Fraunces + Inter + JetBrains Mono)
- Trademark status (Class 36 filed) and domain secured
- Three-gate month-4 urban decision structure
- A-Khata-only rule for urban launch; B-Khata plots excluded
- 79A/B monitoring and TAM-collapse risk plan
- CIS-proof structure (SEBI)
- Defensibility windows (farmland 12-18 months, urban 9-12 months)
- Moat-flip thresholds (30+ farmland fractional by month 12, 20+ urban deals with 10+ fractional by month 9)

**Affected files:**

- `00-current/trueplots-project-document-v4.md` (new)
- `00-current/trueplots-gtm-plan-v4.md` (new)
- `00-current/trueplots-project-pitch-v4.md` (new)
- `05-deprecated/trueplots-project-document-v3.md` (moved from current)
- `05-deprecated/trueplots-gtm-plan-v3.md` (moved from current)
- `05-deprecated/trueplots-project-pitch-v3.md` (moved from current)
- `README.md` (updated to point at v4)
- `AGENTS.md` (new, for AI agent onboarding to this repo)
- `GLOSSARY.md` (new, consolidated term definitions)

**Open decisions after v4:**

- Exact agent commission splits (standard vs exclusive)
- Buyer-side vs seller-side commission mechanics
- Cross-agent referral economics
- Bad-agent removal thresholds and process
- Exclusive listing agreement template and marketing SLA
- Liability structure for later-discovered title defects on agent-listed plots

All are marked "TBD pending Eshwar meeting #2" in the v4 docs.

---

## v3.0 — April 2026 (pre-v4) — Urban-sites scope expansion

**Trigger:** Urban sites top-up analysis identified fractional opportunity (2-buyer 60×40 → 30×40 splits in Bangalore corridors) and surfaced NoBroker as primary fast-follow threat with a 9-12 month window.

**What changed from v2:**

- NoBroker upgraded to primary fast-follow threat on urban sites (9-12 month window, not 18).
- A-Khata-only urban launch rule introduced (B-Khata plots excluded due to financing constraints breaking fractional affordability).
- Month-4 decision restructured from single gate to three gates (farmland pilot validation + RERA counsel memo + urban supply density).
- RERA facilitator-vs-promoter classification added as top-5 risk for urban vertical.
- BMRDA layout developers reframed as supply partners, not competitors.
- Urban Site Ops Lead hire pulled forward from month 7 to month 4-5.
- Urban fractional deal target compressed: 20+ urban deals with 10+ fractional by month 9 (not month 12).

**What carried over unchanged:**

- Farmland as hero vertical
- 3-buyer advance fractional mechanics
- Delight Eco Farms as parent and equity partner
- 120-point verification
- Access-First positioning
- Trademark and domain status

---

## v2.0 — early 2026 — Scope refinement and competitive research integration

**Trigger:** Completion of farmland competitive analysis (`03-research/` files numeric-prefixed without "urban") and Spinny product research (`03-research/01-spinny-research-notes.md`, `11-spinny-ui-ux-analysis.md`).

**What changed from v1:**

- Competitive positioning articulated (three options evaluated; Access-First selected).
- Unit economics benchmarked against managed farmland developers (Swasya, Sanctity Ferme, Mytan, Hasiru, Sanjeevani, Triguna) and farmland aggregators (Farmland Bazaar, Saptashwa).
- Product UX architecture adopted from Spinny (verification scorecard, trust chips, Verified Report PDF, three-layer verification framing) — noting explicitly that the business model is NOT Spinny's buy-and-hold (`09-what-does-not-translate.md`).
- 120-point verification checklist finalized in collaboration with Delight legal team.
- Services layer mapped in detail (`08-trueplots-service-layer-map.md`).

**What carried over:**

- Farmland-first scope
- 3-buyer advance as core fractional mechanic
- Delight partnership terms

---

## v1.0 — late 2025 — Initial scope

**Trigger:** Founder decision to solve the problem after two failed personal farmland purchases in Karnataka over 4 months.

**Original scope:**

- Karnataka farmland only
- Verified-listings marketplace
- 3-buyer advance for fractional pilots
- Delight Eco Farms as operational parent

**Why this changed:** v1 was pre-product. v2 added rigor through research. v3 added urban as second vertical. v4 added agents as first-class platform participants.

---

## Upcoming revisions

The next version will be triggered by one of:

- **Eshwar meeting #2 outcome** — commission splits, liability terms, exclusivity mechanics finalized. Triggers v4.1 (point revision) or v5 if substantive restructure.
- **Month 4 three-gate decision** — urban launch go/no-go. If all three gates pass, triggers a GTM v4.1. If any fails, triggers a strategic re-plan.
- **RERA specialist counsel memo** — if facilitator classification is confirmed, minor update; if refused, major restructuring needed.
- **First fractional deal close outcome** — if successful, minor case-study addition; if subdivision or title issue surfaces, reopens Section 11 (Risks).
- **79A/B restoration in Karnataka** — would trigger immediate TAM reassessment and acceleration of Tamil Nadu farmland and urban sites.
- **Competitive move** — NoBroker launching verification + fractional, or Farmland Bazaar adding verification, triggers defensibility review.
- **New vertical or geography** — addition beyond farmland + urban Karnataka would be v5.

---

## How to read version numbers

- **Major (v4, v5):** New vertical, new geography, new partnership model, change in core positioning, change in business model.
- **Minor (v4.1, v4.2):** New section added, substantive numerical update (e.g., launch target revision), new risk identified, locked decision becomes unlocked (or vice versa).
- **Patch (v4.0.1):** Typo fixes, formatting cleanup, added cross-references, new research citation. Usually batched with the next minor.

A version bump without a changelog entry is not a valid version bump. Always write the changelog first, then update the doc.

---

*Document version: 1.0 — April 21, 2026 — created for GitHub migration. Update in the same commit as any strategic doc version bump.*
