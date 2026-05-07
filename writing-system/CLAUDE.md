---
title: Writing System — Operating Manual
type: context
tags:
  - writing-system
  - claude-md
  - skill-routing
created: {{DATE}}
updated: {{DATE}}
---

# Writing System — Operating Manual

This file is loaded automatically when an agent works inside `writing-system/`. It's the trigger-routing layer — pick the right skill fast, then drop into that skill's SKILL.md for full instructions.

For project status and roadmap, see [[../projects/writing-system/state.md]] and [[../projects/writing-system/plan.md]]. For vault-wide conventions, see [[../CLAUDE.md]].

---

## Architecture: toolbox, not pipeline

Each skill is **independently invocable**. There's no chained workflow with state files. {{VAULT_OWNER_SHORT_NAME}} (or whoever's driving) runs skills as needed and passes results between them manually. The only cross-skill contract is `used_material:` frontmatter on draft outputs — `suggest-topic` reads it from recent drafts to dedup topics whose anchor stories are exhausted.

```
research-topics ──writes──> content-graph/ideas/
                                    │
                                    │ (read)
                                    ▼
suggest-topic ──reads──> content-graph/ + areas/content/ + strategy/
                                    │
                                    │ (returns ranked topics in chat)
                                    ▼
                                {{VAULT_OWNER_SHORT_NAME}} picks one
                                    │
                                    ▼
   long-form-writing (phased)  ──or──  email-writing / landing-page-writing (inline)
                │                                          │
                ▼                                          ▼
   areas/content/newsletters/<list-name>/drafts/   areas/content/emails/drafts/   etc.
                │  (with used_material: frontmatter)      │
                └─────┬─────────────────────────────────────┘
                      ▼
            repurposing (Pattern C: propagate used_material:)
```

Substrate ingestion happens via `content-ingest` (manual-trigger transcripts/voice memos → takes & stories). Maintenance is `/lint` (vault-wide) — Phase 7 covers content-graph health.

---

## Skill triggers — quick reference

| Trigger phrase / slash command | Skill | Outputs to |
|---|---|---|
| "write a newsletter", "draft a long-form", "X article" | [`long-form-writing`](../.claude/skills/long-form-writing/SKILL.md) | `areas/content/newsletters/<list-name>/drafts/` or `areas/content/socials/x-articles/drafts/` |
| "draft a promo email", "welcome sequence", "subject line" | [`email-writing`](../.claude/skills/email-writing/SKILL.md) | `areas/content/emails/drafts/` |
| "landing page", "sales page", "hero copy", "offer page" | [`landing-page-writing`](../.claude/skills/landing-page-writing/SKILL.md) | `areas/content/landing-pages/drafts/` |
| "repurpose this", "turn this into a thread", "LinkedIn post version" | [`repurposing`](../.claude/skills/repurposing/SKILL.md) | `areas/content/socials/{platform}/drafts/` |
| "ingest this transcript", "process this voice memo", "/content-ingest" | [`content-ingest`](../.claude/skills/content-ingest/SKILL.md) | `content-graph/takes/`, `content-graph/stories/` |
| "/research-topics D1" (or D2/D3/D4), "/research-topics --pillar X", "/research-topics \"[seed]\"" | [`research-topics`](../.claude/skills/research-topics/SKILL.md) | `content-graph/ideas/` |
| "what should I write about", "/suggest-topic", "/suggest-topic D1", "/suggest-topic --pillar X" | [`suggest-topic`](../.claude/skills/suggest-topic/SKILL.md) | In-chat (ranked topics, no file written) |

Anything related to the knowledge wiki (people, companies, tools, concepts) belongs in [`/knowledge-ingest`](../.claude/skills/knowledge-ingest/), not `content-ingest`. See [[../CLAUDE.md]] for the layer split.

---

## Drafting-skill patterns

The four drafting skills extend differently for material assembly:

- **Pattern A — phased** (`long-form-writing` only). Five explicit phases: assemble material → draft headline options → draft piece → self-review → emit. {{VAULT_OWNER_SHORT_NAME}} can interject between phases. Brief is held in chat, not written to disk.
- **Pattern B — inline** (`email-writing`, `landing-page-writing`). Material assembly happens silently as part of the existing flow. Output includes 4 alternative subject lines / hero headlines.
- **Pattern C — propagation** (`repurposing`). Reads source piece's `used_material:` and copies forward into derivative outputs. Never re-queries the content-graph itself. Multi-source inputs union the lists.

All four emit `used_material:` frontmatter on output (list of wikilinks to `content-graph/` entries pulled in). Empty list (`used_material: []`) is valid.

---

## Cross-skill state contract: `used_material:`

The single shared field across all drafting skills. Lives in the draft's frontmatter:

```yaml
used_material:
  - "[[content-graph/stories/YYYY-MM-DD-example-story]]"
  - "[[content-graph/takes/YYYY-MM-DD-example-take]]"
  - "[[content-graph/receipts/example-receipt]]"
```

`suggest-topic` reads `used_material:` from drafts in:
- `areas/content/newsletters/<list-name>/drafts/` + `posts/`
- `areas/content/emails/drafts/`

<!-- per-vault: replace <list-name> with your actual newsletter folder names -->

Topics whose anchor stories/receipts are in this set within the last 90 days are demoted or suppressed. **No `used_in:` reverse field on stories** — the draft owns the link, not the source.

---

## Domain + pillar tagging

Every long-form draft tags `domain:` and `pillar:` in its frontmatter so cadence-aware suggestions work and so `repurposing` can apply per-domain platform restrictions.

- **Domains** (4): defined in [[strategy/domains.md]]. Use the slug verbatim in frontmatter.
- **Pillars** (per domain): canonical slugs in [[strategy/pillars.md]] Slug column. Use the slug verbatim in frontmatter.

If domain isn't obvious from the topic, ask the user — domain determines voice-frame nuance and CTA selection per [[strategy/voice-frame.md]].

---

## Cadence (per domain, yearly target)

<!-- per-exec; see strategy/cadence.md (populated by /content-strategy-onboard) -->

| Domain | Target | Channel |
|---|---|---|
| D1 — (your first content domain) | per cadence.md | per distribution.md |
| D2 — (your second content domain) | per cadence.md | per distribution.md |
| D3 — (your third content domain) | per cadence.md | per distribution.md |
| D4 — (your fourth content domain) | per cadence.md | per distribution.md |

`suggest-topic` no-args mode reads recent publish history per domain and weights output toward the lagging domain. Full cadence rules: [[strategy/cadence.md]]. Distribution rules: [[strategy/distribution.md]].

---

## Required loading per skill

Every drafting skill loads these before writing:

1. [[voice.md]] — voice signature
2. [[audience/<primary>.md]] or [[audience/<secondary>.md]] — depending on target audience
3. [[kill-list.md]] — universal banned patterns
4. [[_reference/drafting-feedback.md]] — standing instructions
5. [[strategy/voice-frame.md]] — per-domain voice nuance + per-domain kill-list additions
6. [[engine/hooks.md]], [[engine/frameworks.md]], [[engine/techniques.md]] — rhetorical primitives
7. [[engine/cta-patterns.md]] — CTA library (channel + domain-aware)
8. One channel file from [[channels/]] — channel-specific rules

Then the channel-specific extension (Pattern A/B/C) applies per the section above.

---

## Key references

- **Voice + audience:** [[voice.md]], [[kill-list.md]], [[audience/]], [[_reference/drafting-feedback.md]]
- **Strategy:** [[strategy/]] — domains, pillars, audience-mapping, commercial-mapping, cadence, distribution, voice-frame
- **Engine:** [[engine/]] — hooks, frameworks, techniques, cta-patterns, editorial-filter, repurpose chain
- **Channels:** [[channels/]] — per-channel format and convention
- **Content graph:** [[content-graph/README.md]] — node types, frontmatter contracts, cross-reference protocol
- **Index:** [[index.md]] — full node map of the writing-system

---

## When in doubt

- For a draft request → start with the relevant drafting skill; it'll load everything it needs.
- For a topic question → `suggest-topic` (asks "what should I write about?") or `research-topics` (asks "what's trending in this domain?").
- For new material → `content-ingest` for transcripts/voice memos/pasted text; `research-topics` for external trends.
- For maintenance → `/lint` Phase 7 covers content-graph health.

If still unclear, surface the ambiguity to the user before drafting. The system rewards specificity over assumption.
