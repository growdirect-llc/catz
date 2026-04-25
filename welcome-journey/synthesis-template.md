---
classification: confidential
owner: GrowDirect LLC
type: synthesis-template
status: v0.1
---

# Synthesis Template

The structured artifact ALX produces at the end of an onboarding
journey. The partner copies it from their Claude.ai session and
emails it back to the founder.

## What it captures

Seven verbatim partner reflections (one per article) plus a
synthesized takeaway plus an engagement signal plus any flagged
questions. The verbatim answers are gold — they reveal what the
partner actually thinks before any negotiation framing kicks in.

## Canonical structure

```
─────────────────────────────────────────
GROWDIRECT ONBOARDING — SYNTHESIS BRIEF
─────────────────────────────────────────

Partner: [name or opaque identifier]
Date: [YYYY-MM-DD]
Session: spawned by ALX onboarding prompt v0.1
Hash-chain prev: [NEW or hash of prior artifact]

REACTION TO GROWDIRECT'S FRAMING (Article 1)
[verbatim]

WORKSTREAM CALIBRATION (Article 2)
Right for SMB: [verbatim]
Enterprise overkill: [verbatim]

DIAGNOSTIC FRAME REACTION (Article 3)
Strongest part: [verbatim]
Would push back on: [verbatim]

CBM v2 OPINION (Article 4)
Strongest opinion on: [verbatim]
Their view: [verbatim]

SMB COLLAPSE BULLSHIT DETECTOR (Article 5)
[verbatim]

LAUNCH SHAPE (Article 6)
[verbatim]

EVIDENCE PACK GAPS (Article 7)
Missing: [verbatim]

OVERALL TAKEAWAY (ALX synthesis)
[one paragraph distilling the seven answers]

ENGAGEMENT SIGNAL
[1-5 scale or open-ended]

QUESTIONS FOR GEOFFREY
[any deferred questions]

─────────────────────────────────────────
```

## How the founder uses it

1. **Read once, fully, in the partner's voice.** Don't pre-frame.
   The first read is to hear them.
2. **Cross-reference against the dispatch.** Did they engage with
   what you expected? What surprises?
3. **Tag for memory bus ingestion.**
   - File: `Brain/raw/inbox/onboarding/<partner-slug>-synthesis-<date>.md`
   - Frontmatter: `partner: <slug>`, `chain-prev: <prior-hash or NEW>`,
     `chain-next: <will be set when next artifact lands>`,
     `signal: <1-5>`, `flags: [...]`
4. **Run `engine.py registry build`** to fold into the memory bus.
5. **Compute the SHA-256 hash** of the synthesis file content.
   Record it in `Brain/projects/<partner-slug>.md` under a
   `chain:` section as the latest entry.
6. **Address questions** for Geoffrey directly via email or in
   the next live conversation. Don't let them queue.

## The hash chain — what it gives you

For each partner, you accumulate a chain of artifacts:

```
[NEW] → synthesis-001 → synthesis-002 → debrief-003 → ...
```

Each entry records:
- File path (canonical location)
- Content hash (SHA-256)
- Previous-entry hash (links the chain)
- Date
- Source session description

The partner can request a copy of their chain at any time. Comparing
their chain to GrowDirect's chain proves nothing was rewritten,
inserted, or omitted. This is engagement-grade audit at no extra
cost — same hash-chain pattern Canary uses on transactions.

## Per-partner project file

Recommended structure for `Brain/projects/<partner-slug>.md`:

```markdown
---
type: partner-engagement
partner: <slug>
status: active
classification: confidential
owner: GrowDirect LLC
---

# Partner — <opaque label or name>

## Engagement chain

| Date | Artifact | Hash | Prev | Notes |
|---|---|---|---|---|
| 2026-04-XX | dispatch sent | <hash> | NEW | v0.1 prompt |
| 2026-04-XX | synthesis returned | <hash> | <prev> | signal: 4 |
| 2026-05-XX | follow-up debrief | <hash> | <prev> | post-call |
| ... | | | | |

## Memory profile

What this partner cares about, accumulated:
- ...

## Questions for me

- ...

## Open commitments

- ...
```

Each new interaction with the partner appends to this file and to
the chain.

## Related

- [[onboarding-prompt]] — the prompt that produces this synthesis
- [[dispatch-template]] — the dispatch envelope
- [[../bios/alx]] — ALX persona
- [[../cbm-v2/data-protection-and-governance]] — retention,
  right-to-delete handling
