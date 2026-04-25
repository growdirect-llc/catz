---
classification: confidential
owner: GrowDirect LLC
type: method-artifact
phase: II
workstream: between W1 (To-Be Workshops) and W5 (Scorecard and Shortlist)
---

# Phase II Artifact — Solution Map

## What it is

A consolidated matrix of **spine module coverage** by **candidate platform**. Sits between the To-Be Workshops (W1) and the Scorecard (W5) in Phase II. Translates the workstream-level target state into a vendor-comparison view that's tractable for selection decisions.

The spine (the 13 modules of the retail spine, or the equivalent capability frame for non-retail engagements) provides the rows. Candidate platforms — including the customer's incumbent system, RFP responders, Canary-native modules, and external-vendor fill — provide the columns. Cells encode coverage strength.

The Solution Map is the bridge from "what does the customer need" (To-Be) to "which vendor wins on what" (Scorecard).

## When to produce it

After To-Be Workshops have established the target state at workstream granularity, before RFP responses are scored. The map evolves through Phase II:

- **Draft 1** — at the start of Phase II, populated from the customer's incumbent platform plus general industry knowledge of likely vendors
- **Draft 2** — after RFP responses arrive, rows refined with what each vendor actually claims to cover
- **Final** — at the start of W5 (Scorecard), with cells representing verified coverage based on RFP evidence + reference checks

## Structure

```
                    Vendor A    Vendor B    Vendor C    Native       External
                                                        (Canary)     (3rd party)
Module 1            ●           ●           ◐           —            —
Module 2            ●           ◐           —           —            —
Module 3            —           —           —           ★            ◯ (vendor X)
...
Module 13           —           —           —           —            ◯ (vendor Y)

Legend
●  Full direct coverage              — Not applicable / not offered
◐  Partial / requires derivation     ★ Native build (own product fills gap)
◯  External vendor required          ✗ No coverage anywhere → escalate
```

### Coverage strength taxonomy

For each cell:

| Strength | Symbol | Meaning |
|---|---|---|
| Full direct | ● | Platform exposes the module's data and behaviors directly. Standard integration. |
| Partial / via | ◐ | Platform covers some but not all of the module; or covers it through an indirect path (e.g., omnibus container, derived computation) |
| Native build | ★ | Customer's own product (in our case, Canary) fills the gap natively. Implies a build commitment. |
| External vendor | ◯ | Third-party fills the gap; usually annotated with the vendor name |
| Deferred | — | Module is not in scope for this engagement / phase |
| No coverage | ✗ | Gap exists and no fill is identified — escalate to founder + steering |

### Fill-strategy taxonomy (when a cell is ◐, ★, or ◯)

| Strategy | When to use |
|---|---|
| **(a) Use the platform as-is** — accept partial coverage | When the gap is acceptable for the engagement scope |
| **(b) Derive from existing data** | When the platform's data model contains the underlying primitives but doesn't expose them as a first-class module |
| **(c) Build native** | When the gap is a product opportunity for the customer's own platform (one-stop-shop wedge) |
| **(d) License external vendor** | When the gap is real, the build cost is high, and a mature third-party exists |
| **(e) Defer** | When the gap is not blocking for the engagement scope and can wait for a later phase |

## How the Solution Map feeds Scorecard (W5)

The Scorecard scores vendors on weighted criteria. The Solution Map provides the COVERAGE component of that scoring. Per-module coverage strength translates to per-criterion score. Native and external columns ARE NOT scored as vendor coverage — they're tracked as Phase III scope additions (build budget, third-party license cost, integration burden).

A vendor that has 9 ● modules + 4 ◐ modules scores higher on coverage than a vendor with 7 ● + 6 ◐, but scoring also weighs implementation effort (Phase III burden), strategic fit, and total cost of ownership. The Solution Map informs but does not dictate the Scorecard.

## How the Solution Map informs the customer's roadmap

The Solution Map's ★ (native build) and ◯ (external vendor) columns are NOT just "the gaps." They are **strategic decisions**:

- **★ columns** flag opportunities to extend the customer's own platform — wedges, differentiation, one-stop-shop positioning
- **◯ columns** flag platform partnerships — integration burden, vendor dependency, customer's tool sprawl

Both are inputs to the customer's product roadmap, not just engagement-specific decisions. The CATz engagement surfaces them; the customer's product organization decides whether to act on them.

## Worked example structure

For a hypothetical SMB specialty retailer running an incumbent POS and evaluating a replacement, a Solution Map might look like:

```
                    Incumbent   Vendor A    Vendor B    Native        External
                    POS         (RFP resp)  (RFP resp)  (own build)
T (Transactions)    ●           ●           ●           —             —
R (Customer)        ●           ●           ◐           —             —
N (Devices)         ●           ●           ●           —             —
F (Finance)         ●           ●           ●           —             —
S (Items)           ●           ●           ◐           —             —
D (Distribution)    ◐ via Doc   ●           ◐           —             —
J (Forecast/Order)  ◐ partial   ●           —           —             ◯ (Vendor X)
A (Asset Mgmt)      ◐ derived   —           —           —             ◯ (Vendor Y)
C (Commercial/B2B)  ◐ derived   ●           —           —             —
P (Pricing)         ◐ derived   ●           ◐           —             —
Q (Loss Prev)       substrate   —           —           ★ Canary core —
L (Labor)           ✗           ◐           —           ★ option      ◯ (Vendor Z)
W (Work Exec)       ✗           —           —           ★ option      ◯ (Vendor W)
```

The map shows:
- Vendor A is the strongest direct-coverage candidate
- Modules Q, L, W are **product opportunities** for the customer's native platform — even with vendor selection, these gaps remain unless filled
- Modules J and A are external-vendor candidates regardless of POS selection

The Scorecard (W5) takes the vendor columns and weighs them; the native and external columns inform the product roadmap and total-cost-of-engagement budget.

## What the Solution Map does NOT do

- It does NOT prescribe vendor selection. Scorecard does that, with weighted criteria.
- It does NOT prescribe build-vs-buy decisions for the native column. Those are product-strategic decisions made by the customer's leadership outside the engagement.
- It does NOT replace RFP responses or reference checks. It synthesizes them.
- It does NOT capture commercial terms, pricing, or contract specifics. Those live in W6 (Contract Negotiation).

## Related

- [[../phase-2-select-and-implement]] — Phase II overview and workstreams
- [[scorecard-template]] — Phase II W5 scorecard artifact (TBD if not yet created)
- [[../phase-1-assess-and-design]] — Phase I produces the inputs the To-Be Workshops translate into the Solution Map
- [[../retail-diagnostic]] — the retail diagnostic frame that informs which spine modules are in scope per engagement
