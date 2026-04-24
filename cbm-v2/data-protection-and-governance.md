---
classification: confidential
owner: GrowDirect LLC
type: cbm-cell
---

# CBM v2 Cell — Data Protection & Governance

Data Protection & Governance is the operational discipline around
every piece of PII, payment credential, and evidence record that
flows through a Canary Retail deployment or a CATz engagement.

## Why this is a cell

Classical retail CBMs assigned this work to "Technology" or
"Legal." Neither works:

- **Under Technology.** Data protection becomes a code problem,
  and it gets implemented once, then drifts. The next module
  re-implements incomplete.
- **Under Legal.** Data protection becomes a compliance problem,
  and it gets audited annually instead of operated continuously.

DP&G is operational. It owns daily posture: who can read what,
when data expires, what incident response looks like, how a
right-to-delete request flows. Every module and every engagement
operates within DP&G boundaries.

## Scope

### PII inventory

Every table, every column that carries personally identifiable
information, tagged at schema-definition time. Generated inventory
is auditable and diff-trackable. New PII fields require explicit
DP&G sign-off before merging.

### Payment-credential handling

Canary Retail's posture is "stay out of PCI scope by design." Card
data tokenizes at the payment processor; Canary sees only
tokens and reconciled results. This posture is enforced at code-
review time and verified by the automated security audit.

### Hash-chain evidence

Transaction intake, case evidence, alert disposition — all hash-
chained from ingestion onward. Evidence chain is
cryptographically verifiable, append-only, and signed per-merchant.

### Retention policy

Per-category retention:

| Category | Default retention | Rationale |
|---|---|---|
| Transaction records | 7 years | Financial audit baseline |
| Session records | 30 days | Operational analytics |
| Alert + case records | 7 years | LP retention baseline |
| Agent session memories | 90 days | Recall window; aggregated beyond |
| PII audit log | 7 years | Compliance |

Per-tenant overrides are supported; baseline is the default.

### Right-to-delete

Every PII field carries a deletion path. A right-to-delete request
triggers a cascade that redacts or tombstones records across
app / sales / metrics schemas. Deletion is logged for audit.

### Data residency

Canary Retail's production deploys in a single AWS region by
default (US). Tenants requiring EU residency get their own
region-isolated deployment; cross-region data flow is prohibited.

### Breach response

The founder has personally executed breach response in prior
executive roles. The breach-response playbook covers: detection,
containment, notification timeline per jurisdiction, forensic
evidence preservation, customer communication.

## Compliance posture

| Standard | Current state | Roadmap |
|---|---|---|
| ISO 27001 | Aligned; not certified | Formal certification year 2 |
| SOC II (Type II) | Aligned; not certified | Formal certification year 2 |
| PCI DSS | Out-of-scope by design | Annual AOC attestation |
| GDPR | Operational | Formal DPO engagement on first EU tenant |
| CCPA | Operational | |

"Aligned" means the controls are implemented; "certified" means a
third-party audit has verified them. The roadmap is realistic; the
aligned state is defensible today.

## Cross-cell relationships

- With **Agent Strategy**: every agent that touches PII operates
  within DP&G boundaries.
- With **PMO**: DP&G sign-off is a stage gate for any module
  handling new PII.
- With **ARB**: DP&G holds veto power on architectural decisions
  that weaken data posture.

## Related

- [[overview]]
- [[agent-strategy]]
- [[pmo]]
- [[arb]]
- [[../standards/README]]
