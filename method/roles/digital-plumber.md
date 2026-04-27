---
classification: confidential
owner: GrowDirect LLC
type: role-playbook
nav_order: 83
---

# Role — Digital Plumber

Digital Plumbers wire a retailer's sources into the canonical runtime
data model. Given the source-to-canonical mapping produced by a Data
Detective, the Digital Plumber builds the integrations, schedules,
idempotency guarantees, and observability so the data flows
continuously and reliably.

## The mandate

A diagnostic reveals the prize. An architecture evaluation picks the
path. Neither produces value until data actually moves. Digital
Plumbers are what turns "we could connect this" into "this is
connected, it's running, and it hasn't broken for 30 days."

## What a Digital Plumber delivers

1. **Connector inventory.** Every source connected, with connection
   type (webhook, polling, batch SFTP, manual upload), authentication,
   refresh cadence, owner.
2. **Idempotency and dedup strategy.** For each connector, how
   replayed events, late-arriving data, and duplicate submissions are
   handled without corrupting the canonical model.
3. **Evidence chain.** Every row in the canonical model traceable
   back to a source event. Hash-chained where the compliance posture
   requires it.
4. **Observability.** Dashboard per connector (throughput, error
   rate, lag). Alerting on SLA breach.
5. **Runbook per connector.** What to do when the source system goes
   down, what to do when the schema changes, what to do when data
   stops flowing.

## How the role is trained

Digital Plumbers are agents (or human-agent pairs) trained through:

1. **Knowledge cards** for integration patterns — webhook-with-
   idempotency-key, poll-with-delta-tracking, batch-SFTP-with-
   manifest-file, event-sourced-with-replay.
2. **Memory chunking** on prior integrations — every connector built
   becomes a template with known edge cases encoded.
3. **Shadow-run discipline** — every new connector runs in shadow
   mode for 7+ days alongside the client's existing data flow
   before cutting over.

## Relationship to other roles

- **Data Detectives** ([[method/roles/data-detective]]) produce the
  source-to-canonical mapping the Plumber implements.
- **Architects** approve the connector's fit to the target
  architecture and sign off on the observability contract.
- **Engineers** implement the connector code (or delegate to
  agents running under Plumber supervision).
- **Writers** document the connector in the engagement's runbook.

## Anti-patterns

- **Wiring without idempotency.** The first duplicate or replayed
  event breaks the canonical model. Every connector starts with
  idempotency, not as a later hardening pass.
- **Connecting without observability.** A connector without
  monitoring is a connector that will silently fail and corrupt
  downstream analytics.
- **Skipping the shadow run.** Direct cutover from an old flow to a
  new connector is how you lose a week of data on a silent schema
  mismatch.
- **Treating the canonical model as optional.** Every source has
  quirks. Every source gets mapped through the canonical model
  anyway. If a source requires bypassing the model, that's a
  canonical-model gap, escalated to the Architect.

## Related

- [[method/roles/data-detective]]
- [[method/it-architecture-options]]
- [[cbm-v2/data-protection-and-governance]]
