---
classification: confidential
owner: GrowDirect LLC
type: dispatch-template
status: v0.1
---

# Welcome Dispatch — Template

The dispatch that lands in a partner's inbox. Customize per-partner
before sending. This file is the canonical template; produce a
copy for each partner under
`Brain/raw/inbox/onboarding/<partner-slug>-dispatch.md` (internal,
not external).

---

## Email envelope (the part you actually send)

```
To: [partner-email]
From: [founder-email]@growdirect.io
Subject: GrowDirect onboarding — your turn at the keyboard

[Partner first name],

You'll be the one driving this. The way I'd like to share what
GrowDirect is — the methodology, the platform, the architecture —
is by handing you a guided walkthrough you run at your own pace.
About 30–45 minutes total. Stop and resume whenever.

Three things below. Read them in order.

────────────────────────────────────────────
STEP 1 — Acknowledge the access terms

By opening the materials linked in step 2, you're acknowledging
that the contents are GrowDirect LLC's confidential and proprietary
information. Full terms here:

  https://github.com/growdirect-llc/catz/blob/main/ACKNOWLEDGMENT.md
  https://github.com/growdirect-llc/canary-retail-brain/blob/main/ACKNOWLEDGMENT.md

Reply to this email with "I acknowledge and agree" before
proceeding to step 2. The reply is the durable record.

────────────────────────────────────────────
STEP 2 — Open Claude.ai (any tier; free works)

Visit https://claude.ai and start a new conversation. Paste the
prompt block below into the message box and hit send.

What happens next: you'll be talking to ALX (Alejandro Castillo) —
GrowDirect's onboarding companion. ALX will walk you through five
short articles in order, asking you a couple of reflection
questions at each step. About 30 minutes of reading + thinking.

The prompt block:

[ATTACH: onboarding-prompt-vN.md as the inline block, OR paste
the full text inline. The prompt is large — 2,000–3,000 words.
Easier to send as an attachment than inline.]

────────────────────────────────────────────
STEP 3 — Send back what ALX produces

At the end of the journey, ALX will produce a structured brief —
your priorities, areas of interest, concerns, questions. Copy
that brief and email it back to me at [founder-email]@growdirect.io.

That's the artifact I'll work from when we have our follow-up
conversation. It also becomes part of GrowDirect's memory bus so
the next time we talk, ALX (or I) will start in context.

If anything in the journey doesn't make sense, or ALX gets stuck,
just email me and we'll handle it.

— [Founder name]
GrowDirect LLC
contact@growdirect.io
```

---

## Customization notes (internal — strip before sending)

Things to adjust per partner:

- **Reading sequence in the prompt.** The default sequence covers
  CATz home → method overview → retail-diagnostic → role
  playbooks → CBM v2 overview → Canary-Retail-Brain platform
  overview → spine → CRDM → worked example. For verticals where a
  specific module matters more, reorder.
- **Reflection questions.** The default questions are general; per-
  vertical or per-partner-stage questions can replace them.
- **The "what happens next" framing.** A buyer-side partner gets
  different framing than a co-founder candidate.

Track per-partner customization in the matching internal dispatch
file so the variant is reproducible.

## Hash-chain note

The synthesis returned by the partner gets hashed and entered into
the partner's memory chain. The hash of this dispatch (the version
they received) is the chain's first link. Subsequent artifacts
chain forward from here.

## Related

- [[onboarding-prompt]] — the prompt the partner pastes
- [[synthesis-template]] — what comes back
- [[../bios/alx]] — ALX persona being spawned
