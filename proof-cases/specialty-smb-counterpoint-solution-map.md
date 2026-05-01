---
classification: confidential
owner: GrowDirect LLC
type: proof-case
applies-to-archetype: specialty SMB retailer (10-50 stores) on NCR Counterpoint via a vertical-specialized VAR
companion-artifact: ../method/artifacts/solution-map.md
date: 2026-04-25
---

# Proof Case — Specialty SMB Retailer on NCR Counterpoint (Solution Map)

## Archetype framing

A specialty SMB retailer running NCR Counterpoint, deployed and configured by an NCR Partner Network VAR (Rapid POS for garden centers; equivalents for gun stores, specialty food, wine, feed-and-tack). 10–50 stores. Front-of-store covered by Counterpoint; back-office layer is the gap.

This proof case applies the Solution Map artifact template to that archetype. It is reusable across customers in the same shape; it does not name any specific retailer.

## The retailer's situation

- Incumbent POS: NCR Counterpoint, deployed by a vertical-specialized VAR. Stable, in-production, customer is generally satisfied with front-of-store
- Pain points: limited back-office analytics, no native loss-prevention layer, no fraud detection, labor scheduling done in spreadsheets or a separate workforce tool, work-execution / store-ops checklists run via paper or text-message
- Vertical-specific needs: multi-tier customer pricing (B2B contractor pricing alongside retail), seasonal demand patterns, multi-skill labor staffing, perishable / live-goods inventory write-off (where applicable)
- IT capacity: thin. A bookkeeper, an outside CPA, possibly an IT contractor on retainer. No in-house engineering.

## Solution Map (Draft 1)

Constructed from To-Be Workshop outputs + general industry knowledge of the candidate platforms. Refined as RFP responses arrive.

```
                    Counterpoint    Replacement      Canary           External
                    (incumbent)     POS candidates   Native           vendor
                                    (RFP TBD)
T (Transactions)    ●               TBD              —                —
C (Customer)        ●               TBD              —                —
N (Devices)         ●               TBD              —                —
F (Finance)         ●               TBD              —                —
S (Items)           ●               TBD              —                —
D (Distribution)    ◐ via Document  TBD              —                —
J (Forecast/Order)  ◐ partial       TBD              —                ◯ (potentially)
A (Asset Mgmt)      ◐ derived       TBD              —                ◯ (potentially)
C (Commercial/B2B)  ◐ derived       TBD              —                —
P (Pricing)         ◐ derived       TBD              —                —
Q (Loss Prev)       substrate only  —                ★ Canary core    —
L (Labor)           ✗ no REST       —                ★ option (d)     ◯ (Homebase / ADP / Deputy)
W (Execution)  ✗               —                ★ option (d)     ◯ (Beekeeper / YOOBIC)

●  Full direct coverage          —  Not applicable / not offered
◐  Partial / requires derivation ★  Native build (Canary fills)
◯  External vendor available     ✗  No coverage from this column
```

## Per-row coverage notes

Coverage strength comes from `Brain/wiki/ncr-counterpoint-api-reference.md` (the GrowDirect-internal Counterpoint reference) and the Counterpoint API repo's `Endpoints/` documentation.

### T (Transactions) — ● Full direct
Counterpoint's `Document` family is comprehensive: sales tickets, returns, voids, orders, layaways. Multi-authority tax, line-level pricing rules, payment detail, audit log embedded. Direct CRDM mapping.

### C (Customer) — ● Full direct
17 endpoints covering Customer, Customer_Address, Customer_Note, Customer_OpenItems, Customers_EC, CustomerControl, Customer_Card. Loyalty embedded in Customer record (12 LOY_* fields). Tier captured as `CATEG_COD`.

### N (Devices) — ● Full direct
Store + Station + Device_Config + Workgroup + StoreTokenize endpoints. Plus per-store config (`PS_STR_CFG_PS`) carries ~150 fields covering tax defaults, drawer config, max discount limits, EDC processor, ticket numbering, dropship, layaway/order workflows.

### F (Finance) — ● Full direct
PayCode (tender taxonomy, cached), TaxCode, GiftCard family, Document_Payments. Multi-authority tax modeled in Document. Tender + tax detail per ticket.

### S (Items / Catalog) — ● Full direct
17 endpoints covering Item, Items, Items_ByLocation, ItemCategories, ItemCategory, ItemSerial(s), Item_Images, Item_Inventory, Inventory_*, VendorItem, EC, ECCategories. Categories carry MIN_PFT_PCT + TRGT_PFT_PCT (margin targets — Module Q substrate). Mix-and-match codes, attribute codes, ecommerce flags.

### D (Distribution) — ◐ Via Document
No dedicated transfer endpoints. Inter-store transfers flow as `Document` records with `DOC_TYP: XFER`. Inventory snapshots via Inventory_* endpoints. Adapter type-routes on DOC_TYP.

### J (Forecast / Order) — ◐ Partial
Purchase orders, purchase requests, returns-to-vendor flow as Document records with PO/PREQ/RTV type codes. Vendor master via VendorItem. **No replenishment-engine endpoint** — replenishment recommendations are likely UI-only. External forecasting / replenishment tool may fill this for customers who need it.

### A (Asset Management) — ◐ Derived
No dedicated asset endpoints. Non-saleable assets likely tracked as items with status flags. Derive from Item + ItemCategories.

### C (Commercial / B2B) — ◐ Derived
No dedicated B2B endpoint family. Derive from Customer record fields (account-charge flags, B2B tier in CATEG_COD, AR balances, terms code). Customer_OpenItems for AR.

### P (Pricing / Promotion) — ◐ Derived
**No dedicated Pricing or Promotion endpoint family.** Pricing lives in Item base prices + Customer-tier flags. Promotion semantics are UI-only — Counterpoint emits the OUTPUT (PS_DOC_LIN_PRICE per ticket line) but does not expose the rules. Multi-tier customer pricing derived from Customer.CATEG_COD + Item prices.

### Q (Loss Prevention) — Substrate only / ★ Canary native
Counterpoint exposes the substrate (Document audit logs, drawer sessions, void-comp reasons, max discount thresholds, category margin targets, employee-on-ticket via USR_ID/SLS_REP) but NOT a loss-prevention module. **★ Canary core covers this** — detection rules run on top of the Counterpoint substrate.

### L (Labor) — ✗ NO Counterpoint coverage / ★ Native option / ◯ External alternative
**Counterpoint REST has no Employee, Timeclock, or Schedule endpoints.** Three real options:

- ◯ External: Homebase / Deputy / When I Work / ADP — mature category, customer pays separately, integration burden
- ★ Native option (d): Canary builds Module L native. POS-data-native scheduling (forecast staff from sales velocity), one-stop-shop wedge for SMB. Tradeoffs: real compliance burden, crowded category, Phase 6+ work.
- — Defer: leave the gap open until customer demand justifies the build / external license

Strategic decision sits with the platform owner. See `project_canary_native_labor_module_opportunity.md` (in GrowDirect memory).

### W (Execution) — ✗ NO Counterpoint coverage / ★ Native option / ◯ External alternative
**Counterpoint REST has no work-execution / task / checklist endpoints.** Same option set as Module L:

- ◯ External: Beekeeper / YOOBIC / Foko Retail — mature task-management for retail
- ★ Native option (d): Canary builds Module E native — store-ops checklists, daily tasks, store-floor workflows
- — Defer

Same strategic decision as Module L.

## Fill-strategy decisions for this archetype

For an SMB engagement in this archetype, the recommended Phase II Solution Map closes as follows (subject to customer-specific constraints):

| Module | Strategy | Rationale |
|---|---|---|
| T R N F S | Use Counterpoint as-is | Direct coverage; standard integration |
| D | Use Counterpoint as-is | ◐ via Document is operationally sufficient for back-office analytics |
| J | (a) Use as-is OR (d) external | Replenishment engine UI-only; if customer needs automation, license a forecasting tool. Otherwise ad-hoc reports suffice for SMB scale. |
| A | Use Counterpoint derived | Asset-tracking depth not typically needed at SMB scale |
| C | Use Counterpoint derived | B2B handling sufficient via Customer-tier fields for SMB scale |
| P | Use Counterpoint derived | Pricing rules opaque but observable per-ticket; sufficient for analytics |
| Q | Canary native | Canary core; non-negotiable |
| L | DECIDE — strategic | (d) native if pursuing one-stop-shop; (◯) external otherwise. **Customer-aware decision.** |
| W | DECIDE — strategic | Same as L |

## Implications for engagement

### Phase II output (vendor selection)

For customers happy with Counterpoint, the recommendation may be to KEEP Counterpoint and add Canary as the back-office analytics layer + LP module. No POS replacement. Phase II becomes a "Canary + retain incumbent" engagement, not a POS-replacement one.

For customers wanting POS replacement, Counterpoint becomes a column to compare against alternatives. The Solution Map evolves through RFP responses.

### Phase III implementation

- Counterpoint integration: standard Canary TSP adapter against the public REST API (covered by `docs/sdds/canary/ncr-counterpoint-retail-spine-integration.md`)
- Q module: Canary core; no external integration needed
- L and W: per the strategic decision (native build vs external license vs defer)

### Customer roadmap implications

L and W as native-build options surface as **product opportunities for the customer's platform owner** (in this case: GrowDirect's Canary product roadmap). A Solution Map for one engagement becomes input to many — patterns repeat across SMB specialty retailers running Counterpoint.

## Related

- `../method/artifacts/solution-map.md` — Phase II artifact template this proof case demonstrates
- `../method/phases/phase-2-select-and-implement.md` — Phase II overview
- `../method/retail-diagnostic.md` — the spine the Solution Map maps against
- (GrowDirect-internal) `Brain/wiki/ncr-counterpoint-api-reference.md` — Counterpoint REST surface catalog informing the coverage assessments
- (GrowDirect-internal) `docs/sdds/canary/ncr-counterpoint-retail-spine-integration.md` — Canary's integration SDD; per-module coverage detail
