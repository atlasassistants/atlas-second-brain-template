---
title: "Engine: Hook formulas"
type: note
tags:
  - writing-system
created: 2026-04-29
updated: 2026-05-06
---

# Engine: Hook formulas

> **Status:** Hook library v1, extracted from voice analysis and the swipe file. Update with performance data and new formulas as patterns emerge.

Hooks are where 70% of a piece's performance is decided. The body can be perfect; if the first line doesn't earn the second, nobody reads the rest.

---

## The seven core formulas

### 1. Authority-moment simulation

**Pattern:** *"If [authority figure] has been telling you to [action], [follow-up]"*

**Why it works for this audience:** Mirrors the trigger compound from `audience/executives.md`. Writing in that voice surrogates the moment.

**Examples (in {{VAULT_OWNER_SHORT_NAME}}'s voice):**
- *"if your coach has been telling you to hire an EA"*
- *"if your fractional COO recommended you call us, they're right"*
- *"if your board cleared the budget for this hire, you're not the only one they're telling"*

### 2. Specific receipt

**Pattern:** *"[Named person/company] [specific outcome] in [specific timeframe]"*

**Why it works:** Voice frame demands receipts over claims. Real numbers and named subjects beat adjectives.

**Examples:**
- *"Patric replaced his US EA in 11 days"*
- *"$150K → $0 in two weeks"*
- *"Eduardo built four months of policy work in four days"*

### 3. Contrast (signature)

**Pattern:** *"You don't need [conventional thing]. You need [reframe]."*

**Why it works:** {{VAULT_OWNER_SHORT_NAME}}'s signature voice move (see `voice.md`). Sets up the anti-pattern explicitly before showing the move.

**Examples:**
- *"you don't need another tool. you need to be managed."*
- *"stop hiring. start subscribing."*
- *"you don't need to fully understand AI. you need to learn how to build and ship."*

**Caution:** Use once per piece. Repeated contrast hooks back-to-back read as AI rhythm. See `kill-list.md` rule on negative parallelism.

### 4. Personal observation / failure moment

**Pattern:** *"[Specific moment of breakdown I witnessed]. [What it revealed]."*

**Why it works:** Specific failure stories outperform abstract claims. Voice frame demands the moment, not the abstraction.

**Examples:**
- *"the EA I hired corrected every output. that was the wrong move."*
- *"a friend told me 'my life has changed' two weeks after I taught him to build with AI"*
- *"my CLAUDE.md was 20,000 lines. I wasn't making the model smarter. I was drowning it."* (Garry Tan style)

### 5. Curiosity question

**Pattern:** *"What would [audience] do if [specific scenario]?"*

**Why it works:** Forces the reader to imagine themselves in the scene before deciding whether to keep reading.

**Examples:**
- *"what would week one look like if your operations person left tomorrow?"*
- *"what's the one tool in your stack that costs the most and gives you the least?"*
- *"if your EA quit on Friday, what would your Monday actually look like?"*

### 6. Replacement

**Pattern:** *"I replaced [expensive/complex thing] with [simple thing]"*

**Why it works:** Strong proof signal. Specific before-after that sounds like a story rather than a claim.

**Examples:**
- *"I replaced four months of policy work with a generator I built in four days"*
- *"we replaced our $8K/mo content stack with a folder of markdown files"*
- *"I replaced our $12K/mo SaaS subscriptions with custom tools we built in a week"*

### 7. Behind-the-scenes

**Pattern:** *"I run [impressive thing] and [surprising method]"*

**Why it works:** Combines authority (the impressive thing) with curiosity (the surprising method). Best for long-form openers.

**Examples:**
- *"I built our AI strategy without writing a single line of code"*
- *"I run 100+ client engagements and don't track them in any CRM"* (hypothetical)

---

## Per-channel hook fit

✅ Best, ⚠️ Mid, ❌ Avoid

| Hook formula | Email subject | X short | X thread | LinkedIn | Newsletter / X article open |
|---|---|---|---|---|---|
| Authority-moment | ✅ | ⚠️ | ⚠️ | ❌ | ✅ |
| Specific receipt | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| Contrast | ✅ | ✅ | ✅ | ✅ | ✅ |
| Personal observation | ✅ | ⚠️ | ✅ | ✅ | ✅ |
| Curiosity question | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ |
| Replacement | ⚠️ | ✅ | ✅ | ✅ | ⚠️ |
| Behind-the-scenes | ⚠️ | ⚠️ | ✅ | ✅ | ✅ |

---

## Rules for hook generation

1. **Two to three hooks per topic, then pick.** Don't ship the first one. The first one is usually the most generic.
2. **Hook for one channel never reuses verbatim for another.** Repurpose by rethinking, not reformatting (see `engine/repurpose.md`).
3. **No em dashes in the hook.** Period.
4. **One specific over five generic.** *"Patric"* beats *"a client."* Real numbers beat *"significant."*
5. **Test against `kill-list.md`** before committing. If the hook contains *"In today's…"*, *"Imagine a world where…"*, or *"Here's the truth…"*, rewrite.
6. **Mystery requires context, or it's just noise.** Pure mystery is ignorable — the reader can just not click the scary movie. For mystery to become magnetic, the hook needs enough specific context that the reader feels *"I don't want to look but I have to."* *"The strangest thing happened…"* is mystery without context. *"$150K → $0 in two weeks. Here's the move."* is specific *and* makes the reader want the rest. The pairing is what creates the magnetic pull.

---

## Performance tracking

> Empty until real data exists. Track formula → channel → engagement (open rate, reply rate, click rate, retweet/save count). Update this file with which formulas actually win on each channel.

| Date | Hook formula | Channel | Piece | Engagement metric |
|---|---|---|---|---|
| | | | | |
