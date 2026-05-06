---
tags:
- content
created: '{{DATE}}'
updated: '{{DATE}}'
name: long-form-writing
description: Use this skill whenever writing long-form content for {{VAULT_OWNER_SHORT_NAME}} — newsletters for their primary or secondary lists, OR long-form articles posted on X. Activate on any task involving drafting newsletter essays, X long-form articles, recurring sections, opening notes, curated commentary, or teaser blurbs that route readers to longer pieces. Enforces {{VAULT_OWNER_SHORT_NAME}}'s voice, audience language, long-form frameworks (Garry-Tan-style is default), and kill list. Unlike promotional emails, long-form content is not directly sales-focused — trigger this skill, not `email-writing`, when the task is recurring or essay content rather than a pitch. Use this skill, not `repurposing`, when generating the original long-form piece (repurposing transforms an existing long-form piece into shorter formats).
title: Long-form writing skill
type: note
---

# Long-form writing skill

## Load first — every time, before writing anything

Read these files in order:

1. `../../voice.md` — {{VAULT_OWNER_SHORT_NAME}}'s voice signature
2. `../../audience/<primary>.md` (and `audience/<secondary>.md` for secondary list newsletters) — audience language
3. `../../kill-list.md` — universal kill list (AI fingerprints, banned patterns)
4. `../../_reference/drafting-feedback.md` — standing instructions (kill-list extension; living)
5. `../../strategy/voice-frame.md` — **per-domain voice nuances + per-domain kill-list additions.** Apply the section matching the piece's domain. See `../../strategy/domains.md` if domain assignment is unclear; ask the user if not specified.
6. `../../engine/hooks.md` — hook formula library
7. `../../engine/frameworks.md` — Garry-Tan-style is the default for long-form
8. `../../engine/techniques.md` — granular rhetorical moves within frameworks
9. `../../engine/cta-patterns.md` — CTA library (newsletter uses direct reply in P.S.; X article uses different CTAs)
10. **One channel file based on output target:**
    - `../../channels/newsletter.md` — for email newsletters
    - `../../channels/x-article.md` — for X long-form articles

These override default writing habits. The shared layer wins on voice, audience, and kill list. The strategy layer adds per-domain nuance on top. The channel file wins on format.

After drafting, run the piece against the **Top 5 highest-violation patterns** at the top of `kill-list.md` before output.

---

## What this skill does

Generates long-form content:

- Primary newsletter (for your primary audience)
- Secondary newsletter (for your secondary audience)
- X long-form articles (1000–2500+ words)
- Newsletter subject lines, opening hooks, philosophical pullbacks
- Recurring newsletter sections
- Curated commentary blurbs

For promotional / pitch emails, use `email-writing` skill.
For taking a long-form piece and creating short-form versions across X thread / X short / LinkedIn, use `repurposing` skill.

---

## When to use this skill vs. `email-writing`

| Task | This skill | `email-writing` |
|---|---|---|
| Recurring weekly content | ✅ | |
| Essay or think-piece | ✅ | |
| Curated commentary | ✅ | |
| X long-form article | ✅ | |
| Promotional / pitch / launch | | ✅ |
| Welcome / onboarding sequence | | ✅ |
| Re-engagement after lapse | | ✅ |

If ambiguous, ask the user.

---

## Process — five phases

The skill runs as five explicit phases. {{VAULT_OWNER_SHORT_NAME}} can interject between phases ("not those headlines, more curiosity-driven") or run end-to-end.

### Phase 1 — Assemble material

Given the topic + audience + channel:

1. **Confirm intent.** Newsletter (primary or secondary list) or X long-form article?
2. **Confirm topic.** What's the central argument / story / observation?
3. **Identify the domain.** Which content domain? Ask if not obvious — domain determines which voice-frame layer applies and which CTAs feel native. See `../../strategy/domains.md`.
4. **Search content-graph for relevant material.** Read `../../content-graph/README.md` "How skills query the graph" for the search protocol. Pull:
   - Takes that anchor the topic's argument or perspective
   - Stories that ground it in lived experience
   - Receipts (specific numbers, dollar amounts, named outcomes) that prove it
   - Quotes (cited wisdom from others) that frame or extend it
   - Recent ideas (trending external signals) that make it timely
   Assemble these as a working brief held in chat — not written to disk. Track every wikilink pulled; this populates `used_material:` in Phase 5.
5. **Identify the confessional opening.** What's the specific moment / quote / scene the piece will open on, drawn from the assembled material? If there isn't one, push back — confessional openings are load-bearing for Garry-Tan-style.
6. **Pick the framework** from `../../engine/frameworks.md`. Garry-Tan-style is default. Per-domain leanings defined in `../../strategy/voice-frame.md`.
7. **Pick a hook formula** from `../../engine/hooks.md` matching the chosen framework and the confessional opening.

### Phase 2 — Draft headline options

Generate 5 channel-appropriate headline candidates following `../../channels/newsletter.md` (or `../../channels/x-article.md`) conventions.

Surface all 5 to {{VAULT_OWNER_SHORT_NAME}} and ask them to pick one (or ask for another set). Don't proceed to Phase 3 until a headline is chosen.

### Phase 3 — Draft the piece

Using chosen headline + assembled material + chosen framework + chosen hook:

1. **Draft the skeleton** following `../../channels/newsletter.md` OR `../../channels/x-article.md`.
2. **Insert section-break pullbacks** (newsletter only — X article uses them more sparingly).
3. **Write the philosophical close** at full length (1–3 paragraphs). Weight by domain per `../../strategy/voice-frame.md`.
4. **CTA selection.** Per domain commercial role in `../../strategy/commercial-mapping.md`.

### Phase 4 — Self-review

Run the piece through the Self-review checklist below. Apply per-domain kill-list additions from `../../strategy/voice-frame.md`. Run against the **Top 5 highest-violation patterns** at the top of `../../kill-list.md` before output.

### Phase 5 — Emit

1. **Save the draft** to disk per the *Output* section. Frontmatter must include `used_material:` populated with every wikilink pulled in Phase 1. Empty list (`used_material: []`) is valid only if Phase 1 produced no graph material — flag this in the output if so.
2. **Surface the draft inline** for immediate review.
3. **Confirm the saved path.**

For sub-tasks that don't produce a full piece (a subject line battery, a single section, a philosophical pullback line, a curated commentary blurb), skip Phase 5 save step and surface inline only. Phase 1 material assembly may also be lighter for sub-tasks, and Phase 2 (headline options) is skipped unless a headline is specifically requested.

---

## Output

### Where full drafts save (varies by target)

| Target | Path |
|---|---|
| Newsletter — primary list | `{{VAULT_NAME}}/areas/content/newsletters/<list-name>/drafts/YYYY-MM-DD-{slug}.md` |
| Newsletter — secondary list | `{{VAULT_NAME}}/areas/content/newsletters/<list-name>/drafts/YYYY-MM-DD-{slug}.md` |
| X long-form article | `{{VAULT_NAME}}/areas/content/socials/x-articles/drafts/YYYY-MM-DD-{slug}.md` |

<!-- per-vault: replace <list-name> with your actual newsletter folder names -->

- `YYYY-MM-DD` is today's date.
- `{slug}` is a lowercase kebab-case version of the piece's central idea or working title. 4–8 words.

If the same date already has a draft with the same slug at the same target, append `-v2`, `-v3`, etc. Don't overwrite.

### Frontmatter — newsletter

```yaml
---
title: "<title / subject line>"
type: area
tags:
  - newsletter
  - draft
  - <list-tag>            # per-vault: tag matching your list name
status: draft
list: <list>              # per-vault: your list name
domain: <domain>          # per your strategy/domains.md slugs
pillar: <pillar-slug>     # per your strategy/pillars.md Slug column
framework: <framework>    # garry-tan | contrast-driven | pas | bab | story-led
hook: <formula>           # authority-moment | specific-receipt | contrast | personal-observation | curiosity-question | replacement | behind-the-scenes
word_count: <integer>     # rough count after drafting
used_material: []         # wikilinks to content-graph entries pulled into this draft (empty list valid)
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
```

### Frontmatter — X article

```yaml
---
title: "<article title>"
type: area
tags:
  - x-article
  - draft
  - <topic-tag>
status: draft
platform: x
domain: <domain>
pillar: <pillar-slug>
framework: <framework>
hook: <formula>
word_count: <integer>
used_material: []         # wikilinks to content-graph entries pulled into this draft (empty list valid)
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
```

### Body format — newsletter

```markdown
**Subject:** <subject line>

**Preview:** <preview text>

---

<opening hook (confessional)>

<the pivot>

## <section heading>

<tactical content>

<section-break pullback>

## <section heading>

<tactical content>

(repeat for 2–4 sections)

---

<philosophical close — 1–3 paragraphs>

Your Pal,
{{VAULT_OWNER_SHORT_NAME}}

P.S. <reply ask>

P.P.S. <optional tactical add-on>
```

### Body format — X article

```markdown
**Title:** <article title>

**Cover image suggestion:** <text or path, optional>

---

<opening hook — first 280 chars must land>

<the pivot>

## <section heading>

<tactical content>

(repeat for 2–4 sections)

---

<philosophical close>

<optional final-line link to related content (e.g., newsletter signup)>
```

### Inline output

After saving, surface the full piece inline for immediate review. Always confirm the saved path:

> Saved to: `{{VAULT_NAME}}/areas/content/newsletters/<list-name>/drafts/YYYY-MM-DD-{slug}.md`

(Or whichever path applies based on the target.)

---

## Self-review checklist (before output)

- [ ] Subject line / title is specific over clever.
- [ ] Opening drops the reader into a specific moment (named, real, vivid).
- [ ] At least one philosophical pullback at the close, beyond just a tactical summary. Weight matches domain per `../../strategy/voice-frame.md`.
- [ ] If the piece has 3+ sections, at least one section break has a pullback (newsletter only).
- [ ] Specific receipts (real numbers, real names, real timelines) in the tactical middle.
- [ ] No em dashes anywhere.
- [ ] Negative parallelism (*"It's not X. It's Y."*) used at most once across the whole piece.
- [ ] No bold-first bullets unless the bolded term is load-bearing.
- [ ] Section names are not literal repeats of names used in recent newsletters.
- [ ] **Newsletter only:** Sign-off is *Your Pal, / {{VAULT_OWNER_SHORT_NAME}}*. P.S. asks a specific reply question.
- [ ] **X article only:** No P.S. / sign-off. Optional final-line link to related content.
- [ ] No banned words / phrases / structures from `kill-list.md`.
- [ ] **Per-domain kill-list cleared.** See `../../strategy/voice-frame.md` for full per-domain kill items.
- [ ] CTA matches domain-commercial role per `../../strategy/commercial-mapping.md`.
- [ ] Draft saved to the correct path for the target with complete frontmatter including `domain` and `pillar`. Full pieces only; skip for sub-tasks like subject-line batteries.
- [ ] Saved path confirmed inline.
