---
name: speckit
description: "Spec-Driven Development entry point based on GitHub spec-kit. Use when starting a new feature or project with the spec-kit methodology, or when the user asks about speckit workflow. Orchestrates the speckit-* skills through the full SPECIFY → PLAN → TASKS → IMPLEMENT lifecycle."
compatibility: "Requires the target project to be initialized with `specify init` (creates .specify/ directory). Install the CLI with `uv tool install specify-cli`."
metadata:
  author: "github-spec-kit"
  source: "https://github.com/github/spec-kit"
---

# Spec Kit: Spec-Driven Development Workflow

This is the entry point for the spec-kit workflow. Each phase below has a dedicated skill — invoke the matching `speckit-*` skill for that phase rather than improvising.

## Workflow Order

```
/constitution (once per project) → /specify → [clarify] → /plan → [checklist] → /tasks → [analyze] → /implement → [converge]
```

| Phase | Skill | Purpose | Required? |
|-------|-------|---------|-----------|
| Constitution | `speckit-constitution` | Establish project governance principles | Once per project |
| Specify | `speckit-specify` | Create the feature spec from a natural-language description | Required |
| Clarify | `speckit-clarify` | Structured questions to de-risk ambiguity | Optional, before plan |
| Plan | `speckit-plan` | Technical implementation plan from the spec | Required |
| Checklist | `speckit-checklist` | Quality checklists validating the spec/plan | Optional, after plan |
| Tasks | `speckit-tasks` | Actionable task list from the plan | Required |
| Analyze | `speckit-analyze` | Cross-artifact consistency report | Optional, after tasks |
| Implement | `speckit-implement` | Execute tasks and build the feature | Required |
| Converge | `speckit-converge` | Assess codebase vs. spec, append remaining work | Optional, for iteration |

`speckit-taskstoissues` converts the task list into GitHub issues for tracking.

## How to Run It

1. The user's feature description is the input to `speckit-specify` (or `speckit-constitution` if no project constitution exists yet).
2. Follow the sequence above; do not skip to implementation. Each skill writes its artifact under the feature branch's `specs/<branch>/` directory (spec.md, plan.md, tasks.md, ...).
3. Validate the current phase's artifact with the user before advancing to the next phase.
4. All speckit-* skills expect the project to have a `.specify/` directory (created by `specify init`). If it is missing, tell the user to run:

   ```bash
   uv tool install specify-cli
   specify init . --integration claude --non-interactive
   ```

## Core Philosophy

The specification is the source of truth and is *executable*: intent-driven (what & why before how), refined in multiple steps, and validated by the user at every gate. Code without a spec is guessing.
