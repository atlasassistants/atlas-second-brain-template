---
tags:
- content
created: '{{DATE}}'
updated: '{{DATE}}'
name: email-writing
description: Use this skill whenever writing promotional, broadcast, or sequence emails to {{VAULT_OWNER_SHORT_NAME}}'s email list. Activate on any task that involves drafting email subject lines, preview text, email bodies, welcome sequences, launch emails, re-engagement emails, or anything {{VAULT_OWNER_SHORT_NAME}} will send to their list. Enforces {{VAULT_OWNER_SHORT_NAME}}'s voice, audience language, email-specific frameworks, and kill list. Trigger even on small tasks like a single subject line or a one-liner teaser.
title: Email writing skill
type: note
---

# Email writing skill

## Load first — every time, before writing anything

Read these files in order. Stop and wait for each before continuing.

1. `../../voice.md` — {{VAULT_OWNER_SHORT_NAME}}'s voice signature
2. `../../audience/<primary>.md` — primary audience; also load `audience/<secondary>.md` if writing to the secondary list
3. `../../kill-list.md` — universal kill list (AI fingerprints, banned patterns)
4. `../../_reference/drafting-feedback.md` — standing instructions (kill-list extension; living)
5. `../../strategy/voice-frame.md` — **per-domain voice nuances + per-domain kill-list additions.** Apply the section matching the email's domain. Most promotional emails are the primary commercial domain. See `../../strategy/domains.md` if domain assignment is unclear; ask if not specified.
6. `../../engine/hooks.md` — hook formula library
7. `../../engine/frameworks.md` — pick one framework per email
8. `../../engine/techniques.md` — granular rhetorical moves within frameworks
9. `../../engine/cta-patterns.md` — CTA library
10. `../../channels/email.md` — email-specific format rules
11. `../../content-graph/README.md` — read the "How skills query the graph" section. Before drafting, search the graph for relevant takes/stories/receipts/quotes that anchor the email's pitch. Pull what fits. Track every wikilink pulled — these populate `used_material:` in the output frontmatter.

These override default writing habits. The shared layer wins on voice, audience, and kill list. The strategy layer adds per-domain nuance on top. The channel file wins on email-specific structure.

After drafting, run the email against the **Top 5 highest-violation patterns** at the top of `kill-list.md` before output.

---

## What this skill does

Generates email copy for {{VAULT_OWNER_SHORT_NAME}}'s list:

- Promotional broadcasts
- Welcome sequences
- Launch emails
- Re-engagement emails
- Single subject lines, single P.S. asks, single hook lines

For long-form content (newsletters, X articles), use `long-form-writing` skill instead.
For short-form repurposing of long-form pieces, use `repurposing` skill.

---

## Process

**Material assembly is inline.** Before drafting subject + body, search `../../content-graph/` for relevant takes/stories/receipts/quotes that anchor the pitch. Pull what fits. The output's `used_material:` frontmatter captures every wikilink pulled. If you draft purely off-prompt with no graph material, `used_material: []` is valid.

1. **Confirm intent.** What's the email's purpose? Promotional? Welcome? Re-engagement? Single subject line battery?
2. **Confirm audience.** Primary list (default) or secondary list?
3. **Identify the domain.** Which content domain? Most direct-promo emails belong to the primary commercial domain. Ask if not specified. See `../../strategy/domains.md`.
4. **Pick one framework** from `engine/frameworks.md`. Don't combine.
5. **Pick one hook formula** from `engine/hooks.md` for the subject line.
6. **Pick one CTA** from `engine/cta-patterns.md`. Direct reply is the email default. Match CTA to domain commercial role per `../../strategy/commercial-mapping.md`.
7. **Draft.** Follow the skeleton in `channels/email.md`.
8. **Self-review** against the checklist below. Fix anything that violates `kill-list.md` or the per-domain kill-list additions in `../../strategy/voice-frame.md`.
9. **Save the draft** to disk per the *Output* section below.
10. **Surface the draft inline** for immediate review and confirm the saved path.

For sub-tasks that don't produce a full email (a single subject line battery, a P.S. tweak, a hook line), skip the save step and surface inline only. The save step applies to full email drafts.

---

## Output

### Where full drafts save

Every full email draft saves to:

```
{{VAULT_NAME}}/areas/content/emails/drafts/YYYY-MM-DD-{slug}.md
```

- `YYYY-MM-DD` is today's date.
- `{slug}` is a lowercase kebab-case version of the email's central idea or subject line. Keep it readable, 4–8 words.

If the same date already has a draft with the same slug, append `-v2`, `-v3`, etc. Don't overwrite.

### Frontmatter (vault contract)

```yaml
---
title: "<subject line>"
type: area
tags:
  - email
  - draft
  - <list-tag>          # per-vault: tag matching your list name
status: draft
list: <list>            # per-vault: your list name
domain: <domain>        # per your strategy/domains.md slugs
pillar: <pillar-slug>   # per your strategy/pillars.md Slug column
purpose: <type>         # promotional | welcome-sequence | launch | re-engagement | other
framework: <framework>  # contrast-driven | pas | bab | garry-tan | authority-moment
hook: <formula>         # authority-moment | specific-receipt | contrast | personal-observation | curiosity-question | replacement | behind-the-scenes
cta: <type>             # direct-reply | soft-conditional | book-a-call | curious-open-loop | authority-mirroring
used_material: []         # wikilinks to content-graph entries pulled into this draft (empty list valid)
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
```

The `framework`, `hook`, and `cta` fields exist to track what's working over time. When {{VAULT_OWNER_SHORT_NAME}} reviews drafts later, this lets them see at a glance which combinations keep shipping.

### Body format

After the frontmatter, the email body uses these section markers (helpful for review and for exporting to Beehiiv / Resend / etc.):

```markdown
**Subject:** <subject line>

**Preview:** <preview text>

---

<opening hook>

<body>

<pullback close>

Your Pal,
{{VAULT_OWNER_SHORT_NAME}}

P.S. <reply ask>

P.P.S. <optional tactical add-on>
```

### Alternative subject lines

After the email body, list 4 alternative subject line options to swap in.

### Inline output

After saving, surface the full draft inline in the chat for immediate review. Always confirm the saved path so {{VAULT_OWNER_SHORT_NAME}} knows where to find it. Format the confirmation as:

> Saved to: `{{VAULT_NAME}}/areas/content/emails/drafts/YYYY-MM-DD-{slug}.md`

---

## Self-review checklist (before output)

- [ ] Subject line sounds like a private message, not a marketing send.
- [ ] Opening drops the reader in. No throat-clear, no *"we're excited,"* no *"in today's fast-paced world."*
- [ ] One core argument, not three.
- [ ] At least one specific receipt (real number, real name, real timeline).
- [ ] No em dashes anywhere.
- [ ] Negative parallelism (*"It's not X. It's Y."*) used at most once.
- [ ] No bold-first bullets unless the bolded term is genuinely load-bearing.
- [ ] Pullback at close reframes meaning, doesn't cheerlead.
- [ ] Sign-off is *Your Pal, / {{VAULT_OWNER_SHORT_NAME}}*.
- [ ] P.S. asks for a specific reply.
- [ ] No banned words / phrases / structures from `kill-list.md`.
- [ ] **Per-domain kill-list cleared.** See `../../strategy/voice-frame.md` for full per-domain kill items.
- [ ] If contrast framework: anti-pattern named specifically, not abstract.
- [ ] CTA matches domain commercial role per `../../strategy/commercial-mapping.md`. No book-a-call ask on a top-of-funnel email.
- [ ] Draft saved to `{{VAULT_NAME}}/areas/content/emails/drafts/YYYY-MM-DD-{slug}.md` with complete frontmatter including `domain` and `pillar` (full drafts only; skip for sub-tasks like subject-line batteries).
- [ ] Saved path confirmed inline.
