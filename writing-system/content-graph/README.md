---
title: Content Graph
type: note
tags:
  - writing-system
created: {{DATE}}
updated: {{DATE}}
---

# Content Graph

> The structured material library for {{VAULT_OWNER_SHORT_NAME}}'s writing. Holds their takes, stories, ideas, topics, receipts, and quotes as a knowledge graph in plain markdown with wikilinks. Loaded by writing skills at draft time. Single source of voice-bearing material across the entire content engine.

---

## What this is (and isn't)

The content graph is **{{VAULT_OWNER_SHORT_NAME}}'s voice material indexed for retrieval.** It holds:

- What {{VAULT_OWNER_SHORT_NAME}} **thinks** (takes)
- What {{VAULT_OWNER_SHORT_NAME}} has **witnessed or experienced** (stories)
- What's **happening in the market** {{VAULT_OWNER_SHORT_NAME}} should write about (ideas)
- The **connective tissue** that ties the above to topics they keep returning to (topics)
- The **specific proof points** they cite (receipts)
- The **borrowed wisdom** they attribute to others (quotes)

This is **not** a wiki of facts about the world. That's `{{VAULT_NAME}}/knowledge/`. The two graphs serve different purposes and the distinction matters.

---

## Three layers of the brain

The {{VAULT_NAME}} vault has three layers. Each answers a different question:

| Layer | Location | Answers | POV |
|---|---|---|---|
| **Context** | `{{VAULT_NAME}}/context/` | Who is {{VAULT_OWNER_SHORT_NAME}} / what is their company? | Identity, slow-changing |
| **Knowledge** | `{{VAULT_NAME}}/knowledge/` | What is X? How does Y work? | Third-person, citable, world facts |
| **Content** | `writing-system/content-graph/` | What does {{VAULT_OWNER_SHORT_NAME}} SAY about X? | First-person, voice-rich, drafting material |

**The test:** *"Knowledge answers what something IS. Content answers what {{VAULT_OWNER_SHORT_NAME}} SAYS about it."*

If {{VAULT_OWNER_SHORT_NAME}} is the source (transcript, voice memo, observation), it's content. If it's a synthesized fact about the world, it's knowledge. Information can flow content-graph → knowledge over time when a take matures into a concept worth synthesizing. The reverse never happens.

---

## Structure

```
content-graph/
├── README.md            ← this file
├── _run-log.md          ← when each ingestion source last ran
├── takes/               ← {{VAULT_OWNER_SHORT_NAME}}'s perspectives (1–3 sentences)
│   ├── _index.md
│   └── YYYY-MM-DD-{slug}.md
├── stories/             ← narrative-ready experiences (Setup → Turning Point → Resolution → Lesson)
│   ├── _index.md
│   └── YYYY-MM-DD-{slug}.md
├── ideas/               ← market trends, external signals
│   ├── _index.md
│   └── YYYY-MM-DD-{slug}.md
├── topics/              ← connective tissue: drafting-optimized topic pages
│   ├── _index.md
│   └── {topic-slug}.md
├── receipts/            ← atomic citable proof points (no date prefix; reusable)
│   ├── _index.md
│   └── {descriptive-slug}.md
└── quotes/              ← borrowed wisdom {{VAULT_OWNER_SHORT_NAME}} cites (with attribution)
    ├── _index.md
    └── {author-slug}-{keyword}.md
```

---

## Node types

Six node types. Each has a frontmatter contract and a body template. Skills query the graph by node type, by tag, and by wikilink traversal.

### 1. Takes — {{VAULT_OWNER_SHORT_NAME}}'s perspectives

A take is a 1–3 sentence perspective {{VAULT_OWNER_SHORT_NAME}} holds, sourced from a real transcript, voice memo, or observation. Tagged by topic. The atomic unit of voice.

**Filename:** `takes/YYYY-MM-DD-{slug}.md` (date stated; slug 3–6 words from the take's core idea)

**Frontmatter:**
```yaml
---
title: "Brief title of the take"
type: knowledge
subtype: content-take
tags:
  - leadership
  - delegation
date: YYYY-MM-DD
source: "Source title or session name"
source_link: "[[meetings/YYYY-MM-DD-source]]"
topics:
  - "[[content-graph/topics/leadership]]"
related_takes: []
related_stories: []
private: false
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Body template:**
```markdown
**Take.** {{VAULT_OWNER_SHORT_NAME}}'s perspective in 1–3 sentences.

**Quote.** Verbatim if available, or `—`.

**Context.** What prompted this in 1 sentence.
```

### 2. Stories — narrative experiences

A story is a narrative-ready account of something {{VAULT_OWNER_SHORT_NAME}} witnessed or experienced, structured as Setup → Turning Point → Resolution → Lesson. Used as the anchor for long-form pieces. Stories are the load-bearing material in newsletters.

**Filename:** `stories/YYYY-MM-DD-{slug}.md`

**Frontmatter:**
```yaml
---
title: "Brief title of the story"
type: knowledge
subtype: content-story
tags:
  - delegation
  - zone-of-genius
date: YYYY-MM-DD
source: "Source title or session name"
source_link: "[[meetings/YYYY-MM-DD-source]]"
narrator: first-person  # or third-person-retelling
characters:
  - "{{VAULT_OWNER_SHORT_NAME}}"
  - "Other Person"
topics:
  - "[[content-graph/topics/delegation]]"
related_takes: []
related_stories: []
related_receipts: []
evergreen: true
usable_for: both  # primary | secondary | both (matches your audience segments)
private: false
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Body template:**
```markdown
## Setup
The situation in 2–3 sentences.

## Turning point
The moment of realization in 1–2 sentences.

## Resolution
What happened next in 2–3 sentences.

## Lesson
The takeaway in 1 sentence.

## Key quote
The most powerful direct quote, or `—`.
```

### 3. Ideas — market trends

An idea is a trend, signal, or external piece of news worth writing about. Comes from external research, news feeds, or things {{VAULT_OWNER_SHORT_NAME}} spots. Has a relevance angle filtered through `engine/editorial-filter.md`.

**Filename:** `ideas/YYYY-MM-DD-{slug}.md`

**Frontmatter:**
```yaml
---
title: "Brief title of the trend"
type: knowledge
subtype: content-idea
tags:
  - ai-agents
  - general-trends
date_found: YYYY-MM-DD
source: "Publication or source name"
source_url: "https://example.com/article"
angles:
  - primary   # matches your audience segments
  - secondary
topics:
  - "[[content-graph/topics/ai-agents]]"
related_topics: []
private: false
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Body template:**
```markdown
## Trend
What's happening in 2–3 sentences.

## Relevance
Why this matters for your audience in 1–2 sentences.

## Content opportunity
How to use this in 1–2 sentences. Hook angle, story angle, framework angle.
```

### 4. Topics — connective tissue

A topic page is the **single drafting entry point** for everything content-graph holds about a subject {{VAULT_OWNER_SHORT_NAME}} keeps returning to. Skills load a topic page first when assembling material for a piece. The topic page does the curation work so skills don't have to query 5 folders separately.

**Filename:** `topics/{topic-slug}.md` (slug matches the tag name)

**Frontmatter:**
```yaml
---
title: "Topic name"
type: knowledge
subtype: content-topic
tags:
  - <topic-slug>
linked_knowledge: "[[knowledge/concepts/<concept-name>]]"  # if equivalent knowledge page exists; null otherwise
related_topics: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Body template:**
```markdown
> For the canonical definition of <topic>, see [[knowledge/concepts/<topic>]] if it exists.
> This page is drafting-optimized scaffolding, not a definition.

## {{VAULT_OWNER_SHORT_NAME}}'s recurring framings
How {{VAULT_OWNER_SHORT_NAME}} talks about this topic. The phrases they reach for. The frame.

## Best opening hooks for pieces on this topic
- Hook 1 — [[content-graph/quotes/<quote-slug>]] or fresh framing
- Hook 2

## Receipts to cite
- [[content-graph/receipts/<receipt-slug>]]

## Stories that anchor it
- [[content-graph/stories/<story-slug>]]

## Takes worth pulling
- [[content-graph/takes/<take-slug>]]

## Quotes worth citing
- [[content-graph/quotes/<quote-slug>]]

## Published pieces about this topic
- [[areas/content/newsletters/.../<piece>]]

## Open questions
Questions {{VAULT_OWNER_SHORT_NAME}} keeps returning to but hasn't fully answered. Each one is a future piece in waiting.
- ...
```

### 5. Receipts — atomic proof points

A receipt is a standalone-citable proof point — a specific number, dollar amount, timeline, or named outcome. Reusable across pieces. Different from stories: stories carry narrative; receipts are the quotable line.

**Filename:** `receipts/{descriptive-slug}.md` (no date prefix; receipts are evergreen atoms)

**Frontmatter:**
```yaml
---
title: "Descriptive title of the receipt"
type: knowledge
subtype: content-receipt
tags:
  - <topic-tags>
metric: "What this measures"
value: "$150K → $0"
timeframe: "Two weeks"
source_story: "[[content-graph/stories/<story-slug>]]"
topics:
  - "[[content-graph/topics/<topic>]]"
usable_for: both
private: false
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Body template:**
```markdown
## Receipt
The exact citable line:
> "$150K → $0 in two weeks."

## Context
Where this came from in 1–2 sentences. Wikilink to the source story.

## Variations
Different forms for different channels:
- Long form: "One client replaced their $150K software stack with custom AI-built tools in two weeks."
- Short form: "$150K → $0 in two weeks."
- Tweet form: "1 exec, 14 days, $150K saved."
```

### 6. Quotes — borrowed wisdom (with attribution)

A quote is something someone else said that {{VAULT_OWNER_SHORT_NAME}} uses in their writing, with attribution. Distinct from `_reference/swipe-file/` because quotes are *citation-ready fragments* indexed by topic, not full source pieces.

**Filename:** `quotes/{author-slug}-{keyword}.md` (e.g., `dan-koe-mind-game.md`, `garry-tan-resolver-management.md`)

**Frontmatter:**
```yaml
---
title: "Quote teaser — first words or topic"
type: knowledge
subtype: content-quote
tags:
  - <topic-tags>
author: "Author Name"
author_handle: "@handle"
source_url: "https://x.com/..."
source_title: "Source title"
source_link: "[[clippings/source-title]]"
topics:
  - "[[content-graph/topics/<topic>]]"
private: false
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

**Body template:**
```markdown
## Quote
> Verbatim quote, exactly as the author wrote it.

— [Author Name](source_url), *source title*

## Context
Where in the source, what it's about, why {{VAULT_OWNER_SHORT_NAME}} would cite it.

## How {{VAULT_OWNER_SHORT_NAME}} uses it
What kind of pieces this lands in. What angle it supports.
```

---

## Tag taxonomy

Tags are the categorization layer. Topics are tags that have earned full topic pages. Every entry must have at least one tag.

**Start with a starter taxonomy** relevant to your niche, then grow organically. When new entries don't fit any existing tag, propose a new one. Tags don't become topics until they accumulate enough material to warrant a page.

<!-- per-vault: populate this taxonomy with tags matching your content domains and pillars -->

Plus one ideas-only tag: `general-trends` (for trends that don't fit other categories).

**The taxonomy grows organically.** When new entries don't fit any existing tag, propose a new one. Tags don't become topics until they accumulate enough material to warrant a page.

---

## Wikilink patterns

Every entry has at least one outgoing wikilink. Otherwise it's an orphan and won't be discoverable.

**From takes:** topics, source, related takes, stories the take appears in.

**From stories:** topics, source, characters (if entity pages exist in knowledge/), related takes, related stories, published pieces using this story.

**From ideas:** source URL (external), relevance angle, related topics, takes/stories the trend intersects.

**From topics:** linked knowledge page (if applicable), related topics. Incoming wikilinks from takes/stories/ideas/receipts/quotes accumulate via Obsidian backlinks — no need to maintain manually.

**From receipts:** source story, topics.

**From quotes:** source clipping (in `{{VAULT_NAME}}/clippings/`), source URL (external), topics.

---

## Cross-reference protocol with knowledge/ and context/

The three layers are separate but linked. Rules:

1. **Knowledge graph is canonical** for "what something is." If `knowledge/concepts/<topic>.md` exists, it's the definition.
2. **Content graph is canonical** for "what {{VAULT_OWNER_SHORT_NAME}} says about something." Topic pages, takes, stories, etc.
3. **Topic pages wikilink OUT** to knowledge/ pages instead of duplicating definitions. Example:
   ```markdown
   > For the canonical definition of <topic>, see [[knowledge/concepts/<topic>]].
   > This page is drafting-optimized scaffolding.
   ```
4. **No duplicate definitions.** If a definition exists in knowledge/, don't restate it in content-graph.
5. **Information flow is mostly one-way.** Content-graph → knowledge/ when a take or story matures into a synthesized concept worth treating as a knowledge entry. Knowledge → content-graph never; knowledge stays canonical.
6. **Context** (`{{VAULT_NAME}}/context/`) is identity. Both graphs reference it. Neither owns it.

**Concrete example:**

- `knowledge/concepts/<topic>.md` — definition: what the concept is, origin, mechanics.
- `content-graph/topics/<topic>.md` — {{VAULT_OWNER_SHORT_NAME}}'s content angle: best opening hooks, receipts to cite, stories that anchor pieces, published pieces, open questions.

These are sibling pages serving different purposes. They wikilink to each other. They don't compete.

---

## How skills query the graph

Different skills load the graph in different ways:

- **Graph search (native):** There is no standalone `graph-search` skill. Graph search is native Claude behavior — Read, Grep, and Glob on markdown files — embedded directly in each drafting skill's "Load first" pattern. Drafting skills navigate to the relevant `topics/<slug>.md` page and follow its wikilinks to reach takes, stories, receipts, quotes, and ideas.
- **`suggest-topic`:** loads `topics/_index.md`, `ideas/`, and `used_material:` frontmatter from recent drafts (last 90 days). Suggests ranked topics per audience. Suppresses topics whose anchor stories or receipts have been recently used (dedup via `used_material:` — see below).
- **`research-topics`:** populates `content-graph/ideas/` from external signals (market trends, conversations, recent events). Writes new idea entries; does not touch other node types.
- **Drafting skills (`long-form-writing`, `email-writing`, `landing-page-writing`, `repurposing`):** query the graph directly via topic page wikilinks. Emit `used_material:` on every output draft (see below).

**Topic pages are the primary skill-query interface.** Optimize them for skill consumption: clear sections, accurate wikilinks, curated rather than exhaustive.

### Reverse-link contract: `used_material:` on drafts

Every draft produced by a drafting skill carries a `used_material:` frontmatter field listing the content-graph entries the draft drew from.

```yaml
used_material:
  - "[[writing-system/content-graph/takes/2026-04-01-example-take]]"
  - "[[writing-system/content-graph/stories/2026-02-17-example-story]]"
  - "[[writing-system/content-graph/receipts/example-receipt]]"
```

**Rules:**

- **Scope:** wikilinks to takes, stories, receipts, quotes, and ideas that materially shaped the draft. Do not list topic pages — topic pages are navigational, not source material.
- **Empty list is valid.** `used_material: []` is correct for a draft written purely from prompt with no graph material pulled in.
- **`repurposing` skill:** propagates `used_material:` forward from the source piece rather than re-querying the graph. The repurposed piece inherits the original's material provenance.
- **No `used_in:` on stories.** There is no reverse field on story or take pages. The draft carries the link; the source does not.
- **`suggest-topic` reads this field** from all drafts in the last 90 days to suppress topics whose anchor stories or receipts are recently exhausted. This is the only dedup mechanism in the system.
- **Draft paths** follow existing canonical locations (e.g., `{{VAULT_NAME}}/areas/content/newsletters/<list-name>/drafts/` while in progress, `{{VAULT_NAME}}/areas/content/newsletters/<list-name>/posts/` after manual publish, `{{VAULT_NAME}}/areas/content/emails/`). The `used_material:` field lives in each draft's frontmatter at that path.

---

## Privacy

Entries with confidential client info, financial details, or personal material set `private: true` in frontmatter. Drafting skills filter out private entries when generating public-facing copy (newsletters, public emails, social posts). Private entries stay accessible for internal docs (sales-call talking points, internal memos, briefs to the team).

When in doubt: mark private. Cheap to flip later. Painful to leak.

---

## Maintenance

The content graph grows automatically via ingestion skills:

- `content-ingest` — Recordings + voice memos → takes & stories.
- `research-topics` — `last30days` (aggregates Reddit, X, YouTube, TikTok, Hacker News, Polymarket, GitHub, web) → ideas.

It stays clean via:

- `/lint` Phase 7 (Content Graph Health) — on-demand maintenance: detects stale entries (frontmatter `updated` older than threshold), orphan nodes (no wikilinks), broken wikilinks, missing frontmatter fields, untagged entries, topics without supporting takes/stories. Reports for manual review. **No automatic deletion** — use lint instead.
- Manual curation when topics need pages, when receipts need to be promoted from stories, when quotes are added from clippings.

Frontmatter `updated:` field tracks currency. Optional `stale: true` flag can be added during lint review.

---

## Naming conventions

| Node type | Filename pattern | Example |
|---|---|---|
| Takes | `YYYY-MM-DD-{slug}.md` | `2026-04-23-no-guardrails-in-my-life.md` |
| Stories | `YYYY-MM-DD-{slug}.md` | `2026-02-17-bridge-week-discovery.md` |
| Ideas | `YYYY-MM-DD-{slug}.md` | `2026-04-29-ai-skill-marketplace.md` |
| Topics | `{topic-slug}.md` | `maker-day.md`, `ai-operator.md` |
| Receipts | `{descriptive-slug}.md` | `client-90-percent-saas-savings.md` |
| Quotes | `{author-slug}-{keyword}.md` | `dan-koe-mind-game.md`, `garry-tan-resolver-management.md` |

Slugs are lowercase kebab-case. 3–6 words. Date-prefixed for time-stamped capture (takes/stories/ideas); descriptive-only for evergreen reusable units (topics/receipts/quotes).

If two entries collide on the same date and slug, append `-v2`, `-v3`. Don't overwrite.

---

## Quick reference

When creating a new entry, ask:

1. **Is {{VAULT_OWNER_SHORT_NAME}} the source?** → Content graph (this directory).
2. **Is this a fact about the world {{VAULT_OWNER_SHORT_NAME}} learned?** → Knowledge graph (`{{VAULT_NAME}}/knowledge/`).
3. **Is this about {{VAULT_OWNER_SHORT_NAME}}'s identity or their company's identity?** → Context (`{{VAULT_NAME}}/context/`).

Within content graph, ask:

| Question | Node type |
|---|---|
| Is this a 1–3 sentence perspective? | takes |
| Is this a narrative experience with Setup→Turning Point→Resolution→Lesson? | stories |
| Is this a market trend or external signal worth writing about? | ideas |
| Is this a topic they keep returning to, where I want to consolidate everything in one drafting-optimized place? | topics |
| Is this a standalone-citable proof point that will be reused? | receipts |
| Is this a verbatim quote from someone else with attribution? | quotes |
