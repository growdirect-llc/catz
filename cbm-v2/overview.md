---
classification: confidential
owner: GrowDirect LLC
type: capability-model
---

# CBM v2 — Retail Capability Model, GrowDirect Extensions

Standard retail Component Business Models cover the classical
dimensions of a retail operation: commercial, supply chain, finance,
store operations, space/range/display, pricing/promotion,
forecasting/ordering, people/labor, property/assets, loss prevention,
technology. They are domain-complete and still useful.

CBM v2 is GrowDirect's extension of that frame. It adds four cells
that the classical models were written too early to include, or that
every consultancy assumed happens "off to the side." In a
platform-company operating model — especially one running on
AI-agent labor — those four cells are first-class.

## The four extensions

| Cell | What it owns | Why it's v2 |
|---|---|---|
| **Agent Strategy** | The AI-agent workforce. Customer-facing agents, delivery agents, knowledge-detective agents. Agent roster, agent SDD templates, memory-bus architecture, agent-to-role mapping. | CBMs pre-2025 assumed humans in every cell. The agent workforce is not "IT tooling" — it's labor, and it belongs as its own function. |
| **Data Protection & Governance** | PII inventory, hash-chain evidence, PCI/GDPR/CCPA posture, audit trail, retention policy, right-to-delete, data residency, encryption-at-rest key management. | Classical CBMs put this under "Technology" or "Legal." Neither works: it's operational. |
| **PMO** | Sprint methodology, factory pipeline, release trains, dispatch pattern, cross-workstream coordination. | Retail CBMs name "Programme Management" as a cell in transformation engagements but drop it once the engagement ends. A platform company needs a permanent PMO function. |
| **ARB** | Architecture Decision Records, design review, cross-module architecture authority, technical-debt governance. | Same problem: retail CBMs reference "Architecture" as a role, not a governance cell. |

## Why these four and not others

The test: would a GrowDirect engagement fail if this cell wasn't
explicitly owned? For each of the four above, the answer is yes:

- **Agent Strategy.** Without explicit ownership, agents become
  "whoever set them up last." Memory drifts. Handoffs break.
  Capability proliferates without curation.
- **Data Protection & Governance.** Without explicit ownership,
  PCI / PII / GDPR become incident-response problems rather than
  operating disciplines. By the time there's an incident, it's
  already too late.
- **PMO.** Without explicit ownership, cross-workstream
  coordination falls to the founder. That doesn't scale past
  one project.
- **ARB.** Without explicit ownership, architectural decisions get
  made in PRs by whichever agent is active. Consistency drifts.
  Technical debt compounds invisibly.

Cells that are NOT in v2 but that others might propose — Marketing,
Legal, Finance-as-cell, Vendor Management — failed the test. They
exist in the operating model, but they're either already owned
by classical CBM cells or they're so small in an SMB-facing platform
company that they don't need their own governance yet.

## How the cells relate

The four v2 cells cut ACROSS the classical cells:

```
                 ┌─────────────── Agent Strategy ────────────────┐
                 │                                                │
    ┌─────────────────────── Data Protection & Governance ─────────────────────────┐
    │                                                                                │
    │   Commercial │ Supply Chain │ Finance │ Store Ops │ SRD │ Pricing │ ...       │
    │                                                                                │
    └────────────────────────────────── PMO ────────────────────────────────────────┘
                 │                                                │
                 └────────────── ARB ────────────────────────────┘
```

Every classical cell has an agent population (Agent Strategy), a
data-protection posture (Data Protection & Governance), a delivery
cadence (PMO), and architectural boundaries (ARB). The v2 cells are
the governance over the classical cells.

## Per-cell deep-dives

- [[cbm-v2/agent-strategy]] — agent roster, SDD template, memory bus
- [[cbm-v2/data-protection-and-governance]] — PII map, hash-chain,
  compliance posture
- [[cbm-v2/pmo]] — sprint methodology, factory pipeline, dispatch
  pattern
- [[cbm-v2/arb]] — ADR governance, design review, tech-debt policy

## Related

- [[method/overview]]
- [[method/roles/architect]]
- [[method/roles/data-detective]]
