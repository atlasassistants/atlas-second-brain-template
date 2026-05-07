---
tags:
- content
created: '{{DATE}}'
updated: '{{DATE}}'
name: repurposing
description: Use this skill whenever {{VAULT_OWNER_SHORT_NAME}} has an existing long-form piece (newsletter or X long-form article) and wants short-mid form platform-native versions for X thread, X short, and/or LinkedIn post. Activate on tasks like "turn this newsletter into a LinkedIn post," "give me an X thread version of this article," "what's the short-form version," or "repurpose this for social." Enforces {{VAULT_OWNER_SHORT_NAME}}'s voice, audience language, repurpose chain logic, and kill list. Each output rethinks the piece for its platform — it does not reformat. Do NOT use this skill to generate the original long-form source (that's `long-form-writing`).
title: Repurposing skill
type: note
---

# Repurposing skill

## Load first — every time, before writing anything

Read these files in order:

1. `../../voice.md` — {{VAULT_OWNER_SHORT_NAME}}'s voice signature
2. `../../audience/<primary>.md` — audience language (also `audience/<secondary>.md` if the source piece targets the secondary audience)
3. `../../kill-list.md` — universal kill list (AI fingerprints, banned patterns)
4. `../../_reference/drafting-feedback.md` — standing instructions (kill-list extension; living)
5. `../../strategy/voice-frame.md` — **per-domain voice nuances + per-domain kill-list additions.** Apply the section matching the source piece's domain — repurposed pieces inherit the source's domain.
6. `../../strategy/distribution.md` — **which platforms to repurpose to per domain.** Critical: check which domains restrict which platforms. Refuse or push back if the user asks for a target the strategy says skip for that domain.
7. `../../engine/repurpose.md` — chain logic, what changes per platform, the litmus test
8. `../../engine/hooks.md` — hook formula library (per-platform fit matters here)
9. `../../engine/techniques.md` — granular rhetorical moves (light usage in short-form; cross-reference)
10. **One or more channel files based on output targets:**
    - `../../channels/x-thread.md` — for X thread output
    - `../../channels/x-short.md` — for X short output
    - `../../channels/linkedin-post.md` — for LinkedIn post output

After drafting, run each output against the **Top 5 highest-violation patterns** at the top of `kill-list.md`, then run the **litmus test** in `engine/repurpose.md` before output.

---

## What this skill does

Takes a long-form source piece and produces platform-native short-mid form versions:

- LinkedIn post (1300–2000 chars, personal narrative)
- X thread (5–10 tweets, step-by-step or contrarian breakdown)
- X short (1–3 tweets, single hot take or proof)

Optionally on request: email teaser, newsletter excerpt, sales-call talking points.

For generating the original long-form piece, use `long-form-writing` skill.
For promotional emails, use `email-writing` skill.

---

## Process

**Material is the source piece, not content-graph.** When you read the source's frontmatter (see Step 1), also check `used_material:`. If it's populated, **copy that exact list verbatim** into every derivative output's frontmatter. Do not search the content-graph yourself — the source piece already did that work, and propagating its provenance keeps `suggest-topic` dedup honest. If the source piece has no `used_material:` field, the list is empty, or the field is present but not a valid list of wikilinks, output `used_material: []` on each derivative. If repurposing from multiple source pieces, union the `used_material:` lists across all sources (deduping wikilinks).

1. **Confirm the source.** Where's the long-form piece? Newsletter? X article? Provided in the prompt? If it's a saved file in `{{VAULT_NAME}}/areas/content/newsletters/...` or `.../socials/x-articles/...`, capture the path — it goes into the frontmatter for traceability. Read the source's frontmatter to identify its **domain** and **pillar**. If the source predates the strategy (no `domain:` field), infer from content and confirm with the user.
2. **Confirm output targets — and domain-validate them.** Check `../../strategy/distribution.md` for which platforms are on-strategy per domain. Push back if the user requests a target the strategy says to skip for that domain.
3. **Step 1 of the chain — extract building blocks.** Per `engine/repurpose.md`, pull from the source:
   - Thesis (one sentence)
   - Receipts (2–4 specific concrete proofs)
   - Contrast moves
   - Philosophical pullback line(s)
   - Original hook
4. **Step 2 — generate per platform.** For each on-strategy target, apply the platform's native energy:
   - **LinkedIn:** personal narrative reframe, professional but human, first-person heavy
   - **X thread:** step-by-step or contrarian, lowercase casual, one idea per tweet
   - **X short:** maximum compression, single beat
5. **Run the litmus test.** *"If a follower of all three platforms saw what I just wrote, would they be annoyed seeing the same content three times?"* If yes — go back, rethink rather than reformat.
6. **Self-review** each output against the checklist below, including per-domain kill-list additions from `../../strategy/voice-frame.md`.
7. **Save the repurposed bundle** to disk per the *Output* section below. All platform versions go in one file. Frontmatter inherits `domain` and `pillar` from the source.
8. **Surface the bundle inline** for immediate review and confirm the saved path.

---

## Output

### Where bundles save

```
{{VAULT_NAME}}/areas/content/socials/repurposed/drafts/YYYY-MM-DD-{slug}.md
```

- `YYYY-MM-DD` is today's date.
- `{slug}` is a lowercase kebab-case version of the source piece's central idea — ideally matching or echoing the source's slug for traceability. 4–8 words.

If the same date already has a draft with the same slug, append `-v2`, `-v3`, etc. Don't overwrite.

**One file per source idea.** All platform versions go inside the same file, clearly section-separated. The reviewer reads all three side-by-side to apply the litmus test before publishing.

### Frontmatter

```yaml
---
title: "Repurposed: <source title>"
type: area
tags:
  - socials
  - repurposed
  - draft
status: draft
domain: <domain>          # inherited from source — per your strategy/domains.md slugs
pillar: <pillar-slug>     # inherited from source
source_path: <relative path to source long-form piece>
source_title: "<source title>"
source_published: <YYYY-MM-DD or null>
platforms:                # only those on-strategy for the source's domain
  - linkedin              # check strategy/distribution.md per domain
  - x-thread              # check strategy/distribution.md per domain
  - x-short               # check strategy/distribution.md per domain
used_material: []         # wikilinks to content-graph entries — propagated verbatim from source piece's used_material: (empty list valid)
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
```

If only some platforms were generated (e.g., user requested LinkedIn only), reflect that in the `platforms` list.

### Body format

```markdown
# Repurposed: <source title>

**Source:** [<source title>](<relative path to source>)
**Source published:** <YYYY-MM-DD or "not yet">

## Building blocks (extracted from source)

- **Thesis:** <one sentence>
- **Receipts:** <2–4 specific proofs>
- **Contrast moves:** <list>
- **Philosophical pullback:** <key line(s)>
- **Original hook:** <source hook>

---

## LinkedIn post

<full LinkedIn post, 1300–2000 chars>

---

## X thread

**Tweet 1 (hook):**
<text>

**Tweet 2:**
<text>

**Tweet 3:**
<text>

(continue for 5–10 tweets)

**Final tweet:**
<text>

---

## X short

<single tweet OR 2–3 tweet setup-punchline, with each tweet labeled if multi-tweet>

---

## Litmus test

- [ ] LinkedIn version uses first-person narrative framing.
- [ ] X thread is step-by-step or contrarian, not just a reformatted LinkedIn.
- [ ] X short strips everything except the punch.
- [ ] If a follower of all three saw all three, they would NOT be annoyed.
```

### Inline output

After saving, surface all platform versions inline for immediate review. Always confirm the saved path:

> Saved to: `{{VAULT_NAME}}/areas/content/socials/repurposed/drafts/YYYY-MM-DD-{slug}.md`

---

## Self-review checklist (per output)

### All outputs
- [ ] Specific receipt from the source preserved.
- [ ] No em dashes anywhere.
- [ ] No banned words / phrases / structures from `kill-list.md`.
- [ ] **Per-domain kill-list cleared** for the source's domain (see `../../strategy/voice-frame.md`).
- [ ] Hook differs from the source's hook (rethink, not reformat).
- [ ] Output platforms match the strategy per `../../strategy/distribution.md`. No off-strategy outputs.

### LinkedIn post specific
- [ ] First line is a hook that lands within ~210 characters (LinkedIn truncation point).
- [ ] First-person narrative framing throughout (heavy *"I"* usage).
- [ ] Sentence case (not lowercase casual).
- [ ] No more than 3 hashtags (or zero) at the end.
- [ ] Soft CTA or no explicit CTA.
- [ ] Link in first comment if used, never in body.

### X thread specific
- [ ] Hook tweet stands alone (most readers see only this one).
- [ ] Lowercase casual.
- [ ] Line breaks between thoughts in tweets.
- [ ] No hashtags.
- [ ] One idea per tweet.
- [ ] Specific receipt per tweet, not all compressed into one.
- [ ] Closing tweet is either compressed pullback OR soft prompt, not both.
- [ ] Link in self-reply, never in main thread.

### X short specific
- [ ] One complete idea, ≤ 280 chars (or 2–3 tweet setup-punchline).
- [ ] Strips everything except the punch.
- [ ] No hashtags, no exclamation points.
- [ ] Lowercase casual.

### After all outputs generated
- [ ] **Litmus test passed:** a follower of all three platforms would NOT be annoyed seeing all three versions.
- [ ] Bundle saved to `{{VAULT_NAME}}/areas/content/socials/repurposed/drafts/YYYY-MM-DD-{slug}.md` with complete frontmatter (source path, source title, domain, pillar, platforms list).
- [ ] Saved path confirmed inline.
