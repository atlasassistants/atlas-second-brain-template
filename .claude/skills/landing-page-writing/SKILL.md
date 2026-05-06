---
tags:
- content
created: '{{DATE}}'
updated: '{{DATE}}'
name: landing-page-writing
description: Use this skill whenever writing landing page, sales page, or offer page copy for {{VAULT_OWNER_SHORT_NAME}}'s services. Activate on any task that involves drafting heroes, sub-heads, problem-framing sections, proof blocks, pricing sections, FAQ copy, or full page layouts. Enforces {{VAULT_OWNER_SHORT_NAME}}'s voice, audience language, landing-page frameworks, and kill list. Trigger even on small tasks like a single hero line or section heading.
title: Landing page writing skill
type: note
---

# Landing page writing skill

## Load first — every time, before writing anything

Read these files in order:

1. `../../voice.md` — {{VAULT_OWNER_SHORT_NAME}}'s voice signature
2. `../../audience/<primary>.md` — primary audience
3. `../../kill-list.md` — universal kill list (AI fingerprints, banned patterns)
4. `../../_reference/drafting-feedback.md` — standing instructions (kill-list extension; living)
5. `../../strategy/voice-frame.md` — **per-domain voice nuances + per-domain kill-list additions.** Most landing pages belong to the primary commercial domain. See `../../strategy/distribution.md` for which domains get landing pages.
6. `../../engine/hooks.md` — hook formula library
7. `../../engine/frameworks.md` — pick one framework per page
8. `../../engine/techniques.md` — granular rhetorical moves within frameworks
9. `../../engine/cta-patterns.md` — CTA library
10. `../../channels/landing-page.md` — landing-page-specific format rules
11. `../../content-graph/README.md` — read the "How skills query the graph" section. Before drafting, search the graph for relevant takes/stories/receipts/quotes that anchor the page's claims and proof points. Pull what fits. Track every wikilink pulled — these populate `used_material:` in the output frontmatter.

These override default writing habits. The shared layer wins on voice, audience, and kill list. The strategy layer adds per-domain nuance on top. The channel file wins on landing-page structure.

After drafting, run the page against the **Top 5 highest-violation patterns** at the top of `kill-list.md` before output.

---

## What this skill does

Generates landing page / sales page / offer page copy:

- Service overview pages
- Long-form sales pages
- Single-offer or waitlist pages
- Hero sections
- Individual sections (problem framing, anti-pattern, proof, pricing, FAQ, final CTA)
- Single hero lines or section headings

For email copy, use `email-writing` skill.
For newsletters or long-form X articles, use `long-form-writing` skill.

---

## Process

**Material assembly is inline.** Before drafting hero + sections, search `../../content-graph/` for relevant takes/stories/receipts/quotes that anchor the offer. Pull what fits. The output's `used_material:` frontmatter captures every wikilink pulled. `used_material: []` is valid for pure-from-prompt drafts.

1. **Confirm intent.** Full page or single section? What's the offer or service the page sells?
2. **Confirm audience.** Default is primary audience. Could also be a specific sub-archetype — see `audience/<primary>.md`.
3. **Identify the domain.** Which content domain? Default is primary commercial domain for service/offer pages. Ask if not specified. See `../../strategy/domains.md`.
4. **Pick the framework** from `engine/frameworks.md`. Contrast-driven applies at the section level always; pick one whole-page framework on top.
5. **Draft section by section** following the skeleton in `channels/landing-page.md`. Apply the per-domain voice frame from `../../strategy/voice-frame.md`.
6. **Self-review** against the checklist below.
7. **Save the draft** to disk per the *Output* section below.
8. **Surface the draft inline** for immediate review and confirm the saved path.

For sub-tasks that don't produce a full page (a single hero line, a single section, an FAQ block), skip the save step and surface inline only. The save step applies to full page drafts.

---

## Output

### Where full drafts save

```
{{VAULT_NAME}}/areas/content/landing-pages/drafts/YYYY-MM-DD-{slug}.md
```

- `YYYY-MM-DD` is today's date.
- `{slug}` is a lowercase kebab-case version of the offer or service name. 4–8 words.

If the same date already has a draft with the same slug, append `-v2`, `-v3`, etc. Don't overwrite.

### Frontmatter

```yaml
---
title: "<page H1 / hero headline>"
type: area
tags:
  - landing-page
  - draft
  - <offer-tag>           # per-vault: tag for this offer/service
status: draft
offer: <offer-name>
domain: <domain>          # per your strategy/domains.md slugs
pillar: <pillar-slug>     # per your strategy/pillars.md Slug column
audience_archetype: <archetype>  # per audience/<primary>.md sub-archetypes
framework: <framework>    # contrast-driven | pas | bab | garry-tan | authority-moment
primary_cta: <type>       # book-a-call | direct-reply | see-pricing | see-system | community-enroll
length: <type>            # service-overview | long-form-sales | waitlist | hero-only
used_material: []         # wikilinks to content-graph entries pulled into this draft (empty list valid)
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
---
```

### Body format

After frontmatter, structure the page using these labeled section markers (helpful for reviewing and exporting to Webflow / Framer / wherever the page builds):

```markdown
## Hero

**Headline:** <hero headline>

**Subhead:** <subhead>

**CTA:** <button text>

---

## Problem framing

<copy>

---

## Anti-pattern (what they've tried)

<copy>

---

## The move

<copy>

---

## Proof / receipts

<copy>

---

## Pricing / packaging

<copy>

---

## FAQ / objections

**Q: <question phrased the way the audience phrases it>**
A: <answer>

(repeat for 5–7 questions)

---

## Final CTA

**Pullback:** <philosophical pullback above the button>

**CTA:** <button text — must match hero CTA>
```

### Alternative hero headlines

After the page body, list 4 alternative hero headlines to swap in.

### Inline output

After saving, surface the full page inline for immediate review. Always confirm the saved path:

> Saved to: `{{VAULT_NAME}}/areas/content/landing-pages/drafts/YYYY-MM-DD-{slug}.md`

---

## Self-review checklist (before output)

- [ ] Hero is audience-state + contrast, not a tagline.
- [ ] Subhead names the structural move, not features.
- [ ] Problem section pulls verbatim language from `audience/<primary>.md`.
- [ ] Anti-pattern section honors the effort the reader has already made (no *"you weren't trying hard enough"* energy).
- [ ] At least one specific named proof story with numbers, timelines, dollars.
- [ ] Pricing is direct and clear.
- [ ] FAQ questions are phrased the way the audience phrases them.
- [ ] No em dashes anywhere.
- [ ] Negative parallelism used at most once across the whole page.
- [ ] No bold-first bullets unless genuinely load-bearing.
- [ ] Final CTA matches hero CTA.
- [ ] Pullback above final CTA reframes meaning, doesn't cheerlead.
- [ ] No banned words / phrases / structures from `kill-list.md`.
- [ ] **Per-domain kill-list cleared.** See `../../strategy/voice-frame.md` for full per-domain kill items.
- [ ] CTA matches domain commercial role per `../../strategy/commercial-mapping.md`.
- [ ] Draft saved to `{{VAULT_NAME}}/areas/content/landing-pages/drafts/YYYY-MM-DD-{slug}.md` with complete frontmatter including `domain` and `pillar` (full pages only; skip for sub-tasks like single hero lines).
- [ ] Saved path confirmed inline.
