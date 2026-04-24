---
classification: confidential
owner: GrowDirect LLC
date: 2026-04-24
type: dry-run-verification
scope: CATz
---

# CATz — Cold-Reader Verification

## Verdict

**PASS**

Walked by a first-time reader simulating a skilled engineer / CTO-type
partner opening the vault under NDA. The vault is small, internally
coherent, and free of the prior-client / prior-employer contamination
that would kill it on open. The two methodology frames (retail-diagnostic
and it-architecture-options) are concrete enough that a reader can
immediately picture the deliverable shape. Ready to show.

## Per-Dimension Results

| Dimension | Result | Notes |
|---|---|---|
| Repo-root standards (5 files + Home.md) | PASS | `README.md`, `NOTICE.md`, `ACKNOWLEDGMENT.md`, `SECURITY.md`, `CONTRIBUTING.md`, `Home.md` all present; render cleanly; no other stray root `.md` files. |
| Confidentiality markings | PASS (with declared exceptions) | 10 content files carry `classification: confidential` + `owner: GrowDirect LLC` frontmatter. `README.md` opens with a purpose block that calls out what the vault is and the authoring rules (spec-acceptable exception). `NOTICE.md` and `ACKNOWLEDGMENT.md` are themselves the confidentiality / access-terms documents and open with "Confidential & Proprietary" and "Access Acknowledgment" headings — functionally equivalent to frontmatter for their role. `Home.md`, `SECURITY.md`, `CONTRIBUTING.md` all have complete frontmatter. |
| No prior-client names | PASS | Zero hits for Kroger, Walmart, Tesco, Meijer, Appriss, Sysrepublic, Retek, PwC, Harrods, Staples, Coles, Fireball, Clarks, Morrisons, Circuit City. "Katz" (the Canadian drug chain) has zero hits — the vault name is an acronym, not the company. |
| No former-company refs | PASS (strict read also clean) | Two "IBM" matches exist, both in authoring-rule meta references: `README.md:37` and `CONTRIBUTING.md:14`, each in the form "No IBM, no prior-employer lineage" as prohibition. No attribution use. "BCS" has zero hits. "Appriss" / "Sysrepublic" have zero hits. |
| No personal names from prior engagements | PASS | Zero hits for Don Boyle, John Teller, Drew Riegler, Tanya Kovacik, Garry Birkhofer, AJ Crawford, Bob Walters, Jeff Goethals. |
| Attribution consistency | PASS | Every file with frontmatter attributes to "GrowDirect LLC." All body text attributing methodology names GrowDirect LLC as the owner. No other entity claimed as author. |
| Method frames are actionable | PASS | `retail-diagnostic.md` specifies a 7-section structure, a 4-element repeating drill pattern (Theme Overview / Prize / Per-Root-Cause / Recommendations), an explicit 2×2 prioritisation matrix schema, and a 3-phase roadmap — a reader could sit down and shape a deck from the frame alone. `it-architecture-options.md` gives an 8-section structure, a 7-slide per-option skeleton, and a 9-row decision matrix with named columns and the "recommended row filled last" discipline — equally buildable. |
| Internal coherence | PASS (with planned-TBD links acknowledged) | All existing cross-references resolve: Home → method/* → roles/* → cbm-v2/overview → about/growdirect-llc. Broken wikilinks all point to articles the vault declares as planned (phases/*, cbm-v2/agent-strategy / data-protection-and-governance / pmo / arb, about/founder, about/licenses-and-standards, partnerships/*, method/roles/architect, method/artifacts/sdd-template, method/artifacts/traceability-matrix-template). Consistent with the "some roadmap/TBD links are OK if the file is planned" clause and with the vault being newly scaffolded. |
| Cold-reader narrative | PASS | After Home.md + method/overview.md + retail-diagnostic.md, a reader has a clear mental model: GrowDirect runs a two-phase engagement (Assess & Design, Select & Implement) with ten + six workstreams; its two productized skills are retail-diagnostic and it-architecture-options; two novel roles (Data Detective, Digital Plumber) make small-team delivery possible; a CBM v2 extension adds four governance cells (Agent Strategy, Data Protection & Governance, PMO, ARB) the classical model missed. The narrative is tight. |

## Regressions

None.

## Positives worth noting

- **Authoring discipline is visible in the artifact, not just declared.**
  The `README.md` and `CONTRIBUTING.md` both enumerate the no-prior-client
  / no-former-employer rules and the vault actually holds to them. That
  consistency between stated policy and executed content is what a
  reader looks for to decide whether the rest of the claims are credible.
- **The two methodology articles are deliverable-shaped, not vague.**
  Both `retail-diagnostic.md` and `it-architecture-options.md` describe
  structures with named sections, slide counts, column labels, and
  scoring dimensions. The methodology could be handed to a new
  contributor and produce a recognisable deliverable. This is the
  failure mode most "methodology vaults" hit and this one avoids.
- **The two novel roles (Data Detective, Digital Plumber) are
  substantive, not decorative.** Each has a clear mandate, an
  enumerated deliverable list, a training model, relationships to
  other roles, and anti-patterns. A reader can see how they'd be
  operationalized by agents, not just named.
- **CBM v2's justification is tight.** The "would an engagement fail
  if this cell wasn't explicitly owned?" test is a good forcing
  function and the four included cells pass it convincingly. The
  explicit list of cells considered and rejected (Marketing, Legal,
  Finance-as-cell, Vendor Management) shows the frame was pressure-
  tested, not just assembled.
- **Root-file hygiene is clean.** Five standards files + Home +
  README, nothing stray, no loose drafts at root. The
  "no .md at vault root except [enumerated list]" rule is honoured.

## Cold-reader narrative

Opening the vault cold: the `README.md` establishes purpose in under
a page, the authoring rules are explicit, and the confidentiality
frame is both declared (`NOTICE.md`, `ACKNOWLEDGMENT.md`) and
operationalized (frontmatter on every content file). Nothing feels
scaffolded-for-show; the files that exist are substantive, and the
wikilinks to not-yet-written files are openly acknowledged as planned
in Home.md rather than hidden as broken references.

Following `Home.md` → `method/overview.md` → `method/retail-diagnostic.md`,
a reader forms a coherent mental model quickly: CATz is a two-phase
engagement method, the two productized skills are concrete and deck-
shaped, the two novel roles (Data Detective / Digital Plumber) explain
how a small team delivers engagement-grade work, and the CBM v2 extension
explains why the company's operating model includes four cells a classical
retail capability map would miss. A CTO-type reader would finish the
first pass understanding what GrowDirect sells, how the method differs
from generic consulting output, and where the productized boundaries
sit. No red flags. Ready to show under NDA.
