---
title: Writing System
type: note
tags:
  - writing-system
created: {{DATE}}
updated: {{DATE}}
---

# Writing System

{{VAULT_OWNER_SHORT_NAME}}'s personal writing system — voice, audience, kill list, frameworks, hooks, and channel playbooks for every writing surface.

Activates via Claude skills that load this knowledge graph before producing any copy.

## Layout

```
writing-system/
├── voice.md                     ← voice signature (the core)
├── kill-list.md                 ← banned patterns
├── audience/
│   ├── <primary>.md             ← primary ICP
│   └── <secondary>.md           ← secondary audience
├── engine/                      ← cross-channel logic
│   ├── hooks.md
│   ├── frameworks.md
│   ├── cta-patterns.md
│   ├── repurpose.md
│   └── scheduling.md
├── channels/                    ← per-format playbooks
│   ├── email.md
│   ├── landing-page.md
│   ├── newsletter.md
│   ├── x-article.md
│   ├── x-thread.md
│   ├── x-short.md
│   └── linkedin-post.md
├── content-graph/               ← voice material library
│   ├── README.md
│   ├── _run-log.md
│   ├── takes/
│   ├── stories/
│   ├── ideas/
│   ├── topics/
│   ├── receipts/
│   └── quotes/
├── strategy/                    ← what to write about
│   ├── README.md
│   ├── domains.md
│   ├── pillars.md
│   └── ...
├── examples/
│   ├── in-voice/                ← real drafts that pass review
│   └── out-of-voice/            ← anti-examples for contrast
├── _reference/
│   └── sources.md               ← pointers to swipe file, ICP doc, voice memos
├── index.md                     ← command center / knowledge map
└── README.md                    ← this file
```

## Skills

The skills in `.claude/skills/` activate the writing system:

- `email-writing` — promotional, broadcast, sequence emails
- `landing-page-writing` — service, sales, offer pages
- `long-form-writing` — newsletters and X long-form articles
- `repurposing` — long-form → X thread, X short, LinkedIn post
- `content-ingest` — transcripts/voice memos/pasted text → takes & stories
- `research-topics` — external trends → content-graph/ideas/
- `suggest-topic` — surfaces ranked topic recommendations (cadence-aware)

Each drafting skill loads `voice.md` + `audience/<primary>.md` + `kill-list.md` + relevant engine and channel files before drafting, then runs a self-review checklist before output.

## How it works

The pattern: a folder of interconnected markdown files where each file is one knowledge node, wikilinked to others. When a writing skill activates, it follows the links from its `SKILL.md` outward, reading the relevant nodes to build up complete context before writing a single word.

See `index.md` for the full knowledge map and execution instructions.

## Updating

Edit files in this directory directly. Skills pick up changes on the next invocation. No rebuild required.

When the voice evolves, edit `voice.md`. When new audience signal is captured, update or add audience files. When a new pattern surfaces in real copy, add it to `kill-list.md`.
