---
classification: confidential
owner: GrowDirect LLC
type: method-overview
---

# KATZ Method — Overview

KATZ is GrowDirect's two-phase engagement model. It is how we diagnose
a retailer's operating state, define the target state, evaluate the
architectural options to get there, and execute against the chosen
path. It is designed for small-to-mid specialty retailers with an
online footprint — the segment that needs a real platform and doesn't
have one.

## The two phases

**Phase I — Assess & Design.** What is the retailer's operating
reality, what is the prize, and what target state is worth building
toward?

Ten workstreams run in parallel within Phase I, each producing its own
audit trail:

1. Executive Interviews
2. Field Visits (stores, DCs, customer-facing channels)
3. As-Is Workshops (per business domain)
4. Executive Visioning
5. Benchmarking
6. Balanced Scorecards
7. Quantitative Analysis (inventory, financial, operational)
8. Business Case
9. Presentations (steering committee cadence, final report)
10. Change Management

Phase I ends with a signed decision: proceed, specific vision, quantified
business case.

**Phase II — Select & Implement.** Given the decision from Phase I,
what's the right combination of systems and delivery plan?

Six workstreams run within Phase II:

1. To-Be Workshops (per domain)
2. RFP Package (what's being asked for)
3. RFP Responses (per vendor, structured consistently)
4. IT Architecture (target state, transition plan)
5. Scorecard and Shortlist (how vendors are compared)
6. Contract Negotiation (redlines, LSP/SI engagement, escrow)

Phase II ends with a signed vendor commitment and a funded
implementation plan.

## The discipline that makes it work

**Evidence first, recommendation second.** Every finding is anchored
to data. Every recommendation closes the loop from evidence to action.

**Compilation triad.** Raw source → compiled / merged → summarized.
Per interview, per store visit, per workshop. The individual files are
audit trail; the compilation is the thesis; the summary is what
decision-makers read.

**Per-domain parallel workshops.** Every business domain in scope gets
its own as-is and to-be workshop artifact. Rigid, on purpose — the
domain boundaries force coverage. No folding Pricing into Forecasting.

**Business case triad.** Benefits / Costs / NPV. Plus a traceability
artifact that maps solution components back to value opportunities.
Without the traceability, Phase II becomes untethered.

**Steering committee cadence.** Numbered, dated, marked Final. SC
presentations are the engagement's heartbeat. Every other artifact
feeds into a specific SC.

**Versioning and "Final" marking.** Documents are explicitly versioned.
The terminal version is marked `Final`. Draft and revision status is
part of the filename. No one wonders which is canonical.

## Two signature deliverables

KATZ ships two externally-branded methodology skills under
`plugins/consulting/`:

- **[[retail-diagnostic]]** — a 7-section retail diagnostic deck, the
  Phase I output in concentrated form.
- **[[it-architecture-options]]** — a multi-option architecture
  evaluation, the Phase II bridge from as-is to chosen path.

Both run against a structured client evidence pack (financials,
systems inventory, POS data, workshop notes) and produce pptx-native
deliverables in the style a board expects.

## Who runs the method

Per-role playbooks live in `method/roles/`. The two novel GrowDirect
roles — **Data Detective** (translates heterogeneous retailer data
into the canonical model) and **Digital Plumber** (wires the canonical
model into systems of record) — are what make a small, AI-augmented
team capable of engagement-grade delivery.

## What makes KATZ different

1. **Agent-native.** Phase I ingest, as-is analysis, Phase II option
   modeling — all scaffolded by agents running against the canonical
   retail data model.
2. **Platform-backed.** The same canonical model that anchors the
   diagnostic is the runtime model of Canary Retail. The engagement
   lands on a platform, not a deck.
3. **SMB-first.** The method compresses the Big-4-grade engagement
   into weeks for an SMB retailer, not months for a chain of thousands
   of stores.
4. **Productized.** The deliverables are skills, not consultants.
   They can be run repeatedly. They can be customized per vertical.
5. **Proof case on ourselves.** We run the diagnostic on our own
   platform. Every claim about how it works is grounded in how we
   built our own.

## Adoption

KATZ is the method GrowDirect uses for:
- External engagement work (SMB retailer onboarding to Canary Retail)
- Internal transformation moments (platform v2 moves, major vendor
  cutovers)
- Strategic decisions that would otherwise be ad-hoc (which module to
  productize next, which partnership to invest in)

The `engagement-template/` skeleton under `method/artifacts/` is the
cloneable starter kit for new engagements.

## Related

- [[method/retail-diagnostic]]
- [[method/it-architecture-options]]
- [[cbm-v2/overview]]
- [[about/growdirect-llc]]
