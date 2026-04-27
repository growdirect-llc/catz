---
classification: confidential
owner: GrowDirect LLC
type: method-reference
skill: plugins/consulting/skills/retail-diagnostic/SKILL.md
nav_order: 3
---

# Method — Retail Diagnostic

A 7-section diagnostic frame. Financial baseline → two theme
drill-downs → priorities → roadmap → case for action. The output is
a pptx deck a board can read standalone.

GrowDirect ships this as the `consulting:retail-diagnostic` skill.
Plug in a client evidence pack; get a structured diagnostic deck with
quantified prize-sizing, per-theme drill patterns, a prioritised
roadmap, and a phased case for action.

## The seven sections

Every slide carries a numbered navigator ribbon in the top-right
corner showing 1–7. That ribbon is the skill's sine qua non — every
slide must earn a number.

1. **Executive Summary** — the entire deck rendered in miniature.
   One-page summary of each of the other six sections, plus a
   prize-sizing roll-up and the phased roadmap. Read-standalone.
2. **Background, Scope & Approach** — workshop themes, scope
   (objectives and constraints), approach (phases, stores sampled,
   data extracts).
3. **Financial Analysis & Industry Drivers** — sales, margin, EBIT,
   stock turn, customer satisfaction index, industry peer
   comparison. Every number has a source cite. This section
   establishes the financial reality that makes the prize credible.
4. **Theme 1 — Findings & Observations** — per-root-cause drill
   pattern. Section opens with Overview + prize sizing; closes with
   Recommendations.
5. **Theme 2 — Findings & Observations** — same pattern as Theme 1,
   different domain.
6. **Opportunity Priorities & Roadmap** — 2×2 prioritisation matrix
   (Prize × Cost-of-Change). Recommended Initiatives tables.
   Implementation sequencing.
7. **Prioritised Case for Action** — Phase 1 (quick wins, Q1–Q4 year
   1), Phase 2 (year 2), Phase 3 (year 3+). Milestones overlay.
   Action plan / next steps.

## The repeating drill pattern (per theme)

Every theme uses the same four-element pattern. This is what gives
the deck its rhythm and makes the methodology transferable.

**Element 1 — Theme Overview** (one slide)

- Left panel: High-Level Summary of Findings (6–8 bullets,
  quantified where possible).
- Right panel: Root-cause navigator — a mini-TOC for the drill
  slides that follow.
- Bottom ribbon: Three bold one-line callouts that state the shape
  of the opportunity.

**Element 2 — The Prize (Potential Opportunity)** (one slide)

- Center: Low Range / High Range quantification table. One row per
  driver, with a total sales / margin / cost opportunity.
- Right panel: Findings narrative explaining how the numbers were
  derived (data extract, period, method).
- Bottom ribbon: Three bold callouts anchoring the prize to business
  truths.

**Element 3 — Per-Root-Cause Drill Slide** (repeats N times, once per
navigator entry)

- Title: "Causes of [Theme Problem] — [Root Cause]"
- Left column: **Findings** — 5–8 bullets, each anchored to a fact.
- Right column: **Leading Practice** — what best-in-class retailers
  do, 3–5 bullets. This column is what separates a diagnostic from a
  critique.
- Bottom ribbon: Three bold one-line conclusions.
- Left-edge ribbon: Root-cause navigator with current slide
  highlighted.

**Element 4 — Recommendations block** (closes the theme)

- Title: "[Theme] — Recommendations"
- Left column: **Recommendations** — numbered list, each bound to a
  root cause.
- Right column: **Implementation Challenges** broken into five
  disciplines: People / Process / Technology / Financial / 3rd Parties.
- Bottom ribbon: Three bold one-line anchors.

## The Opportunity Priorities matrix (section 6)

Every recommended initiative is scored on five axes in a heat-map
table:

| # | Focus Area | Recommendation | Prize Dimension 1 | Prize Dimension 2 | Prize Dimension 3 | Cost of Change | Complexity of Change |
|---|---|---|---|---|---|---|---|

- First three columns = **prize**. Potential material improvement
  → no material improvement (scaled rating).
- Last two columns = **cost** (inverted). Significant implementation
  cost / business change required → minimal or no cost.
- This table feeds the 2×2 prioritisation scatter: high-prize /
  low-cost gets Phase 1; high-prize / high-cost gets Phase 2 or 3;
  low-prize / high-cost gets dropped.

## The roadmap (section 7)

Three phases, at least eight quarters visible (Q1-year1 through
Q4-year2 as minimum). Each phase labelled with the question it
answers:

- **Phase 1 — "What are our quick wins?"** Actions that can start
  in Q1 and deliver measurable benefit inside 12 months.
- **Phase 2 — "What builds the system?"** Actions that require
  platform work (new systems, tooling, integration).
- **Phase 3 — "What's the end state?"** Actions that require
  cultural or capability shift (new operating model, new governance,
  new skills).

Above the phase bars: Milestones overlay that aligns each phase with
named programme deliverables.

## What makes this diagnostic durable

1. **Evidence first, recommendation second.** Every slide in
   Sections 3–5 ends with three bold callouts that summarise *what
   the data says*, not *what we think they should do*.
2. **The prize is quantified.** No "significant opportunity"
   without a low/high range. No range without a method cite on the
   same slide.
3. **The drill is symmetrical.** Every root cause gets Findings +
   Leading Practice + three callouts, every time.
4. **The roadmap is phased against milestones already on the
   client's calendar.** The deck doesn't propose a new programme;
   it overlays the client's existing programme with opportunity
   sequencing.

## How the skill applies the frame

The `consulting:retail-diagnostic` skill plugs into:

- **Client evidence ingest.** Financial extracts, POS data, systems
  inventory, workshop notes. Ingest creates a structured JSON
  evidence pack.
- **Prize-sizing generator.** Given the evidence and a theme,
  compute the low/high range and render the quantification table.
- **Per-theme drill generator.** Generate N root-cause drill slides
  using Findings / Leading Practice pairings.
- **Roadmap assembler.** Given Recommended Initiatives and known
  client milestones, assemble the three-phase roadmap.
- **pptx output.** Final deliverable is a `.pptx` matching the
  structural frame (numbered navigator ribbon; left-column /
  right-column body; three-callout footer; heat-map tables).

The methodology is the skill's system prompt. The evidence is the
skill's input. The skill enforces the shape.

## Related

- [[method/overview]]
- [[method/it-architecture-options]]
- [[method/roles/data-detective]]
- [[method/roles/digital-plumber]]
