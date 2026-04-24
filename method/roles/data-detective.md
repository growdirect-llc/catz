---
classification: confidential
owner: GrowDirect LLC
type: role-playbook
---

# Role — Data Detective

Data Detectives translate a retailer's heterogeneous data — POS
exports, spreadsheets, system inventories, interview notes, workshop
transcripts, invoice archives — into GrowDirect's canonical retail
data model. They are the front line of a CATz engagement.

## The mandate

Every retailer has data. Most of it doesn't speak a common language.
Some of it is in a POS system. Some is in spreadsheets an accounts
clerk maintains. Some is in a back-office legacy system nobody has
logged into in three years. Some is in the founder's head.

Data Detectives assume nothing, find everything, and structure what
they find against the canonical model so the rest of the engagement
— diagnostic, option modeling, implementation planning — runs on
ground truth.

## What a Data Detective delivers

1. **Data map.** Every source system, spreadsheet, and document
   cataloged. Format, custodian, refresh cadence, known gaps.
2. **Source-to-canonical mapping.** For each source, how its
   entities translate to the canonical retail data model (People ×
   Places × Things × Events × Workflows). Explicit mappings,
   transformations, defaults for missing values.
3. **Evidence pack.** Structured JSON inputs for the retail-diagnostic
   and it-architecture-options skills. Every number in the skill
   output is traceable to a source.
4. **Gap register.** Known data gaps with severity (blocks analysis /
   degrades analysis / nice-to-have) and proposed remediation.

## How the role is trained

Data Detectives are agents (or human-agent pairs) trained through:

1. **Knowledge cards** in the Brain vault — reusable patterns for
   recognizing source shapes (flat-file POS export vs. database
   extract vs. receipt text), common entity confusions (item-id vs.
   SKU vs. UPC), and canonical-model traps (store ≠ location if a
   store has multiple fulfilment points).
2. **Memory chunking** against the canonical model — every new
   retailer's data shape becomes a delta against the model, stored
   as a reusable translation rule.
3. **Progressive exposure** to real client evidence packs, with each
   pack adding new shapes to the translation corpus.

Over time, a Data Detective's capability isn't in knowing one
retailer; it's in pattern-matching across many retailers and picking
the right translation on first encounter.

## Relationship to other roles

- **Digital Plumbers** ([[method/roles/digital-plumber]]) receive
  the source-to-canonical mappings and wire the runtime integration.
  Detectives tell them what translation to build; plumbers build it.
- **Architects** consume the data map during Phase II option
  modeling — it drives which systems are candidates for
  replacement vs. integration.
- **Engineers** consume the evidence pack during the diagnostic
  skill run.
- **Writers** reference the gap register in the Phase I diagnostic
  deliverable.

## Anti-patterns

- **Assuming the POS is the source of truth.** It usually isn't.
  Receipts, email, spreadsheets, and back-office PDFs carry more
  operational truth than the POS for most SMB retailers.
- **Accepting a source without verifying it.** "We have ten years of
  data in this system" usually means "the system has been running
  for ten years." Whether the data is consistent, complete, or even
  read by anyone is a separate question.
- **Skipping the gap register.** A diagnostic built on incomplete
  data without an acknowledged gap register overclaims. The gap
  register is what makes the rest of the engagement defensible.

## Related

- [[method/roles/digital-plumber]]
- [[method/retail-diagnostic]]
- [[cbm-v2/agent-strategy]]
