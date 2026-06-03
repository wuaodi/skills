---
name: html-view
description: Turn any codebase, concept, system, or comparison into a beautiful self-contained offline HTML explainer — with hand-drawn SVG diagrams, flow charts, architecture maps, and bilingual (Chinese + English) prose. Use when the user wants to "understand X visually", "make an HTML explainer", "create a diagram for Y", or says things like "帮我可视化", "做个html", "画个架构图". The output is a single file that opens offline with zero external dependencies.
---

# html-view skill

## Purpose

Produce a **single, self-contained, offline HTML file** that explains a system, concept, or comparison through:
- SVG diagrams (architecture panorama, workflow, subsystem detail, comparison)
- Concise bilingual prose (Chinese primary, English secondary, code identifiers kept in English)
- Zero external dependencies (no CDN, no `<script src>`, no `<link href>` to remote URLs)

## When invoked

User asks to visualise something: *"帮我理解X"*, *"画个架构图"*, *"做个html explainer"*, *"compare X and Y visually"*, etc.

## Workflow

### 1 · Understand the subject

Before writing HTML, explore enough to get facts right:
- If the subject is **a local codebase** — read the key source files (entry points, core loop, main abstractions). Use parallel `Explore` agents for large codebases.
- If the subject is **an external project or URL** — fetch it with `WebFetch`.
- If the subject includes a **comparison** — explore both sides before drawing any diagram.

Do not guess at class names, file paths, or data flows. Accuracy beats speed.

### 2 · Identify the diagrams needed

### 3 · Output contract

1. **Single file** at a sensible path (e.g. project root `subject-how-it-works.html`, or the user's preferred location)
2. **Offline-clean**: after writing, run `grep -E "<script|cdn|href=.https?://" file.html` — only intentional external hyperlinks (not asset loads) should appear
3. 如果一张架构图+文字就能够说明白，就用一张；否则的话，可以增加一些流程图、思维导图、对比等，但是尽可能保障方便用户来阅读和理解
