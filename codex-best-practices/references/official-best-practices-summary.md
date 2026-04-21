# Official Best Practices Summary

Source page:

- OpenAI Codex best practices: https://developers.openai.com/codex/learn/best-practices

Use this file when you want the official guidance grouped by topic instead of relying on memory.

## Context and prompts

- Treat Codex like a teammate that improves with configuration over time.
- For most tasks, build the request around four fields:
  - Goal
  - Context
  - Constraints
  - Done when
- Better context usually matters more than a perfectly polished prompt.
- Choose reasoning depth based on task difficulty instead of using one level for everything.

## Plan first for difficult tasks

- Plan before coding when the task is complex, ambiguous, or hard to describe.
- Strong options include Plan mode, asking Codex to interview the user first, or using a plan template for longer work.

## Reuse guidance with AGENTS.md

- Put repo layout, run commands, test commands, conventions, constraints, and verification expectations into `AGENTS.md`.
- Keep `AGENTS.md` short and practical.
- If Codex repeats the same mistake, update `AGENTS.md` with the missing rule.
- Prefer layered guidance: global, repo, and subdirectory rules.

## Configure Codex for consistency

- Keep personal defaults in `~/.codex/config.toml`.
- Keep repo-specific defaults in `.codex/config.toml`.
- Use command-line overrides only for one-off cases.
- Quality problems are often setup problems such as the wrong working directory, missing tools, wrong defaults, or missing access.
- Start with tighter approval and sandbox settings, then loosen them only when the workflow is understood.

## Improve reliability with testing and review

- Do not stop at code generation.
- Ask Codex to add or update tests when needed.
- Run relevant checks, confirm final behavior, and review the diff for regressions or risky patterns.
- Make sure Codex knows what "good" looks like through the prompt or `AGENTS.md`.

## Use MCP for external context

- Use MCP when the needed context is outside the repo, changes frequently, or should be accessed as a live tool.
- Start with one or two high-value integrations rather than connecting everything at once.

## Turn repeated work into skills

- Create a skill when a workflow becomes repeatable and you keep reusing the same prompt or correction.
- Keep the skill narrow and centered on one job.
- Start with a few concrete use cases and clear inputs and outputs.
- Add scripts or assets only when they improve reliability.

## Use automations for repeated work

- Skills define the method.
- Automations define the schedule.
- Automate only after the workflow is stable without much manual steering.

## Session controls

- Keep one thread per coherent task.
- Fork only when the work truly branches.
- Use subagents for bounded side work such as exploration, tests, or triage.

## Common mistakes

- Putting durable rules into ad hoc prompts instead of `AGENTS.md` or a skill
- Not telling Codex how to run build and test commands
- Skipping planning on complex work
- Granting too much permission too early
- Running live threads on the same files without worktree separation
- Automating before the manual workflow is reliable
- Keeping one giant thread per project instead of one thread per task
