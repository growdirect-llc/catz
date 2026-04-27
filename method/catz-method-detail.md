---
classification: confidential
owner: GrowDirect LLC
type: method-detail
nav_order: 2
---

# CATz Method — Full Phase and Workstream Detail

The CATz Client Delivery Framework (CDF) is the operational backbone of every engagement. It organizes platform delivery into three sequential phases and five parallel workstreams, with defined entry criteria, exit gates, agent roles, human checkpoints, and artifacts at each stage.

This document is the full-detail reference. For the one-page summary, see [[method/overview]].

---

## The CDF Model

Three phases. Five workstreams. Every workstream runs across all three phases; the work shifts character in each phase — from design to build to validate.

```
             WS1           WS2            WS3           WS4           WS5
         Architecture   Data &         Analytics &   Knowledge &    Program
         & Infra        Integration    Detection     Enablement     Management
         ─────────────  ─────────────  ────────────  ────────────   ───────────
SCAFFOLD │ Design,       Source        Rule catalog  Brain seeding  Stakeholder
         │ provision,    inventory,    design,       plan, agent    kickoff,
         │ tenant setup  connector     threshold     training       milestone
         │               design        baseline      baseline       plan
         ─────────────  ─────────────  ────────────  ────────────   ───────────
SEED     │ Shadow run,   Connector     Historical    Knowledge      Mid-point
         │ scaling       build,        backfill,     card authoring, review,
         │ validation,   shadow mode,  rule tuning,  vault          risk
         │ hardening     canonical     dashboard     population     register
         │               population    configuration               update
         ─────────────  ─────────────  ────────────  ────────────   ───────────
SHOW     │ Cutover,      Live data     Activated     Enablement     Go-live
         │ monitoring,   confirmation, rules,        handoff,       sign-off,
         │ post-live     connector     validated     runbook        retrospective
         │ hardening     sign-off      baselines     delivery
```

---

## Phases

### Phase 1 — Scaffold

The Scaffold phase establishes the operating foundation before any live data touches the system. Nothing moves until architecture is decided, infrastructure is provisioned, data sources are inventoried, and the program cadence is running.

**Entry criteria**

- Phase I (Assess & Design) and Phase II (Select & Implement) are complete or the engagement is starting at implementation with a defined architecture decision already in hand.
- Cloud platform decision is documented (see [[method/cloud-architecture-options]]).
- Tenant identifier and database naming conventions are confirmed.
- Stakeholder list and steering committee cadence are agreed.

**Key activities per workstream**

| Workstream | Activities |
|---|---|
| WS1 — Architecture & Infra | Cloud account provisioning, VPC/network setup, DNS allocation, tenant database creation, Valkey namespace assignment, container registry, secrets management, TLS configuration. |
| WS2 — Data & Integration | Source system inventory (POS, back-office, spreadsheets), connector design per source, shadow-mode scaffolding, authentication setup (OAuth tokens, API keys, SFTP credentials). |
| WS3 — Analytics & Detection | Rule catalog design for tenant vertical, threshold baseline from industry benchmarks, dashboard layout design, alert routing configuration (email, Slack, webhook). |
| WS4 — Knowledge & Enablement | Brain vault seeding: retailer entity cards, location profiles, employee roster baseline. Agent training corpus scoped. Enablement plan drafted. |
| WS5 — Program Management | Kickoff session, milestone plan published (Scaffold/Seed/Show dates), RACI agreed, risk register initialized, steering committee #1 scheduled. |

**Agents active**

- Architect (WS1 lead, WS2/WS3 input)
- Data Detective (WS2 lead, WS4 support)
- PMO (WS5 lead, cross-workstream coordination)

**Human checkpoints**

1. Architecture sign-off: cloud platform, tenant model, and network topology confirmed before provisioning.
2. Stakeholder kick-off: SC#1 delivered, milestone plan accepted.

**Exit criteria**

- Infrastructure is provisioned and passes health checks.
- All source systems are inventoried; connector designs are reviewed.
- Rule catalog baseline is drafted and reviewed by the LP lead.
- SC#1 delivered; proceed decision confirmed.
- Risk register has at least one entry per workstream.

**Artifacts produced**

| Artifact | Owner | Path |
|---|---|---|
| Cloud architecture decision | Architect | `docs/engagements/<tenant>/arch-decision.md` |
| Source inventory | Data Detective | `docs/engagements/<tenant>/source-inventory.md` |
| Connector design specs | Data Detective + Digital Plumber | `docs/engagements/<tenant>/connectors/` |
| Rule catalog baseline | Architect | `docs/engagements/<tenant>/rule-catalog-baseline.md` |
| Milestone plan | PMO | `docs/engagements/<tenant>/milestone-plan.md` |
| SC#1 presentation | PMO + Writer | `docs/engagements/<tenant>/steering/sc-01-final.pptx` |

---

### Phase 2 — Seed

The Seed phase builds out the integration layer, populates the canonical data model with historical data, tunes detection rules against real data, and trains the agents. No go-live happens until the Seed phase has produced stable baselines.

**Entry criteria**

- Scaffold phase exit criteria are met.
- Cloud infrastructure passes connectivity checks from all source systems.
- Connectors are designed and development environments are available.
- Rule catalog baseline is approved.

**Key activities per workstream**

| Workstream | Activities |
|---|---|
| WS1 — Architecture & Infra | Shadow-run monitoring, scaling tests against expected transaction volume, backup/restore validation, security posture review (access logs, key rotation, network ACLs). |
| WS2 — Data & Integration | Connector build per source, shadow mode operation (minimum 7 days alongside existing data flow), canonical model population with historical data (PCI minimum 12 months; LP audit trail 36 months preferred), idempotency and dedup validation. |
| WS3 — Analytics & Detection | Historical backfill drives rule calibration — detection thresholds tuned against actual transaction patterns, dashboard populated with baseline KPIs, false-positive rate reviewed and brought within acceptable range. |
| WS4 — Knowledge & Enablement | Knowledge card authoring (one card per location, one card per key employee group), vault population with operating context, agent memory chunked against canonical model, enablement materials drafted. |
| WS5 — Program Management | Mid-point review (SC#2), risk register updated, any Scaffold phase issues formally closed or escalated, go-live readiness checklist drafted. |

**Agents active**

- Digital Plumber (WS2 lead — connector build and shadow mode)
- Data Detective (WS2 support — canonical model validation)
- Architect (WS1 and WS3 review)
- Writer (WS4 lead)
- PMO (WS5 lead)

**Human checkpoints**

1. Shadow mode sign-off: Digital Plumber and LP lead confirm shadow run output matches expectations before canonical model write begins.
2. Rule calibration review: LP lead reviews false-positive rate against threshold.
3. SC#2 (mid-point review): stakeholders confirm go-live readiness trajectory.

**Exit criteria**

- All connectors operating in shadow mode for ≥7 days with no data loss or duplication.
- Canonical model populated: ≥12 months of historical transaction data loaded and validated.
- Detection rules tuned: false-positive rate below agreed threshold (typically <5% of alerts requiring dismissal without action).
- Dashboard baseline KPIs are populated and reviewed.
- Knowledge vault has at minimum: retailer entity card, location profiles, employee roster baseline, and one vertical context card.
- Go-live readiness checklist is complete (no P1 items open).

**Artifacts produced**

| Artifact | Owner | Path |
|---|---|---|
| Connector runbooks (one per source) | Digital Plumber | `docs/engagements/<tenant>/connectors/<source>-runbook.md` |
| Shadow mode report | Digital Plumber | `docs/engagements/<tenant>/shadow-mode-report.md` |
| Rule calibration log | Architect | `docs/engagements/<tenant>/rule-calibration.md` |
| Historical backfill report | Data Detective | `docs/engagements/<tenant>/backfill-report.md` |
| Go-live readiness checklist | PMO | `docs/engagements/<tenant>/go-live-readiness.md` |
| SC#2 presentation | PMO + Writer | `docs/engagements/<tenant>/steering/sc-02-final.pptx` |

---

### Phase 3 — Show

The Show phase cuts live. Data flows through production connectors. Detection rules fire against real transactions. The retailer's LP and operations teams use the platform. The engagement closes when the value is visible and the handoff is complete.

**Entry criteria**

- Seed phase exit criteria are met.
- Go-live readiness checklist: all P1/P2 items closed.
- Retailer stakeholders have completed onboarding session.
- Monitoring dashboards active and alerts routing correctly.

**Key activities per workstream**

| Workstream | Activities |
|---|---|
| WS1 — Architecture & Infra | Cutover from shadow to live connectors, production monitoring live (throughput, error rate, latency), incident response runbook tested, post-live hardening pass (30-day). |
| WS2 — Data & Integration | Live connector sign-off (first 48–72 hours under active monitoring), dedup / replay edge cases confirmed, connector SLAs agreed and monitored. |
| WS3 — Analytics & Detection | First-week alert validation (LP lead reviews every alert for first 5 business days), rule adjustments applied where needed, baseline KPIs locked and reported to SC. |
| WS4 — Knowledge & Enablement | Enablement sessions delivered (LP team, operations leads), handoff package produced, vault finalized, agent memory confirmed. |
| WS5 — Program Management | Go-live sign-off ceremony (SC#3, final report), retrospective, issue log closed, transition to steady-state support model documented. |

**Agents active**

- Digital Plumber (WS2 — live monitoring, incident response)
- Architect (WS1 and WS3 review)
- Writer (WS4 — enablement delivery)
- PMO (WS5 — go-live coordination, SC#3)

**Human checkpoints**

1. Cutover authorization: founder/engagement lead + LP director sign off before shadow connectors go live.
2. First-week LP review: alert quality validated in person with LP team.
3. SC#3 (final): engagement closed, steady-state handoff confirmed.

**Exit criteria**

- Production connectors live and stable for ≥5 business days.
- First-week alert validation complete; false-positive rate confirmed within range.
- Enablement session delivered; LP team can operate the platform unassisted.
- Handoff package complete (runbooks, alert tuning guide, support contacts).
- SC#3 final report delivered and accepted.
- Retrospective notes filed.

**Artifacts produced**

| Artifact | Owner | Path |
|---|---|---|
| Go-live sign-off memo | PMO | `docs/engagements/<tenant>/go-live-signoff.md` |
| Steady-state support model | Architect + PMO | `docs/engagements/<tenant>/support-model.md` |
| Enablement handoff package | Writer | `docs/engagements/<tenant>/enablement/` |
| Retrospective notes | PMO | `docs/engagements/<tenant>/retro.md` |
| SC#3 final report | PMO + Writer | `docs/engagements/<tenant>/steering/sc-03-final.pptx` |

---

## Workstreams — Swim-Lane Narratives

### WS1 — Architecture & Infrastructure

**Purpose.** Every other workstream depends on WS1. Nothing flows, no data is analyzed, no detection fires until the infrastructure is provisioned, secured, and confirmed stable.

**Scaffold.** The Architect makes the cloud platform decision (see [[method/cloud-architecture-options]]). Tenant database is provisioned: isolated PostgreSQL instance, pgvector extension enabled, Valkey namespace allocated. Container registry and secrets management configured. Network topology reviewed: VPC, security groups, ingress/egress rules. DNS allocated. TLS configured end to end. Decision gate: architecture sign-off before any connector targets the database.

**Seed.** Shadow-mode traffic tests infrastructure under realistic load. Backup and restore validation confirms recovery posture. Security review: access logs audited, key rotation tested, network ACLs confirmed. Scaling headroom estimated against transaction volume projections for the tenant's store count.

**Show.** Cutover to live connectors under active monitoring. Post-live hardening pass: any issues surfaced by production traffic resolved within 30 days. Steady-state monitoring thresholds locked (CPU, memory, connection pool, query latency). Incident response runbook tested.

**Handoffs to:** WS2 (database and Valkey ready), WS3 (dashboards can be served), WS5 (infrastructure milestones drive milestone plan).

**Decision gate.** Architecture sign-off at Scaffold exit. No connector wiring starts until WS1 confirms the environment is ready.

---

### WS2 — Data & Integration

**Purpose.** The canonical retail data model is only as useful as the data flowing into it. WS2 is how the source systems — POS, back-office, inventory, HR — become the continuous feed the rest of the platform depends on.

**Scaffold.** Data Detective produces the source inventory: every system, every spreadsheet, every manual process that holds data the platform needs. For each source: format, custodian, refresh cadence, access method, known gaps. Connector design documented for each source (authentication, integration pattern, idempotency key, retry strategy).

**Seed.** Digital Plumber builds each connector. Shadow mode for minimum 7 days alongside the source system's existing data flow — output compared, dedup validated, late-arriving event handling confirmed. Historical backfill runs: ≥12 months of transaction data loaded into the canonical model. Gap register updated with any sources that couldn't be connected or had incomplete history.

**Show.** Shadow connectors cut to live. First 48–72 hours monitored actively: throughput, error rate, lag. LP lead reviews first-week alert output for connector-related anomalies. Connector SLAs agreed and baseline established. Runbook per connector finalized.

**Handoffs to:** WS1 (connector infrastructure requirements), WS3 (canonical data drives rule evaluation), WS4 (source entities drive vault population).

**Decision gate.** Shadow mode sign-off before canonical model population begins. No historical backfill until shadow output validates correctly.

---

### WS3 — Analytics & Detection

**Purpose.** Data in the canonical model is necessary but not sufficient. WS3 configures what the platform does with it: detection rules, alert thresholds, dashboards, and the intelligence layer.

**Scaffold.** Rule catalog designed for the tenant's vertical (retail category, store format, transaction patterns). Threshold baselines drawn from industry benchmarks rather than live data — these will be replaced by data-driven calibration during Seed. Dashboard layout designed: which KPIs, which alert categories, which time horizons.

**Seed.** Historical backfill enables data-driven calibration. Rule thresholds tuned against actual transaction patterns for this tenant. False-positive rate measured and iterated against agreed target. Dashboard populated: baseline KPIs calculated from historical data, trend lines established. Alert routing configured and tested.

**Show.** Rules active against live data. First-week alert validation: LP lead reviews every alert for 5 business days, annotating true positives and dismissals. Rule adjustments applied in real time based on this review. Alert quality confirmed. Baseline KPIs locked for ongoing tracking.

**Handoffs to:** WS2 (detection depends on canonical model completeness), WS4 (alert outputs feed agent knowledge), WS5 (detection results drive SC reporting).

**Decision gate.** Rule calibration review before go-live: false-positive rate above threshold blocks Show phase entry.

---

### WS4 — Knowledge & Enablement

**Purpose.** The platform operates best when it has context about the retailer. WS4 populates the vault, trains the agents, and ensures the human team can operate the platform unassisted after the engagement ends.

**Scaffold.** Brain vault seeding plan documented. Retailer entity cards drafted: company profile, store locations, operating model, key personnel, known risks and patterns. Agent training corpus scoped: what knowledge should the agents have at go-live?

**Seed.** Knowledge cards authored and loaded: one card per location (format, staff profile, transaction patterns, known shrinkage context), employee group profiles, vertical context (what does normal look like in this product category?). Vault populated. Agent memory chunked against canonical model — the agents can answer retailer-specific questions from day one. Enablement materials drafted: alert tuning guide, platform walkthrough, FAQ.

**Show.** Enablement sessions delivered to LP team and operations leads. Vault finalized: any gaps from the engagement resolved. Handoff package produced: runbooks, alert tuning guide, vault access guide, support contacts. Agent memory confirmed stable.

**Handoffs to:** WS2 (source entities inform vault structure), WS3 (alert taxonomy drives agent training), WS5 (enablement completion is a go-live gate).

**Decision gate.** Vault minimum viable: entity card, location profiles, employee roster, vertical context card — all required before Show entry.

---

### WS5 — Program Management

**Purpose.** CATz engagements have a defined structure. WS5 is what keeps all five workstreams on track, surfaces risks before they become problems, and provides the stakeholder interface through which the engagement is governed.

**Scaffold.** Kickoff session. Stakeholder list confirmed. Milestone plan published: Scaffold/Seed/Show target dates, key gates, and owner assignments. RACI agreed. SC#1 delivered. Risk register initialized.

**Seed.** Mid-point review (SC#2): all workstream leads report status, risk register updated, any Scaffold phase issues formally closed or escalated. Go-live readiness checklist drafted and tracking. Schedule compression options identified if the engagement is at risk.

**Show.** Go-live sign-off (SC#3): all exit criteria confirmed, final report delivered. Retrospective session: what went well, what would be done differently, lessons for the next engagement. Steady-state support model documented and agreed. Engagement formally closed.

**Handoffs to:** All workstreams (WS5 coordinates cadence and escalation across all). Owner of every gate.

---

## RACI Matrix

Rows are workstreams. Columns are roles. Cells show R/A/C/I per phase (Scaffold / Seed / Show).

R = Responsible (does the work), A = Accountable (owns the outcome), C = Consulted (input required), I = Informed (kept up to date).

| Workstream | Architect | Digital Plumber | Data Detective | Writer | PMO |
|---|---|---|---|---|---|
| **WS1 — Architecture & Infra** | | | | | |
| Scaffold | R/A | I | I | I | C |
| Seed | R/A | C | I | I | C |
| Show | R/A | C | I | I | C |
| **WS2 — Data & Integration** | | | | | |
| Scaffold | C | C | R/A | I | I |
| Seed | C | R/A | C | I | I |
| Show | C | R/A | C | I | I |
| **WS3 — Analytics & Detection** | | | | | |
| Scaffold | R/A | I | C | I | I |
| Seed | R/A | C | C | I | I |
| Show | A | C | C | I | I |
| **WS4 — Knowledge & Enablement** | | | | | |
| Scaffold | C | I | R | A | C |
| Seed | C | I | C | R/A | I |
| Show | C | I | C | R/A | I |
| **WS5 — Program Management** | | | | | |
| Scaffold | C | I | I | C | R/A |
| Seed | C | C | C | C | R/A |
| Show | C | C | C | C | R/A |

**Notes on accountability splits.** For WS3 in the Show phase, the Architect is accountable (the rules are an architectural decision) but the LP lead within the retailer is the operational owner of alert quality review. This is the one point where external accountability sits outside the CATz team. Make this explicit in the RACI conversation with the client.

---

## What Can Go Wrong — Risk Register by Phase

### Scaffold Phase Risks

**1. Cloud platform decision deferred too long.**
The Scaffold phase can't complete without a platform decision. Teams that attempt to scaffold before the architecture is decided end up reprovisioning infrastructure. Mitigation: architecture decision is a *Scaffold entry criterion*, not a task to be completed during Scaffold. If it's not decided, Scaffold has not started.

**2. Source system access blocked or undocumented.**
"We'll get you access to the POS" is not access. Retailers routinely underestimate how difficult it is to obtain API credentials, SFTP access, or system-level exports from legacy or managed systems. Mitigation: Data Detective runs source inventory in week 1 and flags access blockers immediately. Any source with access risk escalated to PMO within 48 hours of discovery.

**3. Stakeholder misalignment on scope.**
The kickoff session uncovers that different stakeholders have different ideas of what the engagement delivers. If SC#1 doesn't surface this, it surfaces in Seed when missed scope becomes visible. Mitigation: SC#1 agenda explicitly surfaces scope commitments. RACI is reviewed out loud. Any scope ambiguity documented as a risk.

---

### Seed Phase Risks

**1. Shadow mode reveals canonical model gaps.**
The source system exports data in a shape that doesn't map cleanly to the canonical model. This surfaces in shadow mode — it's supposed to. The risk is that the gap is larger than expected and the backfill timeline is inadequate. Mitigation: shadow mode output is reviewed at day 3 (not day 7). Early review catches major gaps with time to remediate. Gap register updated immediately.

**2. Historical data is incomplete or inconsistent.**
A retailer on an old POS system may have 10 years of data in their system and 3 years of usable data. Schema changes, data migration, system replacements, and manual interventions create discontinuities. Mitigation: Data Detective reviews data completeness before committing to backfill scope. Partial backfill with explicit gap register is better than a silent omission.

**3. Rule calibration takes longer than planned.**
Detection thresholds that work for one transaction pattern may produce unacceptable false-positive rates for another. Specialty retailers with unusual transaction patterns (garden centers, liquor stores, high-value items) often require more calibration iterations. Mitigation: rule calibration timeline is padded for vertical-specific engagements. LP lead availability for calibration review is confirmed before Seed begins.

---

### Show Phase Risks

**1. First-week alert volume overwhelms the LP team.**
Going live on a platform that fires 200 alerts in week one — most of them for uncalibrated rules — destroys adoption. Mitigation: first-week LP lead review is a mandatory gate, not an optional best practice. Alert volume is monitored daily and rules are adjusted in real time.

**2. Connector incident post-cutover.**
A source system changes its schema, API contract, or authentication method after cutover. This is a when, not an if, for any long-running engagement. Mitigation: connector runbooks include schema change response procedures. Digital Plumber is on active watch for the first 5 business days. Canary monitoring alerts on connector health in real time.

**3. Enablement handoff incomplete.**
The LP team can't operate the platform unassisted because the enablement sessions were rushed or the documentation was thin. Mitigation: enablement minimum viable content is a *Show entry criterion* — if WS4 hasn't delivered the core materials, Show doesn't start. Enablement is not an afterthought; it's a gate.

---

## Related

- [[method/overview]] — one-page method summary
- [[method/cloud-architecture-options]] — where the platform runs
- [[method/data-economics]] — data economics and own-your-data positioning
- [[method/roles/architect]]
- [[method/roles/digital-plumber]]
- [[method/roles/data-detective]]
- [[cbm-v2/pmo]]
