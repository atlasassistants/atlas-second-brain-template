---
title: "The Agent Harness We Had to Build Before the Models Started Mattering"
type: area
tags:
  - newsletter
  - from-the-build
  - sample-exec
  - ai-native-infra
  - agent-harness-design
newsletter: from-the-build
domain: ai-native-infra
pillar: agent-harness-design
published_date: 2026-05-06
created: 2026-05-06
updated: 2026-05-06
used_material: []
status: published
---

# The Agent Harness We Had to Build Before the Models Started Mattering

We shipped our first real agent harness six weeks ago. Not the demo version — the one we use internally for every meaningful build task now.

Here's what changed: nothing about the models. Same Claude we'd been running. Same Cursor sessions. What changed was that we stopped letting the agents pick their own jobs and started defining the jobs for them.

I know this sounds like every founder essay about process being the answer. Stay with me — the receipt is specific.

---

## What we had before

Six months ago, our AI tooling looked like what most teams have: a chat window for research, Cursor for code generation, a few custom prompts we called "agents" in Slack because it made us feel advanced. Engineers were genuinely faster as individuals. Our shipped-per-sprint number looked better in reporting.

What the reporting missed: the output of one tool wasn't feeding the next. A Claude-written spec had to be manually pasted into Cursor context. Cursor-generated code had to be manually reviewed against a style guide nobody kept current. The test suite ran fine but coverage wasn't mapped back to the parts of the codebase actually changing. Every tool was producing artifacts. None of the artifacts were talking to each other.

The hard part isn't that AI tools are bad. It's that they're discrete. Each one is doing its job. Nobody told them they had a job *within the system.*

---

## What a harness actually is

I want to be concrete here because this word gets used loosely.

A harness, in our definition, is the scaffolding that gives an agent:

- A defined input format (what it receives)
- A defined output format (what it produces)
- A defined scope of authority (what decisions it can make vs. what it must flag)
- A handoff contract (where its output goes and in what shape)

That's it. It's not a new model. It's not a specialized AI service. It's just engineering — the same discipline you'd apply to a service boundary in your backend.

The moment we wrote down those four things for each agent we were running, the compound effect we'd been chasing showed up.

---

## The first harness that actually held

Here's the one that changed how I think about this.

We were using Claude to write first-pass specs for new features. Good drafts. But they were unstructured — sometimes long, sometimes missing the technical constraints, always requiring substantial engineer rewrite before they were useful. An engineer would take a Claude spec, read it, throw out half of it, and write the actual spec themselves. Net time saved: maybe 20%. Mostly just felt faster because the blank-page problem was gone.

We wrote a harness for the spec-writing agent. Input: the user story, the relevant existing API contracts (pulled automatically from a script that reads our OpenAPI spec), and the last three related specs we'd shipped (pulled from a vector search over our spec archive). Output: a spec in a rigid template our engineers had designed — problem statement, constraints, acceptance criteria, and a section called "what the agent is not deciding" (scope limits, explicit exclusions). Scope of authority: the agent can make implementation suggestions, but anything touching the data model goes into the "flag for review" section automatically.

The rewrite rate dropped from ~70% to ~20% in the first two weeks. The receipt is the PR comments — before the harness, engineers would gut the Claude spec in their first PR; after, the comments were refinements, not rewrites.

---

## The skeptic case (and why it's half right)

The obvious objection: you're just writing better prompts. If you're disciplined about prompting, you get the same outcome without all this "harness" framing.

The first part is true. A well-structured prompt with good context produces better output. Not new.

Here's what the prompt-only view misses: prompts live in chat windows. Harnesses live in the build system. A prompt is a personal practice. A harness is an infrastructure decision — something another engineer can run, version, and improve without the original author explaining it. The spec-writing harness is checked into the repo. When a new engineer joins, they don't need to learn my prompting style. They run the harness.

That's the compounding part. The knowledge transfers because it's in the system, not in someone's head.

---

## What we're still figuring out

The harnesses that compound are the ones where output is deterministic enough to serve as reliable input. Some agents aren't there yet — we have a PR review agent that produces useful observations but in a format too variable to automate into the next step. We haven't solved that. We're running it as a human-review output for now and watching whether the format stabilizes.

The open question: how many harnesses is too many? At some point the harness infrastructure becomes its own maintenance surface. I don't have a number. My current heuristic is that a harness is worth building when you're running the same agent task more than twice a week on predictably structured inputs. Working for now. Not confident it survives another 6 months of scale.

That's the piece I'm still building.

— Sarah

---

*From The Build is Gridline's biweekly newsletter on AI-native engineering infrastructure. If someone forwarded this, you can subscribe at gridline.build.*
