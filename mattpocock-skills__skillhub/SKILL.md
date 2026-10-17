---
name: mattpocock-skills__skillhub
slug: mattpocock-skills
version: 1.0.0
displayName: Matt Pocock's Skills
description: A disciplined engineering workflow for coding agents — grill before building, TDD with red-green slices, two-axis code review, bug diagnosis loops, issue triage, PRD/issue breakdown, domain modeling, and deep-module architecture improvement. Use when the user wants to "write tests first", "review this PR", "grill me on the plan", "triage issues", "debug this", "improve the architecture", "make a PRD", "split into issues", or otherwise do real (non-vibe) engineering. Triggers on TDD, code review, PRD, triage, diagnose/debug, domain model, ubiquitous language, prototype, architecture refactor, handoff.
summary: Matt Pocock 的「真工程师」技能集 —— 把成熟的软件工程纪律（对齐访谈、TDD、双轴代码评审、Bug 诊断循环、Issue 分诊、PRD/任务拆分、领域建模、深模块架构）浓缩成可复用的 Agent 工作流。
tags:
  - engineering
  - tdd
  - code-review
  - triage
  - debugging
  - architecture
  - domain-modeling
  - prd
  - workflow
  - mattpocock
license: MIT
homepage: https://github.com/mattpocock/skills
agent_created: true
---

# Matt Pocock's Skills

A collection of small, composable agent skills for **real engineering** — not vibe coding.
Ported from Matt Pocock's [skills repo](https://github.com/mattpocock/skills). Each skill is a
self-contained procedure; this file is the **router** that tells you which one to reach for and
how they connect. The full text of every skill lives in `references/`.

> **How to use in WorkBuddy.** This skill is the methodology. When the user's request matches a
> skill below, read that skill's file from `references/` and follow its procedure exactly. Most
> skills are "user-invoked" (the human asks for them) or "model-invoked" (reach for them
> automatically when the task fits). The labels are kept for clarity; WorkBuddy loads all of them.

---

## Why these skills exist

Four failure modes in agent-assisted development, and the skill that fixes each:

1. **The agent didn't do what I want** → misalignment. Fix: a **grilling** session
   (`/grill-me`, `/grill-with-docs`) before any code.
2. **The agent is too verbose** → no shared language. Fix: build a domain model
   (`/domain-modeling`) and keep `CONTEXT.md` as a glossary.
3. **The code doesn't work** → no feedback loop. Fix: **TDD** (`/tdd`) and disciplined
   **bug diagnosis** (`/diagnosing-bugs`).
4. **We built a ball of mud** → entropy. Fix: **deep-module design** (`/codebase-design`,
   `/improve-codebase-architecture`).

---

## The router: idea → ship (main flow)

The path most work travels. You have an idea and want it built.

1. **`/grill-with-docs`** — sharpen the idea by interview. Start here when you **have a codebase**:
   it's stateful, retaining what it learns in `CONTEXT.md` and ADRs. (No codebase? Use
   `/grill-me`.) Both run the same `/grilling` primitive; `grill-with-docs` leaves a paper trail.
   → [references/engineering/grill-with-docs/SKILL.md](references/engineering/grill-with-docs/SKILL.md)
   → [references/productivity/grill-me/SKILL.md](references/productivity/grill-me/SKILL.md)
   → [references/productivity/grilling/SKILL.md](references/productivity/grilling/SKILL.md)

2. **Branch — can you settle every question in conversation?** If a question needs a runnable
   answer (state, business logic, a UI you must see), detour through a prototype, bridged by
   `/handoff` in both directions:
   → `/handoff` out → `/prototype` → `/handoff` back.
   → [references/productivity/handoff/SKILL.md](references/productivity/handoff/SKILL.md)
   → [references/engineering/prototype/SKILL.md](references/engineering/prototype/SKILL.md)

3. **Branch — is this a multi-session build?**
   - **Yes** → `/to-prd` (turn the thread into a PRD) → `/to-issues` (split into independently-grabbable
     vertical slices). Then clear context between each issue: start a fresh session per issue and
     run `/implement` with the PRD + that one issue.
   - **No** → `/implement` right here, in the same window.
   → [references/engineering/to-prd/SKILL.md](references/engineering/to-prd/SKILL.md)
   → [references/engineering/to-issues/SKILL.md](references/engineering/to-issues/SKILL.md)
   → [references/engineering/implement/SKILL.md](references/engineering/implement/SKILL.md)

   Either way, `/implement` builds each issue by driving **`/tdd`** internally — one red-green slice at
   a time — then closes with **`/code-review`** (Standards + Spec) before committing. Use `/tdd` alone
   for a concrete behaviour, and `/code-review` alone to review a branch/PR.
   → [references/engineering/tdd/SKILL.md](references/engineering/tdd/SKILL.md)
   → [references/engineering/code-review/SKILL.md](references/engineering/code-review/SKILL.md)

**Context hygiene:** keep steps 1–3 in one unbroken context window until after `/to-issues`. Each
`/implement` then starts fresh from the issue. If the window approaches the "smart zone" (~120k
tokens) before `/to-issues`, `/handoff` and continue in a fresh thread.

---

## On-ramps

A starting situation that generates work, then merges onto the main flow.

- **Bugs and requests piling up** → `/triage`. Moves issues through triage roles and produces
  agent-ready issues that `/implement` later picks up. Triage is only for issues **you didn't
  create** (bug reports, incoming requests). Issues from `/to-issues` are already agent-ready.
  → [references/engineering/triage/SKILL.md](references/engineering/triage/SKILL.md)
- **Something's broken** → `/diagnosing-bugs`. For the hard ones: reproduces only with a tight
  feedback loop, then fixes with a regression test. Its post-mortem hands off to
  `/improve-codebase-architecture` when the real finding is "no good seam to lock the bug down".
  → [references/engineering/diagnosing-bugs/SKILL.md](references/engineering/diagnosing-bugs/SKILL.md)

---

## Codebase health

- **`/improve-codebase-architecture`** — run whenever you have a spare moment. Surfaces
  **deepening opportunities**; picking one *generates an idea* you can take into the main flow at
  `/grill-with-docs`. It's the survey that finds candidates; `/codebase-design` is the bench you
  design the chosen one on.
  → [references/engineering/improve-codebase-architecture/SKILL.md](references/engineering/improve-codebase-architecture/SKILL.md)

---

## Vocabulary underneath

Two model-invoked references that run *beneath* the other skills — each the single source of truth
for its vocabulary. Reach for them directly when the **words**, not the process, are the problem.

- **`/domain-modeling`** — sharpen the project's *domain* language: challenge a fuzzy term, resolve
  an overloaded word, record a hard-to-reverse decision as an ADR. The active discipline
  `/grill-with-docs` drives to keep `CONTEXT.md` a clean glossary.
  → [references/engineering/domain-modeling/SKILL.md](references/engineering/domain-modeling/SKILL.md)
- **`/codebase-design`** — the deep-module vocabulary (module, interface, depth, seam, adapter,
  leverage, locality) for designing a module's *shape*: a lot of behaviour behind a small interface
  at a clean seam. `/tdd` and `/improve-codebase-architecture` both speak it.
  → [references/engineering/codebase-design/SKILL.md](references/engineering/codebase-design/SKILL.md)

---

## Crossing sessions

- **`/handoff`** — compact the conversation into a markdown file; open a new session and reference
  it to carry context across. The bridge between windows, in either direction.
- **`/compact`** (built-in) — stay in the same conversation, letting earlier turns be summarized.
  Use at intentional phase breaks; don't compact mid-phase.

---

## Standalone

Off the main flow entirely.

- **`/grill-me`** — the relentless interview, but for when you have **no codebase**. Stateless.
- **`/prototype`** — a small, throwaway program that answers one design question. Throwaway from
  day one; keep the answer, delete the code.
- **`/research`** — delegate reading to a **background agent**: it investigates against **primary
  sources**, then leaves a cited Markdown file in the repo. Research feeds the thinking, doesn't
  replace it.
  → [references/engineering/research/SKILL.md](references/engineering/research/SKILL.md)
- **`/teach`** — learn a concept over multiple sessions, using the current directory as a stateful
  workspace.
  → [references/productivity/teach/SKILL.md](references/productivity/teach/SKILL.md)
- **`/writing-great-skills`** — reference for writing and editing skills well.
  → [references/productivity/writing-great-skills/SKILL.md](references/productivity/writing-great-skills/SKILL.md)

---

## Precondition: setup

**`/setup-matt-pocock-skills`** — run before your first engineering flow to configure the issue
tracker, triage labels, and domain-doc layout the other skills assume. Custom trackers also work.
→ [references/engineering/setup-matt-pocock-skills/SKILL.md](references/engineering/setup-matt-pocock-skills/SKILL.md)

---

## Full skill index

### Engineering (user-invoked)

- [ask-matt](references/engineering/ask-matt/SKILL.md) — router over the skills in this repo.
- [grill-with-docs](references/engineering/grill-with-docs/SKILL.md) — grilling session that builds the domain model (`CONTEXT.md` + ADRs).
- [triage](references/engineering/triage/SKILL.md) — move issues/PRs through triage-role state machine.
- [improve-codebase-architecture](references/engineering/improve-codebase-architecture/SKILL.md) — scan for deepening opportunities, HTML report, grill the pick.
- [setup-matt-pocock-skills](references/engineering/setup-matt-pocock-skills/SKILL.md) — configure repo for the engineering skills.
- [to-issues](references/engineering/to-issues/SKILL.md) — break a plan/PRD into independently-grabbable vertical slices.
- [to-prd](references/engineering/to-prd/SKILL.md) — turn the conversation into a PRD, publish to the tracker.

### Engineering (model-invoked)

- [prototype](references/engineering/prototype/SKILL.md) — throwaway prototype answering a design question.
- [diagnosing-bugs](references/engineering/diagnosing-bugs/SKILL.md) — reproduce → minimise → hypothesise → instrument → fix → regression-test.
- [research](references/engineering/research/SKILL.md) — background-agent investigation against primary sources.
- [tdd](references/engineering/tdd/SKILL.md) — red-green-refactor, one vertical slice at a time.
- [domain-modeling](references/engineering/domain-modeling/SKILL.md) — build/sharpen the domain model.
- [codebase-design](references/engineering/codebase-design/SKILL.md) — deep-module vocabulary and principles.
- [code-review](references/engineering/code-review/SKILL.md) — two-axis review (Standards + Spec) via parallel sub-agents.
- [implement](references/engineering/implement/SKILL.md) — implement a PRD/issue via `/tdd`, then `/code-review`.
- [resolving-merge-conflicts](references/engineering/resolving-merge-conflicts/SKILL.md) — resolve merge conflicts deliberately.

### Productivity (user-invoked)

- [grill-me](references/productivity/grill-me/SKILL.md) — relentless interview for stateless plans.
- [handoff](references/productivity/handoff/SKILL.md) — compact conversation for another agent.
- [teach](references/productivity/teach/SKILL.md) — multi-session concept teaching.
- [writing-great-skills](references/productivity/writing-great-skills/SKILL.md) — how to write good skills.

### Productivity (model-invoked)

- [grilling](references/productivity/grilling/SKILL.md) — the reusable interview loop behind `grill-me`/`grill-with-docs`.

### Other buckets (ported for completeness; not promoted)

- `deprecated/` — [design-an-interface](references/deprecated/design-an-interface/SKILL.md), [qa](references/deprecated/qa/SKILL.md), [request-refactor-plan](references/deprecated/request-refactor-plan/SKILL.md), [ubiquitous-language](references/deprecated/ubiquitous-language/SKILL.md).
- `in-progress/` — [claude-handoff](references/in-progress/claude-handoff/SKILL.md), [loop-me](references/in-progress/loop-me/SKILL.md), [wayfinder](references/in-progress/wayfinder/SKILL.md), [wizard](references/in-progress/wizard/SKILL.md), [writing-beats](references/in-progress/writing-beats/SKILL.md), [writing-fragments](references/in-progress/writing-fragments/SKILL.md), [writing-shape](references/in-progress/writing-shape/SKILL.md).
- `misc/` — [git-guardrails-claude-code](references/misc/git-guardrails-claude-code/SKILL.md), [migrate-to-shoehorn](references/misc/migrate-to-shoehorn/SKILL.md), [scaffold-exercises](references/misc/scaffold-exercises/SKILL.md), [setup-pre-commit](references/misc/setup-pre-commit/SKILL.md).
- `personal/` — [edit-article](references/personal/edit-article/SKILL.md), [obsidian-vault](references/personal/obsidian-vault/SKILL.md).

---

## Supporting templates & references

These live under `references/` and are linked from the skills above:

- Domain model: [CONTEXT-FORMAT.md](references/engineering/domain-modeling/CONTEXT-FORMAT.md), [ADR-FORMAT.md](references/engineering/domain-modeling/ADR-FORMAT.md)
- Setup seeds: [issue-tracker-github.md](references/engineering/setup-matt-pocock-skills/issue-tracker-github.md), [issue-tracker-gitlab.md](references/engineering/setup-matt-pocock-skills/issue-tracker-gitlab.md), [issue-tracker-local.md](references/engineering/setup-matt-pocock-skills/issue-tracker-local.md), [triage-labels.md](references/engineering/setup-matt-pocock-skills/triage-labels.md), [domain.md](references/engineering/setup-matt-pocock-skills/domain.md)
- TDD: [tests.md](references/engineering/tdd/tests.md), [mocking.md](references/engineering/tdd/mocking.md)
- Triage: [AGENT-BRIEF.md](references/engineering/triage/AGENT-BRIEF.md), [OUT-OF-SCOPE.md](references/engineering/triage/OUT-OF-SCOPE.md)
- Architecture: [HTML-REPORT.md](references/engineering/improve-codebase-architecture/HTML-REPORT.md), [DEEPENING.md](references/engineering/codebase-design/DEEPENING.md), [DESIGN-IT-TWICE.md](references/engineering/codebase-design/DESIGN-IT-TWICE.md)
- Prototype: [LOGIC.md](references/engineering/prototype/LOGIC.md), [UI.md](references/engineering/prototype/UI.md)
- Teach: [GLOSSARY-FORMAT.md](references/productivity/teach/GLOSSARY-FORMAT.md), [LEARNING-RECORD-FORMAT.md](references/productivity/teach/LEARNING-RECORD-FORMAT.md), [MISSION-FORMAT.md](references/productivity/teach/MISSION-FORMAT.md), [RESOURCES-FORMAT.md](references/productivity/teach/RESOURCES-FORMAT.md)
- HITL debug loop: [scripts/hitl-loop.template.sh](scripts/hitl-loop.template.sh) (also at [references/engineering/diagnosing-bugs/scripts/hitl-loop.template.sh](references/engineering/diagnosing-bugs/scripts/hitl-loop.template.sh))
