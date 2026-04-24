---
classification: confidential
owner: GrowDirect LLC
type: proof-case
status: first-draft
applied-method: method/retail-diagnostic.md
---

# Proof Case — Canary Retail, Applied to Itself

A self-diagnostic. The [[../method/retail-diagnostic|retail-diagnostic
method]] is framed against a retailer's operating reality. Here we
point it at GrowDirect's own platform-build work and ask the seven
questions the method would ask of any retailer.

This is the "proof case on ourselves" leg of the CIO leave-behind
wedge. We don't ship a method to retailers until we've used it on
ourselves. This article is the distilled output; the full pptx
deck is produced by the `consulting:retail-diagnostic` skill run
against a structured evidence pack derived from this document.

## Section 1 — Executive Summary (one page)

**The one-line thesis.** GrowDirect has the ingredients of a full
retail operating system — ARTS-native canonical data model,
multi-tenant platform, detection + case engine, agent mesh,
methodology skills, cleanup discipline — but the parts have been
built in isolation. The prize is in connecting them into a coherent
platform narrative.

**The two themes the diagnostic focuses on.**

- **Theme 1 — Platform Coherence.** Five independently-built modules
  (T, R, N, A, Q) are ready to ship. Nine modules are roadmap. The
  prize is integrating the five, not building the nine.
- **Theme 2 — Productization of Method.** Two consulting skills
  (retail-diagnostic, it-architecture-options) exist as v0.1
  scaffolds. Productizing them into reproducible engagement-grade
  outputs is the difference between "consulting veteran" and
  "CIO leave-behind."

**Prize sizing (low/high, first-year).**

| Driver | Low | High |
|---|---|---|
| Canary Retail as platform sale (vs. LP-only) | 2× | 4× |
| Consulting plugin as revenue stream | +25% | +60% |
| Method as licensable IP | n/a yet | material year-2 |

**Roadmap headline.** Phase 1 (quick wins, Q1–Q2): ship v1
Differentiated-Five, land 3 SMB specialty retailers as v1 customers,
run consulting-skill first dogfood engagement. Phase 2 (Q3–Q4):
v2 CRDM expansion modules (C/D/F/J). Phase 3 (year 2): v3 full
spine + method licensing.

## Section 2 — Background, Scope & Approach

**Workshop themes.** CTO-readiness audit (cleanup, confidentiality,
verification), platform-brand consolidation (three external-facing
surfaces), methodology extraction (CATz from prior engagement
archive), proof case (Solex as first live commerce test client).

**Scope.** Canary Retail product repo + CATz methodology vault +
Canary-Retail-Brain product vault. Excludes: Cove (hobby tier),
Angel (hobby tier), Seacove (hobby tier), GrowDirect monorepo
(internal-only).

**Approach.** Code audit + security audit + cold-reader verification
+ methodology extraction + cross-vault sanitization. Produced 31+
cleanup commits across 4 branches. Scaffolded 2 new externally-
facing vaults. Applied authoring rules uniformly.

## Section 3 — Financial Analysis & Industry Drivers

*(Placeholder — for a customer engagement, this section would carry
the retailer's financial baseline. For this self-diagnostic it's
narrative only.)*

**Industry context.** The SMB specialty retail segment is
underserved by retail software. Enterprise retail suites are
oversized; POS-only tooling is undersized; the platform tier in
between is what Canary Retail targets. ARTS standards adoption is
a credibility move nobody in the segment has made.

**Competitive landscape.** Big 4 AI-consulting products (Zora, the
rest) are pitching the concept of a productized methodology; they
haven't shipped one yet. GrowDirect's plugin architecture ships one.

## Section 4 — Theme 1: Platform Coherence

### 4.1 Overview

**Findings.** Canary Retail has five v1 modules implemented against
a shared canonical data model. Integration across modules is
architecturally supported but not uniformly demonstrated. The
thirteen-module spine is published; four modules are roadmap.

**Root-cause navigator.** Fragmented demo story / Untested integration
paths / Roadmap dilution risk / Module-boundary clarity / Proof-case
coverage.

**Three callouts.**
- The platform claim is true at the code level.
- The platform claim is not yet proven at the customer-demo level.
- Making it true is a matter of integration testing and demo-story
  wiring, not net-new module work.

### 4.2 The Prize

Platform-tier pricing vs. point-solution pricing, with a simultaneous
increase in retention (platform customers churn less than point-
solution customers). Low range: 2× average contract value on v1
customers vs. equivalent LP-only deal. High range: 4× with the full
Differentiated-Five story resonating.

### 4.3 Drill — Fragmented Demo Story

- **Findings:** Atlas knowledge graph exists. `/ops/method` page
  ships six narrated panels. MERCHANT_PROFILE describes the demo
  tenant narrative. But a cold visitor clicks through Canary and
  sees a loss-prevention tool, not an operating system.
- **Leading Practice:** Enterprise retail platforms lead with the
  operating-model diagram and drill into modules. The homepage is
  a platform pitch, not a feature list.
- **Conclusion:** Rewrite the `/home` story to open with the
  thirteen-module spine + Differentiated-Five highlighted.

### 4.4 Drill — Untested Integration Paths

- **Findings:** Transaction pipeline (T) feeds detection (Q) cleanly.
  Customer (R) and Device (N) modules exist but are rarely queried
  together in the demo flow. Asset (A) anomaly detection is module-
  complete but doesn't yet appear in merchant-visible dashboards.
- **Leading Practice:** Cross-module queries are the platform's
  proof. Every demo session exercises 3+ modules.
- **Conclusion:** Add 2-3 cross-module queries to the demo flow
  (customer × transaction; device × asset anomaly).

### 4.5 Drill — Roadmap Dilution Risk

- **Findings:** Nine modules on the v2/v3 roadmap. Historical pattern:
  roadmap expands before v1 locks in. Risk of building v2 modules
  before v1 Differentiated-Five customers land.
- **Leading Practice:** Ship v1 in production against 3+ paying
  customers before starting v2 development.
- **Conclusion:** Phase-gate v2 work against v1 customer acquisition.

### 4.6 Recommendations — Theme 1

1. Rewrite Canary `/home` as platform landing (not LP landing).
2. Add cross-module queries to demo flow. Exercise R × T × Q in
   one click-path.
3. Phase-gate v2 roadmap on v1 customer acquisition (≥3 paying
   SMB specialty retailers).
4. Ship a proof-case deck per v1 customer (the retail-diagnostic
   skill eats its own dog food).

## Section 5 — Theme 2: Productization of Method

### 5.1 Overview

**Findings.** Two consulting skills are scaffolded at v0.1 (retail-
diagnostic, it-architecture-options). Methodology is preserved in
Brain wikis. pptx templates and prompt engineering are not yet
complete. Neither skill has been run against production evidence.

**Root-cause navigator.** pptx template gap / Evidence-pack
specification / Skill dogfood / Vertical customization /
Partnership packaging.

**Three callouts.**
- Method is documented; execution is not yet uniform.
- v0.1 is a valid starting point; v1 requires a working demo run.
- Customer willingness to pay for method increases sharply once
  they see a generated deck.

### 5.2 The Prize

Consulting revenue per engagement. A small-retailer engagement
landing a Phase I assessment and a three-phase roadmap carries six-
figure first-year fee ranges. Plus post-engagement SaaS ACV (Canary
Retail tenant). Plus method-license revenue if the plugin moves
from internal-use to partner-distribution.

### 5.3 Drill — pptx Template Gap

- **Findings:** Skills produce structured JSON. pptx assembly from
  JSON requires a template library (slide masters) that doesn't yet
  exist. Dispatch 2 flagged this as Sprint 2 work.
- **Leading Practice:** A ready-to-paste pptx template library is the
  delta between "writes prose" and "delivers a deck."
- **Conclusion:** Sprint 2 builds the master library. Template per
  skill-output slide type.

### 5.4 Drill — Skill Dogfood

- **Findings:** Neither skill has been run against real evidence
  yet. The self-diagnostic in this article is a hand-written proxy,
  not a skill-produced artifact.
- **Leading Practice:** Run skill on self first; use the output to
  validate the skill's fidelity; use the gaps to tune.
- **Conclusion:** Next sprint dispatches a retail-diagnostic run
  against GrowDirect evidence and compares output to this document.

### 5.5 Recommendations — Theme 2

1. Build pptx master library for retail-diagnostic skill (sprint 2).
2. Build pptx master library for it-architecture-options skill
   (sprint 2).
3. Run retail-diagnostic against GrowDirect as first dogfood case.
4. Run retail-diagnostic against first paying SMB customer as first
   external case.
5. Package both skills as a cowork plugin for external distribution.

## Section 6 — Opportunity Priorities & Roadmap

### Recommended initiatives (scored)

| # | Focus | Recommendation | Platform | Revenue | Defensibility | Cost | Complexity |
|---|---|---|---|---|---|---|---|
| 1 | Platform coherence | Rewrite /home as platform landing | ● | ● | ● | ○ | ○ |
| 2 | Platform coherence | Cross-module demo queries | ● | ○ | ● | ○ | ○ |
| 3 | Platform coherence | Phase-gate v2 on v1 customers | ○ | ● | ● | ○ | ○ |
| 4 | Method productization | pptx template library | ○ | ● | ● | ◐ | ◐ |
| 5 | Method productization | Self-dogfood retail diagnostic | ○ | ◐ | ● | ○ | ◐ |
| 6 | Method productization | Plugin distribution | ○ | ● | ● | ◐ | ● |

Legend: ● material, ◐ moderate, ○ minimal.

### 2×2 prioritisation

- **High prize / low cost** → 1, 2, 3, 5 (Phase 1)
- **High prize / higher cost** → 4, 6 (Phase 2)
- No recommendations fall into low-prize / high-cost.

## Section 7 — Prioritised Case for Action

**Phase 1 — Q1–Q2 2026 — Quick wins (what ships now).**

- /home rewrite (1 week)
- Cross-module demo queries (2 weeks)
- First paying SMB specialty customer landed (ongoing)
- Self-dogfood retail-diagnostic pass against GrowDirect (1 sprint)
- CATz + Canary-Retail-Brain vault publication (this week)
- CTO partner engagement (ongoing)

**Phase 2 — Q3 2026 — System build (what ships next).**

- pptx template library (both skills)
- v2 CRDM expansion modules (C, D, F, J) phase-gated on v1
  customer milestone
- Plugin distribution packaging
- Second paying customer onboarded
- Board pitch packet

**Phase 3 — 2027 — End state.**

- Full 13-prefix spine shipping
- Method licensable to partners
- Board + investor materials mature
- Multi-vertical case studies
- Agent mesh fully expressed in CBM v2 governance

**Milestones overlay.** CTO-partner access (this week). First SMB
specialty customer signed (Q1). Self-dogfood diagnostic complete
(Q1). v1 production-ready (Q2). v2 development start (Q3, gated).

## What this self-diagnostic demonstrates

1. **The method applies to us.** Every section of the 7-section
   frame fits GrowDirect's current platform-build state. No section
   is forced.
2. **The prize is concrete.** Two named themes with two quantified
   ranges. No hand-waving about "transformation."
3. **The drill pattern is symmetric.** Each theme gets Overview →
   Prize → 2–3 drills → Recommendations. Reader is trained once.
4. **The roadmap is phased against milestones already on our
   calendar** — customer acquisition, sprint cycles, board
   readiness — not a new programme overlaid on ours.
5. **The deck writes itself** from this document + the skill's pptx
   master library. Sprint 2 produces that library; this document
   is the evidence pack.

## Next action

Dispatch the `consulting:retail-diagnostic` skill against the
evidence pack derived from this document. Compare the generated
deck against this hand-written version. Tune skill prompts until
the two match. That pass becomes the first validated skill output
and the first externally-ready proof-case deck.

## Related

- [[../method/retail-diagnostic]]
- [[../method/it-architecture-options]]
- [[../method/roles/data-detective]]
- [[../cbm-v2/overview]]
