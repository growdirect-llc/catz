---
classification: confidential
owner: GrowDirect LLC
type: method-artifact
phase: II
workstream: between W1 (To-Be Workshops) and W4 (IT Architecture); also feeds Phase III SDD inputs
---

# Phase II Artifact — Module Functional Decomposition

This artifact is the synthesis of a generation of retail planning, integration, and operations work — distilled into one decomposition pattern Canary commits to. Lineage acknowledged here once so the rest of the document can stand on its own.

## What it is

A **per-module card** that decomposes one spine module into the L2 process areas, L3 functional processes, user stories, substrate contracts, and assumption markers required to plan, build, and operate that module against a target POS substrate. The card is the bridge between two existing CATz artifacts:

- **Solution Map** (W1→W5) sets the L1 cell — coverage strength of one module against one platform (●/◐/★/◯/✗)
- **SDD** (Phase III) carries the L4 — code, schema, deployment

Without the Module Functional Decomposition, those two artifacts disagree silently: the Solution Map says "this is a Canary-native build" but the SDD has no decomposition of what *processes* to build, and no record of what assumptions are platform-knowable vs only resolvable per-customer.

The card closes that gap. One per spine module per engagement.

## When to produce it

Per spine module identified as in-scope by Phase II To-Be Workshops:

- **Draft 1** — when the module's Solution Map cell is set (early Phase II). Establishes L2 areas, L3 processes, initial user stories, assumption markers
- **Draft 2** — after first technical conversations with the customer (mid Phase II). Resolves assumption markers that turned out to be platform-knowable; sharpens cross-module contracts
- **Final** — at start of Phase III SDD drafting. Customer-specific overrides populated; assumption markers either resolved or escalated

The card is a **living artifact** for the lifetime of the engagement. Customer-specific overrides accrete over time; resolved assumptions document what was learned.

## Structure

```
L1 (Solution Map cell)         set elsewhere by W1→W5
                                 │
L2 (Process areas)               6-8 process areas per module
                                 │
L3 (Functional processes)       ~30-50 per module, grouped under L2s
                                 │
L4 (Implementation detail)      lives in the SDD, NOT this card
```

### Required sections per card

The format below is non-negotiable. Per-engagement variation goes in customer-specific overrides at the end, not in restructuring the card.

| Section | Purpose |
|---|---|
| Frontmatter | Module letter, Solution Map cell, companion modules, companion substrate, companion CATz, methodology note |
| Artifact-layer block under H1 | Names this card as one of three module artifact layers (canonical spec, code/schema crosswalk, functional decomposition); points at the other two |
| Governing thesis | One paragraph stating what this module owns and why. Opinions land here. No throat-clearing. |
| Executive summary | Quantified table — count of L2s, L3s, user stories, assumption markers, substrate contracts. Reader can scope effort from the table alone. |
| L1→L2→L3 framework | Visual tree showing the decomposition. Reader can navigate without reading the body. |
| L2 sections (one per process area) | Purpose statement. L3 process table (substrate / logic / notes). User stories. Cross-module contracts where applicable. Coverage posture noted explicitly for partial-coverage cells. |
| Substrate contract registry | What this module promises to downstream consumers. Symmetric to other modules' substrate-ingestion sections. |
| Assumption markers | Tagged `ASSUMPTION-{MOD}-{NN}`. Each has: assumption, what it blocks, resolution path. |
| Customer-specific overrides | Reserved format. Empty until a real engagement starts; populated thereafter. |
| Operating notes | Cross-cutting commentary — actors, methodology hooks, load-bearing assumptions worth pinning. |
| Related | Links to companion cards, substrate references, prior CATz artifacts. |

## Coverage-aware decomposition

The L2 split must reflect the L1 cell. Different cells produce different shapes:

| Solution Map cell | L2 split shape | Example |
|---|---|---|
| **● Full direct** | L2s organized around the substrate's own structure (endpoint families, document types). Coverage is uniform; the work is faithful adaptation. | Module T — substrate ingestion / sealing / parsing / publication / contracts |
| **◐ Partial / via** | L2s explicitly tagged Canary-native vs substrate-supplied vs bridge. The gap-shape IS the decomposition. | Module J — forecast/replenishment/OTB are ★ Canary-native; PO generation/receiving/RTV are ◐ substrate-supplied; recommendation+approval is the bridge |
| **★ Canary native** | L2s organized around the Canary-internal architecture (substrate ingestion / detection lifecycle / tuning / surface / phasing). External substrate is consumed but not central. | Module Q — substrate ingestion / detection rule execution / detection lifecycle / tuning / surface / vertical config / deployment phasing |
| **◯ External vendor** | L2s organized around the integration boundary (vendor data ingest / Canary-side projection / cross-module surface). Vendor is treated as substrate. | (no example yet — Module L native-vs-external decision pending per case-by-case) |

**The coverage tag is load-bearing.** Reviewers should be able to look at the L2 split and infer the L1 cell without checking the Solution Map. If they can't, the L2 split is wrong.

## Actor discipline

User stories carry an explicit actor. The actor must reflect the module's posture toward the substrate:

- **Observer modules** (Q, P-derived, A-derived) — actors are Canary-internal services and analyst-facing surfaces (Chirp, Owl, Fox, LP Analyst, Store GM). No "as a cashier" stories — those decompositions live in the POS UI, not in Canary.
- **Bidirectional modules** (J in particular, future C and F where Canary writes back to Counterpoint) — actor cast expands to include both Canary-internal services AND human-in-the-loop roles (Buyer, Department Head, VP Merch). The bidirection is named explicitly.
- **Substrate modules** (T, R, N, S, F where Canary reads but doesn't act) — actors are pipeline services (Adapter, Sealer, Parser, Publisher) and operational humans (Operator, Auditor).

The actor cast for each module belongs in §Operating notes and shows up as the subject of every user story. If a story's actor doesn't match the module's posture, either the story is wrong or the posture is misstated.

## Substrate contract registry

Every module both **owes** contracts to downstream consumers and **asserts** contracts on upstream producers. The card makes both explicit:

- **Producer-side contract registry** (this module's section §X.N — typically the last L2): what fields, preservation rules, and freshness commitments this module guarantees to downstream
- **Consumer-side contract assertion** (this module's substrate-ingestion L2): what upstream modules must surface for this module to function

The two perspectives must stay symmetric across sister cards. Drift between T's §T.7 (producer contracts) and Q's §Q.1 (consumer assertions) means a contract has silently broken. Naming both makes silent breakage impossible without explicit edit.

The contract registry also feeds Phase III: every contract becomes a contract test in the SDD's test suite.

## Assumption markers

Every card carries a section of `ASSUMPTION-{MOD}-{NN}` markers. Each marker has three required fields: the assumption itself, what it blocks if wrong, and the resolution path.

**Two distinct assumption shapes** — naming both keeps engagement planning honest:

| Shape | Resolution path | Engagement implication |
|---|---|---|
| **Platform-knowable** | Sandbox access, vendor doc deep-read, schema inspection | Resolvable once; resolution applies across all customers on that platform |
| **Engagement-knowable** | Per-customer interview, customer database inspection, customer-specific configuration | Resolvable per-customer only; CATz Phase II To-Be Workshops are the natural surface |

The "highest-leverage gaps" callout at the end of the assumption section identifies which markers, if resolved, unblock the most downstream work. These become the discovery-conversation agenda for the customer kickoff.

## Customer-specific overrides

Reserved format. Empty until a real engagement starts. Populated thereafter as customer-specific configuration emerges:

```
Customer: <name>
<module-specific configuration fields>
Per-process overrides (X.N: <override reason>)
ASSUMPTION resolutions (ASSUMPTION-X-NN: resolved as <answer>; source: <evidence>)
```

The format is intentionally per-module — different modules have different override surfaces. The Q card overrides tier conventions and allow-lists; the J card overrides PO-entry workflow and OTB representation; the T card overrides poll budgets and on-prem reachability.

## How this feeds the rest of Phase II

**Solution Map sharpening (W5).** Every L2 in a partial-coverage card identifies a sub-process where the cell is ★ Canary-native vs ◐ substrate-supplied. The functional decomposition can promote a cell from ◐ to ● if a workaround is found, or demote it if the gap is wider than first assumed. The Scorecard reflects the sharper view.

**Build budget input (W6 / Phase III scoping).** Count of L3s × estimated effort per L3 type yields a build budget per module. Substrate-supplied L3s are integration work (lower per-L3 cost); ★ Canary-native L3s are product work (higher per-L3 cost). The card's Executive Summary table is the source.

**Risk surface for the steering committee.** Assumption markers ranked by leverage become the steering committee's open-questions slide. "Here are the 12 things we're guessing about; here's the resolution path for each."

## How this feeds Phase III

**SDD per module.** Every L2 becomes an SDD section; every L3 becomes a sub-section or test case. The card's L4 pointer at the top of the framework names where the SDD will live.

**Contract test suite.** Every entry in the substrate contract registry becomes a test that runs against every registered POS adapter. Adding a third adapter requires it to pass all existing contract tests — the registry is the conformance bar.

**Onboarding runbook.** The customer-specific overrides format defines what the onboarding runbook captures. Per-tenant configuration follows the override structure.

## Worked-example proofs

Four cards prove the format generalizes across cell shapes. These should be the reference implementations any new card is patterned against:

| Card | Cell shape | Demonstrates |
|---|---|---|
| `canary-module-q-functional-decomposition.md` | ★ Canary native | The canonical example. Detection-shaped module with rich vertical configuration. Use as the template starting point. |
| `canary-module-t-functional-decomposition.md` | ● Full direct | Substrate-shaped module. Producer-side contract registry; multi-source ingress (poll + webhook); cross-cutting cross-module contracts. |
| `canary-module-r-functional-decomposition.md` | ● Full direct | Substrate-shaped module with privacy posture as a load-bearing L2. Demonstrates that some modules pin a cross-cutting concern as a process area, not a footnote. |
| `canary-module-j-functional-decomposition.md` | ◐ Partial | The hardest shape. Canary-native vs substrate-supplied vs bridge tagging is mandatory. Proves the format accommodates gap-shaped modules without compromise. |

When drafting a new module's card, start from the Q card if the new module is ★ Canary native, the T card if ● Full direct and read-only, the R card if ● Full direct with cross-cutting privacy/security concerns, or the J card if ◐ Partial.

## What this artifact does NOT do

- It does NOT replace the Solution Map. The L1 cell is set in the Solution Map and read here.
- It does NOT replace the SDD. L4 implementation detail belongs in SDDs, not in this card. The card stops at L3 user stories.
- It does NOT prescribe build sequence. Cycle planning happens in delivery specs, with the card as input.
- It does NOT capture customer commercial terms or pricing. Those live in W6 (Contract Negotiation).
- It does NOT capture vendor selection rationale. That's the Scorecard's job.

## Related

- `solution-map.md` — Phase II W1→W5 artifact; sets the L1 cell this card decomposes
- `../phase-2-select-and-implement.md` — Phase II overview and workstream sequencing
- `../phase-1-assess-and-design.md` — Phase I produces the inputs the To-Be Workshops translate into the Solution Map and these cards
- `../../proof-cases/specialty-smb-counterpoint-solution-map.md` — proof-case Solution Map; cells ●/◐/★/◯/✗ this artifact decomposes per module
- (worked-example proofs, in `Brain/wiki/`)
  - `canary-module-q-functional-decomposition.md` — ★ Canary native
  - `canary-module-t-functional-decomposition.md` — ● Full direct
  - `canary-module-r-functional-decomposition.md` — ● Full direct with privacy posture
  - `canary-module-j-functional-decomposition.md` — ◐ Partial
