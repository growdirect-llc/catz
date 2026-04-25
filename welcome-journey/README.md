---
classification: confidential
owner: GrowDirect LLC
type: system-overview
---

# Welcome Journey

The asynchronous, AI-mediated onboarding loop for external parties
entering the GrowDirect operating surface. Replaces the deck and
the back-and-forth onboarding meeting with an agent-led walkthrough
the partner runs at their own pace.

## How it works

```
Partner → receives welcome dispatch (email + acknowledgment)
       → opens claude.ai (any tier, free works)
       → pastes the onboarding prompt
       → ALX (Alejandro Castillo) is spawned in their session
       → ALX walks them through CATz + Canary-Retail-Brain articles
       → ALX asks structured reflection questions per article
       → ALX produces a synthesis brief at the end
       → partner emails the synthesis back to GrowDirect

Founder → ingests synthesis into the memory bus
       → next ALX session for that partner starts in full context
       → hash-chained for audit; partner can request the chain
```

## Files in this directory

- [[dispatch-template]] — the welcome dispatch (email + intro
  + acknowledgment + prompt) the partner receives. Customize
  per-partner before sending.
- [[onboarding-prompt]] — the multi-thousand-word prompt the
  partner pastes into Claude.ai. Spawns ALX in onboarding role.
  This is the IP-laden artifact; treat accordingly.
- [[synthesis-template]] — the structured artifact ALX produces
  at the end of an onboarding session. Defines what comes back
  to the founder for memory ingestion.

## Why this works

Three properties make this better than a deck or a wiki alone:

1. **Self-paced.** Partner reads when they have time and attention.
   Not a 60-minute meeting where the partner is already half-checked-
   out. Sessions can pause and resume; ALX preserves state.
2. **Structured reflection.** Asking targeted questions per article
   forces the partner to engage actively rather than skim. The
   synthesis they produce is real — it surfaces priorities and
   concerns the partner might not have articulated otherwise.
3. **Memory-extending.** Every session builds the partner's profile
   in GrowDirect's memory bus. The fifth interaction starts five
   sessions deep in context. Compounding over time.

## What this is not

- Not a chatbot. ALX runs a structured journey; free-form chat is
  out of scope (ALX defers to the founder for anything off-script).
- Not a replacement for human meetings at decision moments. The
  welcome journey is for asynchronous orientation; high-stakes
  conversations stay with the founder.
- Not an autonomous agent committing GrowDirect to anything. ALX
  has principal-awareness ([[../bios/alx]]) and explicit
  no-commitment scope.

## Versioning

This system is v0.1. Each customized engagement may produce a
variant prompt with vertical-specific reading sequence and
questions. Variants live alongside the canonical prompt with
explicit version identifiers. See
[[../method/roles/alx|ALX role]] for governance.

## Related

- [[../bios/alx]] — ALX persona
- [[../method/roles/alx]] — ALX as engagement-coordinator role
- [[../cbm-v2/agent-strategy]] — agent governance
