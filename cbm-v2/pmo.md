---
classification: confidential
owner: GrowDirect LLC
type: cbm-cell
---

# CBM v2 Cell — PMO

Program Management Office. Owns the cadence, the dispatch pattern,
the factory pipeline, and the cross-workstream coordination. In a
classical retail CBM, PMO shows up during transformation
engagements and disappears after. In GrowDirect's platform-company
operating model, PMO is permanent.

## Why this is a cell

Without a permanent PMO function, cross-workstream coordination
falls to the founder. That doesn't scale past one project.

The moment GrowDirect runs two concurrent workstreams (e.g., a
customer engagement and a product release; a methodology sprint
and a code sprint), the PMO cell is what keeps them from
colliding.

## Scope

### Sprint methodology

Two-week sprints with defined factory stages: Blueprint → Parts →
Assembly → QC → Packaging → Ship. Every sprint has a named
deliverable, a factory-stage checklist, and a completeness gate
before the next sprint starts.

### Factory pipeline

SDD → memory chunking → wiki narration → code implementation. Every
stage feeds the next. Every stage is traceable. Drift between
stages surfaces as a finding in the QC stage.

### Dispatch pattern

The dispatch is the unit of cross-session coordination.

- A dispatch is produced by a strategy / brainstorm session.
- A dispatch is consumed by an execution session.
- Every dispatch has: context, decisions made, streams of work,
  acceptance criteria, out-of-scope list, executor handoff notes.
- Dispatches are committed to the repo under `dispatches/` as the
  durable record.

Example: the 2026-04-24 platform-brand consolidation dispatch
(`dispatches/dispatch-platform-brand-consolidation-2026-04.md`)
produced by a strategy session; executed by a subsequent Claude
Code session; artifact-trail visible in both session logs and in
the resulting commits.

### Release trains

Planned, named, dated releases. Every release has:

- A theme (what gets shipped)
- A pre-flight checklist (what needs to be true before cutover)
- A cutover window
- A rollback plan
- A post-release verification checklist

### Cross-workstream coordination

Weekly stand-up (founder + active agents). Blockers surfaced.
Cross-workstream dependencies tracked. Timelines adjusted.

### Ticket hygiene

Linear is the system of record for work tickets (GRO-prefixed
issues). Every commit references the ticket it closes. Every
dispatch references the initiative or issue it produces.

### Metrics

- Sprint-cycle velocity (story points or counted deliverables per
  sprint)
- Dispatch-to-execution lag (how long between strategy output and
  execution start)
- Factory-stage drift (how often stages disagree)
- Release cadence (planned vs actual)

## Cross-cell relationships

- With **ARB**: PMO brings architectural decisions to ARB; ARB
  outcomes flow back into the sprint plan.
- With **Data Protection & Governance**: DP&G sign-off is a sprint
  stage gate for modules handling PII.
- With **Agent Strategy**: PMO tracks the agent roster as part of
  capacity.

## Related

- [[overview]]
- [[arb]]
- [[../method/overview]]
