---
classification: confidential
owner: GrowDirect LLC
type: method-reference
skill: plugins/consulting/skills/it-architecture-options/SKILL.md
nav_order: 4
---

# Method — IT Architecture Options

A multi-option architecture evaluation frame. Given a business target
state, compare three or more architectural paths to get there:
enhance-legacy, best-of-breed-package, integrated-package (or
equivalents per context). The output is a pptx deck with a
side-by-side summary matrix that makes the decision legible to a
board.

GrowDirect ships this as the `consulting:it-architecture-options`
skill. Plug in a retailer's current application landscape and target
operating model; get a structured multi-option deck with per-option
heat-maps, effort estimates, risk, and a side-by-side comparison.

## The eight-section frame

1. **Introduction** — purpose, scope, options under evaluation.
2. **Programme Targets** — margin / overhead / headcount / sales /
   profit targets the architecture must enable.
3. **Business Requirements** — structured by process frame (Sell /
   Plan / Move / Buy or equivalent). This section is domain-driven,
   not technology-driven.
4. **Implications for Legacy Systems** — what the current landscape
   can and can't deliver against the target state.
5. **Option A — Legacy Enhancement** (7-slide skeleton below)
6. **Option B — Best-of-Breed Package**
7. **Option C — Integrated Package**
8. **Summary and Conclusion** — side-by-side comparison, recommendation.

## Per-option slide skeleton

Every option gets the same seven slides, in the same order. The
symmetry is what makes the decision legible.

1. **Application architecture heat-map** — target vs. optimisation
   processes, 4-color legend (full support / partial / gap / not
   applicable).
2. **Aspirational heat-map** — same structure, against future-state
   processes.
3. **Development effort estimate** — design days, build-test days,
   rollout days, converted to man-years.
4. **Target application architecture** — post-change view of the
   landscape.
5. **Advantages / Disadvantages** — balanced list, not a pitch.
6. **Implementation timeline and risk** — phased plan with named
   milestones; risk register.
7. **Resource / sourcing plan** — who builds it (internal, vendor,
   SI partner), with FTE and skills breakdown.

## The decision matrix (section 8)

The side-by-side summary is a single slide that lets a board make
the call. Columns are the options; rows are the decision dimensions.

| Dimension | Option A | Option B | Option C |
|---|---|---|---|
| Fit to programme targets | | | |
| Business requirement coverage | | | |
| Implementation effort (man-years) | | | |
| Implementation timeline (months) | | | |
| Total cost of change | | | |
| Risk profile | | | |
| Strategic flexibility | | | |
| Organisation capability change required | | | |
| Recommended | | | |

The recommended column is filled last, after the evidence in the
preceding rows has been established.

## What makes this evaluation durable

1. **Options are symmetric.** Every option gets the same seven
   slides. The reader is trained once and compares cleanly after.
2. **Heat-maps are honest.** The 4-color legend doesn't distinguish
   between "full" and "excellent"; it distinguishes full / partial /
   gap / not-applicable. A vendor deck calibrated this way is not a
   sales pitch.
3. **Effort is quantified.** Man-years, not "significant effort."
   Timeline in months, not "18-24 months."
4. **Risk is enumerated.** Named risks with severity and mitigation,
   not "there is risk inherent to this path."
5. **The recommendation is anchored.** Evidence in rows 1–8 of the
   decision matrix drives the recommendation in row 9. If the
   evidence doesn't pick the option, the evidence is incomplete.

## How the skill applies the frame

The `consulting:it-architecture-options` skill plugs into:

- **Current-state inventory ingest.** Application landscape,
  integration map, current vendor contracts, known gaps. Produces
  structured input for the heat-maps.
- **Option generator.** Given the target state and the current
  landscape, scaffold the three (or more) options with their
  architectural shape.
- **Heat-map renderer.** Given an option's target architecture and
  the business-requirement frame, render the 4-color heat-maps.
- **Effort estimator.** Given the option's scope of change, produce
  the design / build-test / rollout / man-years table.
- **Decision matrix assembler.** Final side-by-side summary.
- **pptx output.** Deck with the 8-section structure and 7-slide
  per-option skeleton.

## Related

- [[method/overview]]
- [[method/retail-diagnostic]]
- [[method/artifacts/sdd-template]]
- [[method/artifacts/traceability-matrix-template]]
