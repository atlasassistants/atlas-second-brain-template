---
title: "Engine: Frameworks"
type: note
tags:
  - writing-system
created: 2026-04-29
updated: 2026-05-06
---

# Engine: Frameworks

> **Status:** Five frameworks confirmed for {{VAULT_OWNER_SHORT_NAME}}'s writing system as of 2026-04-29. Pick one per piece. Don't combine.

Frameworks are macro-structures for how a piece argues. Voice (`voice.md`) controls *how* sentences sound. Frameworks control *how* the argument moves.

---

## 1. Contrast-driven *(signature default)*

**Structure:** Set up the wrong way explicitly. Show the right way.

**When to use:** Every piece can use this at the *section* level. Use as the *whole-piece* framework when the argument is fundamentally a reframe.

**Pattern:**
1. Open with the anti-pattern, named specifically (Notion, EOS, time-blocking, two failed VAs).
2. Honor the effort the reader has already made.
3. Pivot to the structural shift that actually solves it.
4. Close with the philosophical pullback.

**Example openers:**
- *"You've tried Notion. You've tried EOS. You've tried 'just one more push' on time-blocking. None of it stuck. There's a reason. It's not you."*
- *"Most operators stop at 'do this.' The ones who actually shift their business stop, then ask what doing this means about who they're becoming."*

**Caution:** The contrast move can drift into negative parallelism (*"It's not X. It's Y."*) which is the #1 AI tell. Use the contrast at the section/structural level, but limit the *sentence-level* negative-parallelism phrasing to once per piece (see `kill-list.md`).

---

## 2. PAS (Problem → Agitate → Solve)

**Structure:** Name the problem. Sit in the pain. Offer the move.

**When to use:** Pain-led emails. Re-engagement emails. Landing-page problem sections. When the reader is already aware of their pain and just needs you to mirror it.

**Pattern:**
1. **Problem.** State the audience's situation in their own words. Pull verbatim from `audience/executives.md`.
2. **Agitate.** Drag out the cost. Make the consequence concrete. Use specific failure moments (the missed dinner, the 3am ledger, the dropped ball that lost a deal).
3. **Solve.** Introduce the move. Don't over-explain. End with a tight philosophical pullback.

**Caution:** Easy to overdo the agitate beat and slide into manipulation. Stay specific. *"You've been doing this for two years and your spouse is starting to notice"* is a fact. *"Imagine the regret of looking back…"* is manipulation. Stay with the fact.

---

## 3. BAB (Before → After → Bridge)

**Structure:** Show the broken state. Show the resolved state. Name the bridge.

**When to use:** Transformation-focused emails. Service landing pages. Anything where the value is a state change, not a feature.

**Pattern:**
1. **Before.** Where the reader is now. The bottleneck, the missed dinners, the ledger running at 3am. Specific.
2. **After.** Where the reader could be. Sleep without the ledger. Sieve between them and the noise. Identity preserved.
3. **Bridge.** What gets them across. Human-plus-system + replacement guarantee.

**Example arc (compressed for email length):**
- *"Six months from now: you wake up at 6am because you're rested, not because something dropped overnight. Your inbox is sorted before you read it. Your week has already been triaged. You're running the company you built. Nothing else."*
- *"What gets you there isn't another tool. It's a structural change in how the executive support function works."*

---

## 4. Garry-Tan-style *(default for long-form)*

**Structure:** Confessional opening → tactical middle → philosophical close.

**When to use:** Newsletters. X long-form articles. Long-form sales pages (1500+ words). Anywhere the format gives the philosophical pullback room to breathe.

**Pattern:**
1. **Confessional opening.** Drop into a specific moment of breakdown that you witnessed or experienced. Named subjects, real numbers, vivid scene. Garry's *"My CLAUDE.md was 20,000 lines. I wasn't. I was drowning it."* is the template.
2. **The pivot.** One paragraph naming what the moment revealed.
3. **Tactical middle.** What works, how it works, what to do. Receipts. Sub-headings okay. Section-break pullbacks at major transitions.
4. **Philosophical close.** Reframe what the tactic means for who the reader becomes when they actually do it.

**Length sweet spot:** 800–1500 words for newsletter. 1500–3500 for X long-form articles or sales pages.

---

## 5. Authority-moment simulation

**Structure:** Open by addressing the reader as if their authority figure has already pointed them toward this conversation.

**When to use:** Cold-warm emails to people whose coach / board / fractional COO / mastermind peer has been telling them to make this hire. Mirrors the trigger compound from `audience/executives.md`.

**Pattern:**
1. **The authority moment.** *"If your coach has been telling you to hire an EA…"* / *"If your board just cleared the budget…"*
2. **Validation.** *"They're right. Here's what they know."*
3. **The move.** What the authority figure was pointing at, named specifically.
4. **The CTA.** Direct, low-friction (reply, short call).

**Example opener:** *"If your fractional COO has been pushing you to hire an EA, they're right. Here's what they're seeing that you're not."*

---

## Connective tissue: the therefore-but rule

Independent of which framework you pick, every piece needs the right *kind* of linkage between beats. Two patterns:

- **Vignette chain (avoid):** *"This happened, and then this happened, and then this happened."* Each beat is a self-contained item on a list. The reader can step off any time.
- **Therefore-but cascade (use):** *"This happened, **therefore** this happened, **but** this happened, **thus** this happened, **but** this happened…"* Each beat creates the conditions for the next, then complicates them. The reader stays because each beat earns the next.

This is the difference between a string of points and an argument that pulls. Originally articulated by the South Park writers as their core narrative test.

**How to apply:**

- After drafting, re-read each section transition. Are you joining beats with *"and,"* *"also,"* *"another thing"* — or with *"therefore,"* *"but,"* *"thus,"* *"so"*? If it's the first list, the section is a vignette chain.
- The rule fires hardest in long-form (newsletters, X articles, sales pages) where a 1500-word piece without therefore-but reads as a content dump.
- Inside emails, the same rule applies at the paragraph level. A pain → cost → move sequence is therefore-but. A list of three pains is a vignette chain.
- Doesn't require literally writing the words *"therefore"* or *"but."* The rule is about logical linkage between beats, not the connective itself.

**Test:** Can you summarize each section transition as *"X, therefore Y"* or *"X, but Y"*? If multiple transitions are *"X, also Y,"* the piece is a vignette chain. Restructure.

---

## Per-channel framework fit

✅ Best, ⚠️ Mid, ❌ Avoid

| Framework | Email | Landing page | Newsletter / X article | X thread | X short | LinkedIn |
|---|---|---|---|---|---|---|
| Contrast-driven | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| PAS | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| BAB | ✅ | ✅ | ⚠️ | ✅ | ❌ | ✅ |
| Garry-Tan-style | ⚠️ (long emails only) | ⚠️ (long-form pages) | ✅ | ❌ | ❌ | ⚠️ |
| Authority-moment | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ |

---

## Frameworks intentionally NOT in this system

- **AIDA (Attention-Interest-Desire-Action).** Pushes copy toward generic-marketing tone {{VAULT_OWNER_SHORT_NAME}}'s voice avoids.
- **StoryBrand.** Useful in concept; in practice produces formulaic output. The contrast-driven framework captures the same energy without the rigid template.
- **Long Sales Letter formulas (Halbert, Sugarman, Schwartz).** Powerful but tonally mismatched. Save for direct-response sales pages, never for newsletters or general emails.
