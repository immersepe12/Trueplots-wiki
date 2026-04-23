# TruePlots — Project Orientation

*This folder is the canonical local home for the TruePlots project. It supersedes the Claude project-file workspace. All edits happen in place; files are versioned on disk; deprecated versions move to `05-deprecated/`.*

*Last updated: April 21, 2026. Update this file whenever documents are added, versions change, or scope shifts.*

---

## What changed recently

- **April 21, 2026 — Agent-inclusive pivot.** Kushal met with Eshwar (founder, Delight Realty). Real estate agents are now a first-class part of the platform via Delight Realty's 100+ trusted agent network. Every listing is jointly verified by agent + TruePlots. Premium listings move to tripartite exclusive selling agreements. Commission splits, liability, and exclusivity mechanics TBD pending Eshwar meeting #2. Strategic docs updated from v3 to v4 to reflect this.
- **April 2026 — Cowork handoff.** Project moved from Claude web workspace (read-only copies) to local folder on Kushal's machine. All future edits happen here in place.
- **April 2026 — Code Session 1 shipped.** Claude Code Session 1 of 5 shipped on main (`e56f905`). Next.js 15.1, Supabase schema, design system tokens. Session 2 prompt queued (UI integration from Claude Design HTML outputs).

---

## How to use this folder

If you are an AI agent or new collaborator, read this file first, then read the three current source-of-truth documents (flagged below), then stop and ask clarifying questions before producing any new output. Do not read deprecated versions unless specifically asked — they will mislead you.

If you are making changes to the project, update this file in the same session. A stale orientation document is worse than none.

---

## What TruePlots is (one paragraph)

TruePlots is a verified plots marketplace for South India with a built-in fractional facilitation layer. Every listing is legally verified before buyers see it, and every listing agent is vetted before they can post. Plots too large for a single buyer are sold as individual slices once buyer thresholds are met — Delight Eco Farms' capital acquires the plot, TruePlots handles legal subdivision, and each buyer receives an individually-titled parcel. Supply comes primarily through a curated agent network: Delight Realty (Eshwar) brings 100+ trusted agents to the platform at launch. Two verticals are in scope: farmland (hero product, launches month 0) and urban residential sites (secondary, launches month 4 conditional on a three-gate check). TruePlots is a spin-off of Delight Eco Farms, with Delight Eco Farms as operational parent and equity partner, and Delight Realty as agent-network partner.

---

## Folder structure

```
trueplotscowork/
├── README.md                          (this file — orientation)
├── 00-current/                        (source-of-truth current docs — READ THESE FIRST)
│   ├── trueplots-project-document-v4.md
│   ├── trueplots-gtm-plan-v4.md
│   └── trueplots-project-pitch-v4.md
├── 01-design/                         (design system + design prompts — to be populated)
├── 02-claude-code-prompts/            (build sprint prompts — to be populated)
├── 03-research/                       (competitive + market research)
├── 04-trueplots-spec/                 (product/platform specs derived from research)
├── 05-deprecated/                     (old doc versions — historical record)
└── 06-operations/                     (hiring, tooling, vendor docs — to be populated)
```

---

## Source of truth — read these first

These three documents are the current authoritative version. All strategic decisions should reference these.

| Document | What it is | When to read it |
|---|---|---|
| `00-current/trueplots-project-document-v4.md` | Master project doc — product, market, competition, positioning, business model, platform scope, risks. **Includes agent-inclusive marketplace model.** | Any strategic question |
| `00-current/trueplots-gtm-plan-v4.md` | 12-month go-to-market plan with month-by-month phases, decision gates, and agent onboarding workstream | Any question about launch, sales, marketing, channels, sequencing, agent scaling |
| `00-current/trueplots-project-pitch-v4.md` | 2-page external pitch document (investors, partners, advisors) | When something needs to be sent externally |

If you read nothing else, read these three.

---

## Supporting research — read when relevant

Located in `03-research/`. These informed the v4 documents and remain authoritative on their specific topics; the v4 docs are the synthesis.

**Farmland competitive analysis:**
- `01-research-notes.md` — raw findings
- `03-landscape-map-updated.md` — landscape synthesis
- `04-whitespace-analysis.md` — defensibility read
- `05-pricing-benchmarks.md` — unit economics
- `06-positioning-options.md` — three positioning options (Access-First was selected)
- `07-blind-spots.md` — founder blind spots
- `09-executive-summary.md` — 1-page synthesis
- Competitor YAMLs: `saptashwa-jagati-farms.yaml`, `swasya-living.yaml`, `sanctity-ferme.yaml`, `mytan-hasiru-sanjeevani-triguna.yaml`, `farmland-bazaar.yaml`, `layout-developers.yaml`
- Related: `managed-farmland-alternatives.md`, `how-to-buy-farmland-jointly-in-karnataka.md`, `swasya-living-alternative.md`, `trueplots-vs-99acres-farmland.md`

Read when: assessing farmland competition, fractional farmland market sizing, Saptashwa/Swasya-specific questions.

**Urban sites top-up analysis:**
- `01-urban-sites-research-notes.md`
- `03-urban-landscape-addendum.md`
- `04-urban-whitespace-analysis.md`
- `05-urban-pricing-benchmarks.md`
- `06-urban-blind-spots.md`
- `09-urban-executive-summary.md`
- Competitor YAMLs: `nobroker.yaml`, `99acres-plots.yaml`, `magicbricks-homes247-squareyards.yaml`

Key findings: NoBroker is primary fast-follow threat with 9-12 month window; A-Khata-only at launch; fractional urban still whitespace. Note that NoBroker's agent-removal thesis is structurally different from TruePlots' agent-verification thesis (v4 update).

**Spinny product research (as a UX/service analog, not a business model):**
- `01-spinny-research-notes.md` — raw findings
- `11-spinny-ui-ux-analysis.md` — **critical** — 15 patterns from screenshots that text research missed
- `10-executive-summary.md` — top 15 build priorities, ranked

**TruePlots product/platform specs** (in `04-trueplots-spec/`):
- `03-trueplots-120-checkpoints-farmland.md` — **the 120-point farmland verification checklist**
- `04-trueplots-checkpoints-urban.md` — ~80-point urban site checklist
- `05-trueplots-trust-guarantees.md` — money-back, warranty, fixed-pricing proposals
- `06-trueplots-loan-integration-spec.md` — partner bank list and financing flow
- `07-trueplots-page-specs.md` — page-by-page wireframes
- `08-trueplots-service-layer-map.md` — service layer
- `09-what-does-not-translate.md` — Spinny features to avoid copying
- `12-trueplots-design-system.md` — consolidated design system

Read when: any product build, UX, design, platform engineering question.

---

## Deprecated documents — do not use

Located in `05-deprecated/`. These exist for historical continuity but should not inform current decisions. If you see them referenced, note they are deprecated and reference the v4 equivalents instead.

| Deprecated | Replaced by |
|---|---|
| `trueplots-project-document-v3.md` | `00-current/trueplots-project-document-v4.md` |
| `trueplots-gtm-plan-v3.md` | `00-current/trueplots-gtm-plan-v4.md` |
| `trueplots-project-pitch-v3.md` | `00-current/trueplots-project-pitch-v4.md` |

Older versions (v1, v2, product briefs, hire explainer, HubSpot setup, pre-v3 Claude Code prompts) are referenced in the handoff document and need to be copied in from Kushal's download-archive of his Claude project files. Flagged in the handoff review below.

---

## Key decisions already locked — do not re-litigate

These are settled. If you find yourself wanting to re-open them, check with Kushal first.

1. **Brand name:** TruePlots (TM cleared Class 36, domain secured)
2. **Positioning:** Access-First — "Own premium farmland from ₹40 lakh" is the hero. Verification is infrastructure, not the hero message. Updated in v4 to add verified-agents as second trust layer beneath verification.
3. **Business model:** Facilitator, not developer. Delight's capital acquires plots only after buyer thresholds are met. Customer funds never pool (stays outside SEBI CIS regulation).
4. **Scope:** Farmland-first brand, urban sites as secondary category, gated through three checks at month 4.
5. **Urban launch rule:** A-Khata only. B-Khata plots excluded at launch due to mainstream-loan financing constraints that break fractional affordability.
6. **Competitive positioning:** Farmland has 12-18 month defensibility window. Urban has 9-12 month window (NoBroker fast-follow risk). Moat lives in operational stack + agent network, not UI.
7. **Spinny as product model (not business model):** TruePlots adopts Spinny's trust architecture, verification framing, UX patterns, and service layers — but not Spinny's buy-and-hold inventory model.
8. **Three-layer verification framing:** badge ("120-point verified") + LDP detail ("48 documents, 12 database checks, 4 field inspections, 3 legal experts") + scorecard (10 category scores out of 10 + trust chips).
9. **Partnerships:** Delight Eco Farms is spin-off parent, equity investor, operational partner (brother is co-founder/operator). **Delight Realty (Eshwar) is agent-network partner bringing 100+ trusted agents; commercial terms finalizing in meeting #2 (new in v4).**
10. **Agent-inclusive model (new in v4):** Agents are first-class platform participants. Every listing is jointly verified. Attribution appears on every listing card and LDP ("Listed by [Agent] · Verified by TruePlots"). Public agent scorecard in month 6. Exclusive tripartite agreements for premium inventory.

---

## Open questions — still live

These have not been resolved and will need decisions as the project progresses.

**Commercial (pending Eshwar meeting #2):**
1. Exact agent commission split on standard listings (1% baseline; TruePlots and Delight share TBD)
2. Exclusive tripartite listing commission structure and term length
3. Buyer-side vs seller-side commission payment mechanics
4. Cross-agent referral economics
5. Bad-agent removal thresholds, process, appeal path
6. Liability structure if a verified listing has a later-discovered title defect

**Strategic (carried over from v3):**
7. Exit/resale mechanism for fractional buyers — when buyer #2 wants to sell their 1.5-acre parcel 2 years later, how does that flow?
8. RERA facilitator-vs-promoter classification — being resolved via Karnataka RERA specialist counsel memo before month-4 urban launch. Memo must also cover platform liability in agent-listed transactions.
9. Karnataka Section 79A/B status — currently repealed but politically contested. Monitor monthly.
10. Fundraising timing and size — ₹79-117L year-1 budget is bootstrap-possible but tight; ₹3-5cr seed around month 5-6 creates comfort.
11. Urban fractional coordination fee pricing — current ₹50-75K assumption untested.
12. BMRDA layout developer partnership economics.

---

## How to reason about a new request

If Kushal asks a question or requests new output, the order to think about it is:

1. **Is this settled in Section "Key decisions locked"?** If yes, the answer references the locked decision; don't re-open it.
2. **Is this covered in the v4 source-of-truth docs?** If yes, start from there and cite the section.
3. **Is this a product/design/build question?** Go to `04-trueplots-spec/` files (especially `12-trueplots-design-system.md` and `07-trueplots-page-specs.md`), then `03-research/11-spinny-ui-ux-analysis.md`.
4. **Is this a competitive/market question?** Go to `03-research/` (farmland files) or `03-research/` (urban files — prefixed `*-urban-*`).
5. **Is this a new question not covered anywhere?** Ask clarifying questions before producing output. Do not invent context.

---

## Working conventions (from Cowork handoff)

1. All project documents live in this folder. No more Claude project files. No more copying to outputs. Edit files in place.
2. Version documents when substantive changes happen. A typo fix is v4, a new section is v4.1, a meaningful business model change is v5. Keep the version header current with a one-line summary of what changed.
3. Deprecated files move to `05-deprecated/` — do not delete. Old versions are historical record.
4. Kushal's preference: short, conversational responses over formal reports. He is a founder who has built startups. Skip caveats and preambles. Go directly to answers and proposed actions.
5. Use the `TBD` marker for anything not yet negotiated or decided. Do not fabricate numbers or terms. "TBD pending Eshwar meeting #2" is a valid placeholder.
6. When in doubt about scope, ask rather than expanding. This project has hard-won focus. Creeping scope kills momentum.

---

## Missing files flagged for review

The following files are referenced in the Cowork handoff document but were not present in the source knowledge pack. Kushal may need to drop these in from his Claude Code repo or download archive:

**01-design/:**
- `trueplots-design-system-v1.md`
- `claude-design-prompt-trueplots.md`
- `claude-design-prompt-trueplots-ui.md`

*Note:* `12-trueplots-design-system.md` exists in `04-trueplots-spec/` and may be the same document as or a predecessor to `trueplots-design-system-v1.md`. Confirm with Kushal.

**02-claude-code-prompts/:**
- `claude-code-prompt-session-1-foundation.md` (shipped — likely archived in repo history)
- `claude-code-prompt-session-2-ui-integration.md` (**READY TO EXECUTE — critical to surface before Kushal runs Session 2**)

**05-deprecated/:**
- `trueplots-project-document-v1.md`
- `trueplots-project-document-v2.md`
- `trueplots-gtm-plan-v1.md`
- `trueplots-gtm-plan-v2.md`
- `trueplots-project-pitch.md` (v1)
- `trueplots-project-pitch-v2.md`
- `trueplots-product-brief.md`
- `trueplots-product-brief-v0.2.md`
- `claude-code-prompt-spinny-research.md`

**06-operations/:**
- `trueplots-hire-explainer.md`
- `trueplots-hubspot-setup.md`
- `claude-code-prompt-competitive-analysis-v2.md`
- `claude-code-prompt-urban-sites-topup.md`

---

## How to keep this document fresh

This document must be updated when:

- A new version of any source-of-truth document is created (move old version to deprecated list, update the source-of-truth table)
- A new research document is added to any subdirectory
- A major decision moves from "open question" to "locked"
- Scope changes (new vertical, new geography, new product layer, new partnership)
- The project phase changes (launch → growth → scale)

One-line updates are fine. Don't let perfect be the enemy of current.

**Rule of thumb:** if you finish a session where any of the above happened, update this document before closing the session.

---

*Orientation document version: 2.0 (updated for Cowork handoff + v4 agent-inclusive pivot, separate from project document versioning).*
