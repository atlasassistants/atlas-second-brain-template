---
tags:
- content
created: '{{DATE}}'
updated: '{{DATE}}'
name: content-ingest
description: Process transcripts, voice memos, meeting notes, or pasted text into structured takes and stories in `{{VAULT_NAME}}/writing-system/content-graph/`. Universal manual-trigger ingestion that accepts any input source — file path, wikilink, or pasted text. Decoupled from external services (Fathom, Otter, etc.) — automation pipes inputs to this skill, never the other way around. For ingestion into the knowledge graph (people, companies, tools, concepts, comparisons), use `/knowledge-ingest` instead.
tools: Read, Write, Edit, Glob, Grep, Bash
title: Content Ingest
type: note
---


> **Filing-rules mandate (from `RESOLVER.md`):** Before creating any new page, read `{{VAULT_NAME}}/RESOLVER.md` and file by primary subject. Content-graph nodes (takes, stories, ideas) live in `writing-system/content-graph/` — that is this skill's home. When extracting people or companies mentioned in voice material, route them to `knowledge/people/` or `knowledge/companies/` respectively, with typed `mentions` edges.

# Content Ingest

Process a source document (transcript, voice memo, meeting note, or pasted text) into {{VAULT_OWNER_SHORT_NAME}}'s content graph. Extracts takes (perspectives) and stories (narrative-ready experiences) and writes them to `writing-system/content-graph/takes/` and `writing-system/content-graph/stories/` matching the contracts in `writing-system/content-graph/README.md`.

For raw captures that become wiki-style facts, entities, concepts — use `/knowledge-ingest`. That skill writes to `{{VAULT_NAME}}/knowledge/`, not the content graph.

---

## Trigger

- **Manual file input:** `/content-ingest <path>` or *"ingest this transcript"* with file path or wikilink.
- **Manual paste input:** `/content-ingest` with pasted text in the prompt. Prompt should include a source descriptor like *"from my coaching call on 2026-04-30."*
- **Automation-driven:** A recording watcher, voice memo watcher, or other automation can invoke this skill on a file it just dropped. The skill itself doesn't fetch — automation fetches and points the skill at the result.

## Input

One of:

1. **File path** — absolute or vault-relative. Skill reads the file directly.
2. **Wikilink** — `[[meetings/YYYY-MM-DD-session]]` or similar. Skill resolves to the file path.
3. **Pasted text** — text in the invocation prompt, with a source descriptor (*"from my call on YYYY-MM-DD"*).

Single-file invocation only — one source per call. No batch mode.

---

## Workflow

### Phase 1: Identify source

Determine where the content is coming from. Three branches:

**Branch A — file path or wikilink given.**
- Resolve path. Read file.
- `source` = file's `title` from frontmatter (or filename if no frontmatter).
- `source_link` = wikilink to the file.

**Branch B — pasted text with source descriptor.**
- Parse source descriptor from prompt (*"from my call on YYYY-MM-DD"*).
- `source` = parsed source descriptor.
- `source_link` = empty (or a future wikilink if the user wants the text filed first — see Branch C).

**Branch C — pasted text without source descriptor (fallback).**
- Don't proceed silently. Either ask the user for a source descriptor, OR:
- Create a stub file at `{{VAULT_NAME}}/inbox/transcripts/YYYY-MM-DD-untitled.md` containing the pasted text with minimal frontmatter (title: "Untitled transcript", type: inbox, ingested: false, ingested_date: null, created: today, updated: today).
- `source` = "Untitled transcript YYYY-MM-DD"
- `source_link` = wikilink to the stub file.

### Phase 2: Load writing-system references

Before extraction, read the following so the skill writes contracts-compliant entries with appropriate voice/audience awareness:

1. `{{VAULT_NAME}}/writing-system/voice.md` — voice signature.
2. `{{VAULT_NAME}}/writing-system/audience/<primary>.md` and `audience/<secondary>.md` — audience profiles for tagging.
3. `{{VAULT_NAME}}/writing-system/kill-list.md` — universal kill patterns.
4. `{{VAULT_NAME}}/writing-system/_reference/drafting-feedback.md` — standing instructions.
5. `{{VAULT_NAME}}/writing-system/content-graph/README.md` — frontmatter contracts and tag taxonomy.

These inform what gets extracted and how it's tagged. They do NOT change what's faithfully captured from the source — voice extraction is about {{VAULT_OWNER_SHORT_NAME}}'s actual perspectives, not paraphrasing into the writing-system voice. Capture what was said.

### Phase 3: Read source

Read the entire input. For long transcripts, process top-to-bottom in one pass. Don't chunk artificially — the skill needs the full context to identify story arcs.

### Phase 4: Extract takes

A take is a 1–3 sentence perspective {{VAULT_OWNER_SHORT_NAME}} holds. Look for:

- Statements where {{VAULT_OWNER_SHORT_NAME}} asserts a position or belief.
- Reframes they offer against conventional wisdom.
- Contrarian observations they make.
- Crisp opinions they express about a topic.

For each take:

- **Title.** A brief, distinctive title that captures the take's core idea (3–8 words).
- **Take body.** 1–3 sentences in {{VAULT_OWNER_SHORT_NAME}}'s own words (paraphrased lightly if needed for clarity, but preserve the core voice).
- **Quote.** Verbatim if a clean direct quote exists; otherwise `—`.
- **Context.** 1 sentence explaining what prompted the take.
- **Tags.** Pick from the tag taxonomy in `content-graph/README.md`. Multiple tags okay if applicable. If no tag fits confidently, use `tags: - untagged` and surface in the run summary.

### Phase 5: Extract stories

A story is a narrative-ready experience {{VAULT_OWNER_SHORT_NAME}} witnessed or participated in. Must have a recognizable arc:

- **Setup** — the situation, 2–3 sentences.
- **Turning point** — the moment of realization or change, 1–2 sentences.
- **Resolution** — what happened next, 2–3 sentences.
- **Lesson** — the takeaway, 1 sentence.
- **Key quote** — the most powerful direct quote from the source, or `—`.

For each story:

- **Title.** A brief, evocative title (4–8 words).
- **Source, source_link** — same as Phase 1.
- **Narrator** — *"first-person"* if {{VAULT_OWNER_SHORT_NAME}} is in the story; *"retelling"* if {{VAULT_OWNER_SHORT_NAME}} is recounting someone else's experience.
- **Characters** — list of named people in the story.
- **Tags** — same rules as takes.
- **Evergreen** — `true` if the story doesn't lose relevance with time; `false` if it's tied to a specific moment that won't recur.
- **Usable for** — `primary` if it lands best in primary-audience content, `secondary` for secondary audience, `both` if either.

A single chunk of source can produce **both a take and a story** — a perspective stated, plus a story illustrating it. Don't force one or the other.

### Phase 6: Dedupe

For each new entry (take or story):

- Compute `{date}-{slug}` from the date and slug.
- Check if `content-graph/{takes|stories}/{date}-{slug}.md` already exists.
- If exact match: skip the entry, surface in the run summary as a dupe.
- If near-match (similar title, same date): flag as a possible dupe in the run summary, but write with a `-v2` suffix on the slug. Manual review later via `/lint`.

### Phase 7: Write entries

Write each entry as a separate markdown file matching the Phase 2 contracts in `content-graph/README.md`.

**Take filename:** `content-graph/takes/YYYY-MM-DD-{slug}.md`
**Story filename:** `content-graph/stories/YYYY-MM-DD-{slug}.md`

Slug: lowercase kebab-case, derived from the title. 4–6 words. 60-char max.

**Frontmatter must include all required fields per the contract in `content-graph/README.md`.** Don't omit fields — when a field is unknown, use empty list `[]` or empty string `""`, but include the field.

**Body must follow the contract template** for the node type (Take/Quote/Context for takes; Setup/Turning Point/Resolution/Lesson/Key Quote for stories).

**Typed `related:` entries.** When the take or story references named people, companies, or concepts, emit typed entries in the entry's `related:` frontmatter list. Use the typed-edge format from CLAUDE.md / RESOLVER.md:

```yaml
related:
  - link: "[[knowledge/people/<name>]]"
    type: mentions
  - link: "[[knowledge/companies/<name>]]"
    type: mentions
  - link: "[[knowledge/concepts/<name>]]"
    type: applies   # use `applies` if the take *uses* the concept; `mentions` if it's just referenced
```

If the referenced person, company, or concept doesn't yet have a knowledge page, still emit the wikilink — `/lint` will surface the broken link, and `/knowledge-ingest` can create the page later. Do NOT create the knowledge page from inside content-ingest; this skill's home is `writing-system/content-graph/`.

### Phase 8: Update run log

Append a row to `content-graph/_run-log.md`:

```
| {source} | YYYY-MM-DD | {N} takes / {M} stories | content-ingest | {brief notes if anything unusual} |
```

### Phase 9: Surface summary inline

Output a summary in the chat:

```
Content ingest complete from {source}.

Takes extracted: {N}
- {date}-{slug-1} — {title-1}
- {date}-{slug-2} — {title-2}
...

Stories extracted: {M}
- {date}-{slug-1} — {title-1}
- {date}-{slug-2} — {title-2}
...

Skipped as duplicates: {K}
- {date}-{slug} — already exists at {path}

Flagged for manual tagging (tags: - untagged): {J}
- {date}-{slug-1} — couldn't confidently tag from current taxonomy
- {date}-{slug-2} — same

Saved to: {{VAULT_NAME}}/writing-system/content-graph/
Run log updated: {{VAULT_NAME}}/writing-system/content-graph/_run-log.md
```

If anything was created via Branch C (stub file fallback), call out the stub file location explicitly.

---

## Rules

- **Never paraphrase voice into the writing-system voice.** This skill captures {{VAULT_OWNER_SHORT_NAME}}'s actual statements as takes/stories. The writing-system voice is for OUTPUT (drafts), not INPUT capture. Capture what was actually said.
- **Never invent stories.** If the transcript doesn't have a story arc (Setup → Turning Point → Resolution → Lesson), don't manufacture one. Just extract takes.
- **Never skip an entry due to ambiguous tagging.** Tag with `tags: - untagged` and surface for manual review. Material is precious; don't lose it.
- **Never overwrite existing entries.** If a date+slug collision exists, append `-v2`, `-v3`. Manual reconciliation via `/lint` later.
- **Never write to topics/, receipts/, or quotes/.** Those are curation jobs — manual or follow-up skills, not auto-extracted.
- **Never write knowledge pages.** Don't create files under `{{VAULT_NAME}}/knowledge/`. That's `/knowledge-ingest`'s job. Linking to knowledge pages from a take/story's `related:` (with typed edges) is fine — and expected — even if the target page doesn't exist yet.
- **Always wikilink the source.** Every entry has `source_link` filled (or pointing to the stub file in Branch C).
- **Always update the run log.** Even if the run produced 0 entries (e.g., the source was small talk with no extractable material), log the run with 0/0 counts.
- **Single source per invocation.** No batch mode in v1.

---

## Distinguishing takes from stories — quick reference

| Type | Shape | Length | Example trigger phrase |
|---|---|---|---|
| **Take** | Perspective, opinion, reframe | 1–3 sentences | *"The thing I keep saying is..."* / *"Most people think X but..."* / *"What actually matters is..."* |
| **Story** | Setup → Turning Point → Resolution → Lesson | Multi-paragraph arc | *"So [name] was..."* / *"Last week with [person]..."* / *"Two years ago I didn't know..."* |

When the source has both — which is common — extract both.

---

## Tag taxonomy reference

When tagging entries, pull from the tag taxonomy locked in `content-graph/README.md`.

<!-- per-vault: populate the tag taxonomy in content-graph/README.md with your niche-specific tags -->

If no tag confidently fits, use `tags: - untagged` and flag in run summary. Don't auto-create new tags — propose them in the summary, let the vault owner decide if a new tag should be added to the taxonomy.

---

## Cross-skill relationships

- **`/knowledge-ingest`** — sibling skill that ingests into the knowledge graph (entities, concepts, comparisons in `{{VAULT_NAME}}/knowledge/`). Same source might be ingested by both — `/knowledge-ingest` for facts about the world, `/content-ingest` for {{VAULT_OWNER_SHORT_NAME}}'s perspectives and stories. They don't conflict.
- **`/lint`** — surfaces duplicates, untagged entries, broken wikilinks, and other graph health issues that `/content-ingest` flagged.
- **Drafting skills** (`email-writing`, `long-form-writing`, etc.) — consume the takes/stories this skill produces. Don't call this skill; they read the graph.
