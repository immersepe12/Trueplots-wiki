# AGENTS.md — Reading guide for AI agents

*This file is the entry point for any AI agent (Claude Code, Cowork, Cursor, Copilot, custom) asked to understand or act on the TruePlots project. Read this first. Do not skip. A stale read of this file leads to stale decisions.*

---

## 1. What this repo is

This is the **strategy and product documentation** for TruePlots — a verified plots marketplace for South India. Every strategic, product, market, and operational decision is written down here.

This repo is NOT the application code. The code lives in a separate repo (the TruePlots Next.js + Supabase codebase). If you are asked to write code, that happens in the code repo; this repo is the source of intent that the code must reflect.

**If you are an AI agent doing strategy, market, product, GTM, or operational work:** read this repo.
**If you are an AI agent writing code:** read this repo for context, then switch to the code repo for implementation.

---

## 2. What TruePlots is (60 seconds)

TruePlots is a verified plots marketplace for South India with built-in fractional access. Every listing is legally verified by a 120-point checklist before buyers see it. Plots too large for a single buyer can be jointly purchased by three buyers (two for urban 60×40 splits) — Delight Eco Farms' capital acquires the plot, TruePlots handles legal subdivision, and each buyer receives an individually-titled parcel.

Two categories are in scope, sequenced:
- **Farmland** — hero product, launches month 0, 100-200 listings at launch via agent partner network.
- **Urban residential sites** — secondary, launches month 4 conditional on a three-gate check.

Supply comes primarily from Delight Realty's 100+ trusted real estate agent network (Eshwar partnership). Every listing is jointly verified by agent + TruePlots before going live. Premium plots use tripartite exclusive selling agreements.

**Key brand and positioning:** "We don't fight the existing system, we organize it. Agents get products, we get customers."

**Parent company:** Delight Eco Farms (6 years, 140+ acres across 4 Karnataka districts). TruePlots is a spin-off.

**Founder:** Kushal (sole founder). Co-founder: brother (Delight Eco Farms operator). Partner: Eshwar (Delight Realty).

For the full one-pager, read `00-current/trueplots-project-pitch-v4.md`.

---

## 3. Reading order for a new agent

In this exact order. Do not skip. Do not read deprecated files unless specifically asked to.

1. `AGENTS.md` (this file)
2. `README.md` — folder orientation
3. `GLOSSARY.md` — term definitions. Many key terms in the strategic docs are India-specific (PTCL, 79A/B, A-Khata, BBMP, RERA, CIS, etc.). Read the glossary before the strategic docs or you will misunderstand.
4. `00-current/trueplots-project-document-v4.md` — master doc. Product, market, competition, positioning, business model, platform scope, risks. Authoritative on any strategic question.
5. `00-current/trueplots-gtm-plan-v4.md` — 12-month go-to-market. Authoritative on sequencing, phases, decision gates, channel strategy, hiring.
6. `00-current/trueplots-project-pitch-v4.md` — 2-page external pitch. Authoritative on how to describe TruePlots to outsiders.

If you have read these six files you have enough context to reason about 95% of questions.

For specific domains, continue:
7. `04-trueplots-spec/` — product and platform specs (verification checklists, trust guarantees, loan integration, page specs, service layer, design system)
8. `03-research/` — competitive research, whitespace analysis, positioning options, Spinny benchmarks
9. `02-claude-code-prompts/` — build-session prompts for Claude Code. Read the latest shipped prompt to know what the app currently does.
10. `CHANGELOG.md` — doc version history

Deprecated files are in `05-deprecated/`. Do not read them unless specifically asked. They will mislead you.

---

## 4. Decisions already locked — do NOT re-open

If any of these come up in your task, cite the locked decision rather than reconsidering it. Only open a re-litigation conversation if Kushal explicitly asks.

1. **Brand:** TruePlots, Class 36 trademark filed, domain secured.
2. **Positioning:** Access-First — "Own premium farmland from ₹40 lakh" is the hero message. Verification is infrastructure, not the headline.
3. **Business model:** Facilitator, not developer. Delight's capital acquires plots only after buyer thresholds are met. Customer funds never pool. Stays outside SEBI CIS regulation.
4. **Scope:** Farmland-first brand. Urban sites secondary, gated by three checks at month 4.
5. **Urban launch rule:** A-Khata only. B-Khata plots excluded at launch (financing constraint breaks fractional affordability).
6. **Moat composition:** Operational stack + agent network, not marketplace UI. UIs are copyable in a sprint; the 100-agent network + 120-point verification + subdivision playbook + services layer is not.
7. **Agent-inclusive model (v4):** Agents are first-class platform participants. Every listing is jointly verified by agent + TruePlots. Attribution line "Listed by [Agent] · Verified by TruePlots" appears on every listing card and LDP. Agent scorecard, dashboard, and profile pages are month 3 — not launch scope.
8. **Partnerships:** Delight Eco Farms (spin-off parent, equity, operations) + Delight Realty (agent network, Eshwar as partner). Commission splits TBD pending Eshwar meeting #2.
9. **Three-layer verification framing:** badge ("120-point verified") + LDP detail ("48 documents, 12 database checks, 4 field inspections, 3 legal experts") + 10-category scorecard with trust chips.
10. **Spinny as product model only:** TruePlots adopts Spinny's trust architecture, verification UX, and service patterns — NOT Spinny's buy-and-hold inventory model.

For the full list and rationale, see `00-current/trueplots-project-document-v4.md` Section 5.4 and the "Key decisions already locked" section of `README.md`.

---

## 5. Decisions still open — watch for updates

These are actively unresolved. If your task touches any of them, note that they are open and that your output is contingent on the resolution.

**Commercial (pending Eshwar meeting #2):**
- Exact agent commission split on standard listings
- Exclusive tripartite commission structure
- Buyer-side vs seller-side payment mechanics
- Cross-agent referral economics
- Bad-agent removal thresholds
- Liability structure for later-discovered title defects

**Strategic:**
- Exit/resale mechanism for fractional buyers
- RERA facilitator-vs-promoter classification (specialist memo in progress)
- Karnataka Section 79A/B restoration risk (monitor monthly)
- Fundraising timing (bootstrap possible year 1; ₹3-5cr seed creates comfort month 5-6)
- Urban fractional coordination fee pricing (₹50-75K untested)
- BMRDA layout developer partnership economics

For the full list see `00-current/trueplots-project-document-v4.md` Section 11.2.

---

## 6. How to reason about a new request

If Kushal (or someone acting for him) asks a question or requests new output:

1. Is the answer in the **locked decisions** above? → Cite the decision. Don't re-open.
2. Is the answer in the **v4 source-of-truth docs** (project document / GTM / pitch)? → Start there and cite the section.
3. Is it a **product / design / build question**? → Go to `04-trueplots-spec/` (especially `12-trueplots-design-system.md` and `07-trueplots-page-specs.md`) and `03-research/11-spinny-ui-ux-analysis.md`.
4. Is it a **competitive or market question**? → Go to `03-research/` — farmland files (numeric prefix) or urban files (prefixed `*-urban-*`).
5. Is it a **new question not covered anywhere**? → Say so explicitly. Ask clarifying questions. Do not invent context.

---

## 7. Response conventions Kushal expects

He is a founder with prior startup experience. He moves fast. He dislikes:

- Long preambles and throat-clearing
- Repeated pushback on the same point (say it once, then defer)
- Reports when a 3-sentence answer would do
- Hedging language ("I think maybe it could possibly...")
- Consensus-seeking when a direct recommendation is possible
- Markdown lists for simple answers

He prefers:

- Short, conversational responses
- Direct recommendations ("I'd do X because Y")
- Specifics over generalities (actual numbers, actual URLs, actual file paths)
- Proposing a concrete next step rather than asking what to do
- Flagging real risks bluntly once, then respecting his decision
- "One task at a time" — when executing a multi-step task, give him one step, wait for confirmation, then the next

When writing documents (not conversation), the opposite applies: be thorough, comprehensive, structured. Documents are the archive. Conversations are the execution layer.

---

## 8. Placeholders to watch for

Any time you see these markers in a doc, treat them as known-unknowns, not as mistakes:

- **TBD** — decision pending
- **TBD pending Eshwar meeting #2** — commercial terms waiting on partnership meeting
- **Placeholder** — stub content to be filled in later
- **Month X — [feature]** — scheduled feature not yet built
- **Coming Soon** / **Draft** / **In progress** — UI states for features in planning

Do NOT replace these with invented specifics. If you need to reference a number or term that is TBD, keep the TBD and note what you would recommend if a value were needed.

---

## 9. When to propose updates to these docs

Strategic docs change when:
- Eshwar meeting #2 lands (commission terms)
- RERA counsel memo lands (regulatory classification)
- First fractional farmland deals close (GTM validation data)
- Month 4 three-gate decision (urban launch go/no-go)
- 79A/B regulatory changes in Karnataka
- Competitive moves from NoBroker or Farmland Bazaar
- A new vertical or geography is added
- A new partnership is signed

If your task surfaces information that would substantively change any v4 doc, say so at the end of your output. Do not silently rewrite strategic docs.

Typo fixes, formatting cleanup, additions of links or cross-references — fine to do inline, note in your response. Substantive changes (new section, changed number, changed positioning) — propose first, wait for Kushal's greenlight.

---

## 10. File structure reference

```
trueplots-docs/
├── AGENTS.md                        (this file — read first)
├── README.md                        (folder orientation + key decisions)
├── GLOSSARY.md                      (terms and definitions)
├── CHANGELOG.md                     (doc version history)
├── 00-current/                      (source-of-truth strategic docs)
│   ├── trueplots-project-document-v4.md
│   ├── trueplots-gtm-plan-v4.md
│   └── trueplots-project-pitch-v4.md
├── 01-design/                       (design system + design prompts)
├── 02-claude-code-prompts/          (build sprint prompts)
├── 03-research/                     (competitive + market research)
├── 04-trueplots-spec/               (product + platform specs)
├── 05-deprecated/                   (old doc versions — do not use)
└── 06-operations/                   (hiring, tooling, vendor docs)
```

---

## 11. Contact

This repo is maintained by Kushal (founder, kushal@exar.fit) with AI assistance via Cowork. If you are an agent with a question you cannot resolve from the docs alone, surface it to Kushal directly — do not improvise.

---

*Document version: 1.0 — April 21, 2026 — created for GitHub migration. Update when reading conventions or locked decisions change.*
