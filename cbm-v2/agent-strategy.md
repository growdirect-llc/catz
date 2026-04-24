---
classification: confidential
owner: GrowDirect LLC
type: cbm-cell
---

# CBM v2 Cell — Agent Strategy

The AI-agent workforce is a first-class function in GrowDirect's
operating model. It has a roster, a governance layer, a memory
infrastructure, and a distinction between customer-facing agents
and delivery agents.

## Why this is a cell

Pre-2025 CBMs placed "IT tooling" under the Technology cell. Agents
aren't tooling — they're labor. They do work, produce artifacts,
collaborate with humans, and need governance. The moment agents
become load-bearing, they earn their own cell.

## Agent populations

### Customer-facing agents

Agents that Canary Retail operates on behalf of a merchant, visible
to the merchant's end users or operators.

- Chirp rule-evaluation agents (detection pipeline)
- Fox case-management agents (case triage, evidence collation)
- Owl search agents (natural-language retrieval over the merchant's
  canonical data)
- RaaS namespace-resolution agents (principal identification across
  the MCP mesh)

### Delivery agents

Agents that run alongside the KATZ delivery team during an
engagement. Not visible to the merchant as "agents"; they appear as
the delivery team's capability.

- Data Detective ([[../method/roles/data-detective]]) — source-to-
  canonical translation
- Digital Plumber ([[../method/roles/digital-plumber]]) — integration
  wiring
- Architect ([[../method/roles/architect]]) — target architecture
  production (planned)
- Writer ([[../method/roles/writer]]) — engagement documentation
  (planned)

### Platform agents

Agents that keep the platform running, not visible to merchants or
engagement teams directly.

- Memory-bus indexer
- Embeddings-rebuild scheduler
- Skill registry validator
- Atlas knowledge-graph maintainer

## Memory-bus architecture

Every agent reads from and contributes to a shared memory bus
backed by pgvector. The memory bus carries three kinds of content:

1. **Curated knowledge cards** — structured method fragments,
   data-shape patterns, integration patterns. Written by humans,
   read by agents.
2. **Session memories** — per-merchant, per-tenant, per-agent
   recall over prior sessions. Produced by agents, consumed by
   successor agents.
3. **Decision records** — architectural decisions, disposition
   calls, judgment-call resolutions. Authored by humans, recalled
   by agents when context matches.

Every memory chunk carries principal scoping. A delivery agent for
one engagement cannot recall memories belonging to another
engagement unless the partner explicitly cross-shared.

## Principal-awareness — a hard requirement

Every agent in the GrowDirect mesh knows:

- Its own identity (which agent, which version).
- Its principal (whose authority it is acting under — the merchant
  tenant for customer-facing agents; the engagement team for
  delivery agents).
- Its authority scope (which MCP tools, which data, which actions
  it is authorized to invoke).
- Its audit trail (every action is hash-chained for evidence).

Agents that don't know their principal get exploited in an open-
agent world. Principal-awareness is a security property, not a
convenience.

## Agent SDD template

Every production agent has an SDD covering:

- Purpose and scope
- Principal and authority boundaries
- Tools and data sources it reads / writes
- Memory bus interaction (reads what, writes what, retention policy)
- Failure modes and escalation paths
- Versioning and rollback
- Audit footprint

The template lives at `method/artifacts/agent-sdd-template.md` (to
be populated).

## Cross-cell relationships

- With **Data Protection & Governance**: agents carry PII in their
  context windows; PII handling flows through the DP&G cell.
- With **PMO**: the agent roster is part of the capacity model.
- With **ARB**: every agent addition or authority expansion is an
  ADR.

## Related

- [[overview]]
- [[data-protection-and-governance]]
- [[arb]]
- [[../method/roles/data-detective]]
- [[../method/roles/digital-plumber]]
