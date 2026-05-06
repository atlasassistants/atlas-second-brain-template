---
title: "Engine: Repurpose chain"
type: note
tags:
  - writing-system
created: 2026-04-29
updated: 2026-04-29
---

# Engine: Repurpose chain

> **Status:** v1 chain logic for repurposing long-form content into platform-native pieces. Used by the `repurposing` skill.

The repurposing skill takes a long-form piece (newsletter or X article) and produces platform-native versions for X thread, X short, and LinkedIn post. **Each output rethinks the piece for its platform — it does not reformat.**

---

## When this fires

The `repurposing` skill activates when:
- A newsletter or long-form X article has been written and is the source of truth.
- The user wants short-mid form versions of the same idea for X thread, X short, or LinkedIn.

The skill does NOT activate to:
- Generate the original long-form piece (that's `long-form-writing` skill).
- Write standalone short-form content not derived from a longer piece.

---

## The chain order

Always work from the long-form piece outward. Don't write the short-form first and try to expand later — the depth has to come from the source.

### Step 1: Extract the load-bearing pieces from the long-form source

Read the source piece and pull:

1. **The thesis.** One sentence that captures the central argument.
2. **The receipts.** 2–4 specific concrete proofs (real numbers, named subjects, real timelines).
3. **The contrast moves.** Anti-patterns {{VAULT_OWNER_SHORT_NAME}} set up explicitly, and the moves shown in response.
4. **The philosophical pullback.** The line(s) at the close that reframe what the tactic means.
5. **The hook.** The opener actually used in the source.

These are the building blocks for every platform variant.

### Step 2: Generate per platform

Each platform gets a fundamentally different version. Match the angle to the platform's native energy:

#### LinkedIn post (1300–2000 chars)
- **Angle:** Personal narrative. *"I [did/learned/saw something specific]. Here's what it taught me."*
- **Hook:** First line is everything (LinkedIn truncates at ~210 chars). Lead with the receipt or the personal observation, not the thesis.
- **Body:** Build the lesson from the specific story. End with the philosophical pullback.
- **CTA:** Soft (reply, save) or none. Link in first comment, never in the post body.
- **What changes from the source:** Tonally professional but personal. Uses *"I"* heavily. The hook reframes for first-person narrative even if the source was more analytical.

#### X thread (5–10 tweets)
- **Angle:** Step-by-step or contrarian breakdown. The thread structure forces serial logic, so pick the part of the source piece that breaks down cleanly into steps or numbered points.
- **Hook (tweet 1):** Contrarian, receipt, or replacement formula (see `engine/hooks.md`). Must stand alone — most readers see only tweet 1.
- **Body (tweets 2–N):** One idea per tweet. Numbered steps work. Concrete examples per tweet (one specific receipt per tweet beats five compressed into one).
- **Final tweet:** Either the philosophical pullback compressed, or a soft prompt to reply / save.
- **What changes from the source:** Lowercase, casual tone. Sentence fragments allowed (but not all-fragment per `kill-list.md`). No em dashes.

#### X short (1–3 tweets)
- **Angle:** A single hot take, proof drop, or contrarian one-liner.
- **Format:** One tweet, max 280 chars. Or a 2–3 tweet micro-thread for a setup-punchline.
- **Pull from:** The source's most-quotable line. The receipt that's most specific. The contrast move that lands hardest.
- **What changes from the source:** Massively compressed. Strip everything except the punch.

---

## The litmus test

After generating all three versions, run this test:

> *"If a reader followed {{VAULT_OWNER_SHORT_NAME}} on LinkedIn AND X AND read the newsletter, would they be annoyed seeing what feels like the same content three times?"*

- **If yes:** It's reformatting, not rethinking. Go back. Each version should give a follower of all three platforms a meaningfully different read of the same idea.
- **If no:** Done correctly.

---

## What changes between platforms

| Element | Newsletter source | LinkedIn | X thread | X short |
|---|---|---|---|---|
| Tone | Reflective, personal | Professional but personal | Casual, lowercase | Sharpest, compressed |
| Length | 800–1500 words | 1300–2000 chars | 5–10 tweets | 1–3 tweets |
| Hook | Confessional or scene | First-person narrative | Contrarian / receipt | Hot take or proof |
| Structure | Garry-Tan: confessional → tactical → philosophical | Personal narrative + lesson | Step-by-step or contrarian breakdown | Single beat |
| Receipts | All of them | 1–2 best, in story form | 1 per tweet | 1 total |
| Philosophical pullback | Full paragraphs | One line at close | Final tweet or none | Implicit |
| CTA | Direct reply (P.S.) | Reply / save / link in comment | Reply / RT prompt | None or implicit |

---

## Anti-patterns to kill (specific to repurposing)

- **Pasting the same opening across all platforms.** Each platform gets a fresh hook.
- **Using the same hook structure across all platforms.** Different platforms reward different hook formulas (see `engine/hooks.md`).
- **Including the email-style P.S. in X or LinkedIn versions.** Format mismatch.
- **Including @mentions or hashtags in the newsletter source.** They don't belong in the email format.
- **Generating LinkedIn version with X-style lowercase casual.** Tonal mismatch.
- **Repurposing without first extracting the building blocks.** Skipping Step 1 produces shallow output.
- **Compressing the philosophical pullback into a one-liner that reads as cheerleading.** If the pullback won't survive compression, omit it from the short-form version rather than mangling it.

---

## Optional outputs (can be added on request)

The default outputs are LinkedIn + X thread + X short. The repurposing skill can also produce on demand:

- **Email teaser.** A 100–200 word email pointing readers to the full newsletter / X article.
- **Newsletter excerpt.** A 200–400 word excerpt for cross-promotion (e.g., a guest spot in another newsletter).
- **Sales-call talking points.** 3–5 bullet points that capture the piece's argument for verbal delivery.

These are not generated by default. The user must request them explicitly.
