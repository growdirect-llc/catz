---
classification: confidential
owner: GrowDirect LLC
type: cbm-cell
---

# CBM v2 Cell — Architecture Review Board (ARB)

The ARB is the cross-module architectural authority. It owns
Architecture Decision Records (ADRs), design review, technical-debt
governance, and architectural consistency across the module spine.

## Why this is a cell

Without an explicit ARB, architectural decisions get made in pull
requests by whichever agent is active. Consistency drifts. Technical
debt compounds invisibly. Cross-module integration breaks because
no one owned the boundary definition.

ARB is the governance layer that prevents that drift. In a solo-
founder platform company, ARB is the founder plus delegated agents
operating under explicit review protocols.

## Scope

### ADRs

Every architectural decision with cross-module impact produces an
ADR. Template covers:

- Context (what's being decided and why now)
- Decision (what's chosen)
- Consequences (what becomes easier, what becomes harder)
- Alternatives considered (why the chosen option beats them)
- Status (proposed / accepted / superseded)

ADRs live at `docs/decisions/ADR-<domain>-<nnn>_<title>.md` in the
Canary repo.

### Design review

New modules, new integrations, and new cross-module interfaces go
through design review before implementation starts. Review covers:

- Fit to target architecture
- CRDM compatibility
- Security posture (via DP&G cell)
- Performance implications
- Integration surface
- Test strategy
- Operational observability

### Technical-debt governance

Known debt is catalogued. Every piece of debt has:

- Description
- Severity (blocks scaling / degrades quality / nice-to-fix)
- Ownership (which module)
- Repayment plan (sprint, quarter, or "never")

The ARB reviews the debt register quarterly and adjusts priorities.

### Boundary definition

Module boundaries are ARB-defined. Which responsibilities belong
to C vs F vs J. Where commercial ends and merchandising begins.
How the detection engine (Q) interacts with work execution (W).
Boundaries are documented; boundary violations are findings.

### Authority veto

ARB has veto authority over architectural decisions that would:

- Break CRDM compatibility
- Weaken multi-tenancy
- Introduce un-bounded operational cost
- Violate DP&G posture
- Create a module boundary that can't be maintained

Veto is rare; its existence matters more than its use.

## Review cadence

- Per-sprint: quick architectural check on new work during sprint
  planning (15 min)
- Per-release: design review for any new module or major change
  (30–60 min)
- Per-quarter: technical-debt review (60 min), cross-module
  consistency check (60 min)

## ADR catalog (current)

A running list of accepted ADRs lives at
`docs/decisions/INDEX.md` in the Canary repo. As of Q2 2026:

- ADR-PLA-001 — Presentation Layer Architecture (four-layer:
  Functional Blueprint + Theme + Locale + Vocabulary)
- ADR-001 — Multi-Tenant Partition Architecture (historical;
  superseded)
- (Additional ADRs added as architectural decisions are made)

## Cross-cell relationships

- With **PMO**: ARB outcomes drive sprint planning.
- With **Agent Strategy**: every agent authority change is an ADR.
- With **Data Protection & Governance**: DP&G posture changes go
  through ARB.

## Related

- [[overview]]
- [[pmo]]
- [[agent-strategy]]
- [[../method/artifacts/sdd-template]]
