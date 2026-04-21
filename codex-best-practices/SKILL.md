---
name: codex-best-practices
description: Improve how Codex is used on a task or workflow. Use when the user asks how to get better Codex results, how to structure a prompt or plan, whether guidance belongs in the prompt or AGENTS.md or config.toml, when to use MCP, when to package work as a skill or automation, or how to turn a vague request into a reliable Codex execution brief.
---

# Codex Best Practices

## Overview

Use this skill to turn fuzzy Codex work into a reliable operating pattern. Focus on the task brief, planning depth, durable guidance location, validation loop, and the next reusable improvement.

## Core Workflow

1. Classify the request:
   - one-off task
   - ambiguous or multi-step task
   - recurring workflow
   - setup or configuration issue
2. Rewrite the task into four fields:
   - Goal
   - Context
   - Constraints
   - Done when
3. Choose execution depth:
   - Low reasoning for fast, well-scoped work
   - Medium or High for debugging, larger edits, or higher-risk changes
   - Extra High for long-horizon, agentic, reasoning-heavy work
   - Plan first when the task is ambiguous, hard to describe, or multi-step
4. Choose where durable guidance should live:
   - prompt for task-local instructions
   - `AGENTS.md` for repo and team rules
   - `config.toml` for personal or repo defaults
   - MCP for external, changing, tool-backed context
   - skill for repeatable workflows
   - automation for already-stable recurring work
5. Add the reliability loop:
   - tests or checks
   - behavior verification
   - diff review
6. Call out the smallest useful next improvement:
   - tighten the prompt
   - update `AGENTS.md`
   - add one MCP
   - extract a skill
   - automate a stable workflow

## Decision Rules

### Prompt vs durable guidance

- Keep task-specific instructions in the prompt.
- Move repeated repo guidance into `AGENTS.md`.
- Move execution defaults such as model choice, reasoning, approvals, sandboxing, profiles, or MCP setup into `config.toml`.

### Planning

- Ask Codex to plan first when the work is hard to scope, still fuzzy, or likely to branch.
- Skip explicit planning when the task is small and the acceptance criteria are already concrete.

### External context

- Prefer MCP when the needed context lives outside the repo, changes frequently, or should be accessed as a tool instead of pasted text.
- Start with one or two MCP integrations that remove a real manual loop.

### Skills and automations

- Create a skill when the same prompt, checklist, or correction keeps repeating.
- Keep each skill scoped to one job with clear inputs and outputs.
- Create an automation only after the manual workflow is stable and predictable.

## Output Contract

When using this skill, return the minimum useful package:

1. A rewritten task brief with `Goal`, `Context`, `Constraints`, and `Done when`
2. A recommended reasoning level and whether to plan first
3. The best durable home for repeated guidance
4. A validation checklist
5. One to three mistakes or risks to avoid

## Default Prompt Template

Use this structure when the user has a vague request:

```text
Goal:
Context:
Constraints:
Done when:
```

If the task is still fuzzy after filling this in, recommend planning before coding.

## Common Mistakes To Catch

- Overloading a single prompt with rules that belong in `AGENTS.md` or a skill
- Skipping planning for multi-step work
- Running with overly broad permissions before the workflow is understood
- Creating an automation before the manual workflow is reliable
- Keeping unrelated tasks in one long thread until the context becomes noisy

## Reference Map

Read `references/official-best-practices-summary.md` when you need the section-by-section source notes from the official OpenAI Codex best practices page.
