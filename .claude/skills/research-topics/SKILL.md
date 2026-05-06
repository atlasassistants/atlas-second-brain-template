---
tags:
- writing-system
- research
- content-graph
created: '{{DATE}}'
updated: '{{DATE}}'
name: research-topics
description: Pull external trending content aligned with {{VAULT_OWNER_SHORT_NAME}}'s content strategy, score against the editorial filter, and write candidate ideas to content-graph/ideas/. Activate on triggers like "/research-topics D1" (domain-driven), "/research-topics --pillar <slug>" (pillar-narrowed), or "/research-topics \"[seed query]\"" (free-text exploratory). Operates as a thin layer on top of the last30days skill, scoring its output through editorial-filter v2 (domain fit + content quality) and writing the top candidates as new entries in content-graph/ideas/.
tools: Read, Write, Edit, Glob, Grep, Bash
title: Research Topics Skill
type: note
---

# Research Topics Skill

## Load first — every time, before researching

Read these files in order:

1. `../../engine/editorial-filter.md` — two-filter scoring (Filter 1 domain fit + Filter 2 content quality, six-criteria rubric)
2. `../../strategy/domains.md` — domain definitions (D1, D2, D3, D4 or per-vault equivalent)
3. `../../strategy/pillars.md` — pillars + which domain each belongs to
4. `../../content-graph/ideas/_index.md` — dedup against existing ideas (don't re-write a candidate that's already in the graph)
5. `../../content-graph/README.md` — idea entry frontmatter contract + tagging rules

---

## Triggers

- `/research-topics D1` (or other domain codes) — domain-driven sweep across all pillars in that domain
- `/research-topics --pillar <slug>` — pillar-narrowed within a domain
- `/research-topics "[seed query]"` — free-text exploratory research
- Optional flag on any mode: `--count N` (default 5)

---

## Workflow

1. **Resolve scope** from the trigger:
   - Domain mode → all pillars within that domain (per `strategy/pillars.md`).
   - Pillar mode → that pillar only.
   - Free-text mode → seed query as-is, no domain assumed.
2. **Invoke `last30days`** with scope-appropriate query/queries. For domain or pillar mode, generate one query per pillar (or per pillar facet) tuned to the pillar's content focus. For free-text mode, pass the seed through directly.
3. **Filter** returned items through editorial-filter v2:
   - **Filter 1 (domain fit):** Drop items that don't cleanly fit one of the defined domains. Free-text mode candidates that don't fit a domain are carried through with `domain: untagged` (see Free-text fallback below).
   - **Filter 2 (content quality):** Score each surviving candidate on the six-criteria rubric in the editorial filter (loaded above).
4. **Rank and select top N candidates** (default N=5, override via `--count`).
5. **Write each candidate** to `{{VAULT_NAME}}/writing-system/content-graph/ideas/YYYY-MM-DD-{slug}.md` per the existing idea contract (see `content-graph/README.md`). Tag each with proposed `domain:` and `pillar:` per editorial-filter scoring.
6. **Update** `{{VAULT_NAME}}/writing-system/content-graph/_run-log.md` with run metadata: timestamp, trigger, scope, count of candidates written, count untagged.
7. **Output run summary in chat** (see Output section below).

---

## Free-text fallback handling

When `/research-topics "[seed]"` returns candidates that don't cleanly map to any domain:
- Write them with `domain: untagged` (mirroring `content-ingest`'s untagged pattern).
- Surface them under "Untagged candidates — manual review needed" in the chat run summary.
- Never silently drop a candidate. Always write with surfacing.

---

## Output

### Per-candidate file at `content-graph/ideas/YYYY-MM-DD-{slug}.md`

Frontmatter follows the existing idea contract from `content-graph/README.md`. Score and editorial-filter reasoning do **not** go into the file — they live only in the chat run summary and the `_run-log.md` entry.

### Chat run summary format

```markdown
# Research Topics Run — {timestamp}

**Trigger:** /research-topics <args>
**Scope:** <resolved scope>
**Source:** last30days ({list of platforms hit})

## Candidates written (N)

### 1. <Title>
- **Domain:** <domain code> — <domain name>
- **Pillar:** <pillar-slug>
- **Score:** 5/6 (clears domain fit + 4 of 6 quality criteria; missing strong story anchor)
- **Signal sources:** Reddit (3 posts), X (2 threads)
- **Path:** `content-graph/ideas/YYYY-MM-DD-{slug}.md`

(repeat for each candidate)

## Untagged candidates (M)
(only present in free-text mode when domain fit fails)

### 1. <Title>
- **Reason untagged:** No clean fit to defined domains
- **Path:** `content-graph/ideas/YYYY-MM-DD-{slug}.md` (with domain: untagged)

## Run-log entry
Appended to: `content-graph/_run-log.md`
```

---

## Cross-skill relationships

- **Upstream:** `last30days` (existing skill) provides the raw signal substrate.
- **Downstream:** `suggest-topic` reads the ideas this skill writes when surfacing recommendations.
- **Sibling:** `content-ingest` is the manual analog — universal manual ingestion of transcripts/voice memos/pasted text into takes and stories. `research-topics` is the automated analog for ideas only.
- **Lint:** `/lint` Phase 7 (Content Graph Health) handles staleness on ideas this skill creates.

---

## Out of scope (v1)

- Perplexity / Composio integration (substrate is `last30days` only).
- RSS feed scraping or curated source lists.
- Periodic / scheduled invocation (manual-trigger only).
- Writing takes/stories (those come from `content-ingest`, not this skill).
