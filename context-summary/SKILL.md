---
name: context-summary
description: Maintain and refresh a project-root CONTEXT.md so Codex can recover the current project state across sessions. Use when starting work in a project, resuming an old workspace, initializing missing project context, or updating a stale CONTEXT.md after meaningful code or structure changes. Focus on folder structure, the purpose of important files and directories, the current project goal, key commands or entry points when discoverable, and other concise handoff details that help a later session rebuild context quickly.
---

# Context Summary

Maintain a single `CONTEXT.md` file at the current project root as the durable handoff note for future sessions.

Read the workspace first, then write or refresh `CONTEXT.md` so it reflects what the project is, how it is organized, and which files matter.

## Workflow

### 1. Detect the context file

Check whether `CONTEXT.md` already exists at the project root.

If it exists, read it before doing anything else. Treat it as the current project summary, not as ground truth. Verify the important claims against the current files before preserving them.

If it does not exist, inspect the workspace first and create it from scratch.

### 2. Build a lightweight project map

Read only the files needed to understand the project quickly.

Start from the top level:

- List top-level files and directories.
- Identify the main code directories, config files, data folders, docs, and entry points.
- Prefer reading representative files such as `README`, `AGENTS.md`, `pyproject.toml`, `package.json`, `requirements.txt`, `Cargo.toml`, main scripts, and important configs.
- Read key source files only until the role of each major folder or file is clear.

Keep the scan concise. Do not try to summarize every generated file or every leaf file in large trees.

### 3. Decide what is important enough to record

Record stable, high-value context that helps another session start fast:

- What the project appears to do.
- What the main folders are for.
- What the important files are for.
- Which script, app, notebook, or config seems to be the main entry point.
- Which commands are useful to run, if they are discoverable from the repo.
- Which conventions, constraints, or caveats are visible from the files.
- Which parts are incomplete, risky, or obviously in flux.

Prefer durable facts over temporary noise.

Do not include:

- Full code listings.
- Long prose copied from docs.
- Exhaustive dependency dumps.
- Generated artifacts unless they matter to understanding the project.
- Speculation presented as certainty.

### 4. Write or refresh `CONTEXT.md`

Keep the file short, readable, and easy to update by hand.

Use a structure close to this:

```md
# Context

## Project Summary
- One short paragraph on what the project is and what it is currently trying to do.

## Structure
- `path/or/file`: what it is for
- `path/or/file`: what it is for

## Key Files
- `file`: why it matters
- `file`: why it matters

## Entry Points And Commands
- Main script/app:
- Common run/test/build commands:

## Current Constraints Or Risks
- Important caveat
- Important caveat

## Notes For Future Sessions
- Anything that would save re-discovery time later
```

Prefer bullet lists for structure and key files. Keep each description concrete and brief.

When refreshing an existing `CONTEXT.md`, preserve useful information that is still true, delete stale details, and rewrite ambiguous notes into crisp statements.

## Coverage Rules

For folder structure, aim for practical coverage instead of exhaustive coverage.

Usually include:

- Every important top-level directory.
- Key nested directories when they have distinct responsibilities.
- Important standalone files at the root.
- Any unusual assets, datasets, prompts, notebooks, or scripts that drive the project.

Usually skip or compress:

- `.git/`
- dependency caches such as `node_modules/`, `.venv/`, `__pycache__/`
- build outputs such as `dist/`, `build/`, `out/`, `coverage/`
- large generated result folders unless they are central to the workflow

If a directory is huge, summarize it at a higher level instead of listing many children.

## Writing Rules

- Write in UTF-8.
- Prefer short factual sentences.
- State uncertainty explicitly when needed, using wording like `appears to`, `likely`, or `not yet confirmed`.
- Avoid repeating information across sections.
- Keep `CONTEXT.md` useful for a future Codex session that has not seen the prior conversation.
- Update the existing file in place instead of creating extra handoff documents.

## Triggers And Examples

Use this skill for requests such as:

- `初始化这个项目的 CONTEXT.md`
- `更新一下当前仓库的 CONTEXT.md`
- `先读 CONTEXT.md，再继续做这个项目`
- `帮我整理一下项目结构，方便下次继续`

When the user asks to maintain project memory across sessions, default to this skill and treat `CONTEXT.md` as the single source of durable handoff context.
