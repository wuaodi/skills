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

Choose the minimum set that answers the user's question. Common picks:

| User goal | Diagram types |
|-----------|---------------|
| "How does it work?" | Overall architecture panorama + message/data flow sequence |
| "What's the core loop?" | Flowchart of the main loop with branches and exit conditions |
| "How do subsystems fit together?" | One overview + one per subsystem (small detail SVGs) |
| "How does X compare to Y?" | Side-by-side loop diagrams + comparison table |
| "Show me the state machine" | State-transition diagram |

Cap at **6–8 SVG figures** for readability. Each figure gets a caption.

### 3 · Visual design rules

**Colors (dark theme — always use this palette):**
```css
--bg:#0f1419; --panel:#161c24; --panel2:#1c2530; --ink:#e6edf3; --muted:#9fb0c0;
--line:#2b3947; --accent:#5aa9e6; --accent2:#7ee787; --warn:#f2cc60; --pink:#ff7b9c;
--purple:#bc8cff; --orange:#ffa657;
```

**SVG conventions:**
- Every diagram uses `viewBox` and `role="img" aria-label="…"` — scales to container width
- Define `<marker>` arrowheads in `<defs>` (one per color used for arrows)
- Use semantic grouping: subsystem boxes are visually distinct (different `fill`/`stroke` per layer)
- Font stacks inside SVG: `-apple-system,"PingFang SC","Microsoft YaHei",Segoe UI,sans-serif` for labels; `Menlo,Consolas,monospace` for code identifiers
- Keep coordinates round numbers; leave ≥10px margin from viewBox edges
- Color coding is consistent across all figures (e.g. green = agent core, blue = external/channel, orange = tools, pink = LLM)

**Layout:**
- Sticky left TOC (anchor links) + scrollable main column
- `max-width: 1180px`, centered
- Sections separated by a subtle border
- Cards for key concepts, tables for comparisons, numbered steps for sequences
- Responsive: collapse multi-column to single column on narrow viewports

**Text:**
- Chinese prose for explanations, English for code symbols and technical terms
- Bilingual section subtitles: Chinese primary, English in `<small>`
- `<code>` for identifiers, file paths, function names
- `file:line` references where they add precision

### 4 · File structure template

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Subject] 工作原理图解</title>
  <style>
    /* full inline CSS — dark theme palette, layout, SVG text classes */
  </style>
</head>
<body>
  <div class="wrap">
    <nav class="toc">…anchor links per section…</nav>
    <main>
      <header class="hero">…title, one-line description, badges…</header>
      <!-- Sections: intro, panorama, core flow, subsystems, patterns, comparison, file map -->
      <section id="…">
        <h2><span class="num">N</span>Title<small>English subtitle</small></h2>
        <div class="fig"><svg viewBox="…">…</svg><div class="cap">Caption</div></div>
        …prose, steps, cards, tables…
      </section>
      <footer>…source note, date…</footer>
    </main>
  </div>
</body>
</html>
```

### 5 · Output contract

1. **Single file** at a sensible path (e.g. project root `subject-how-it-works.html`, or the user's preferred location)
2. **Offline-clean**: after writing, run `grep -E "<script|cdn|href=.https?://" file.html` — only intentional external hyperlinks (not asset loads) should appear
3. **Tag balance**: confirm `<section>`, `<svg>`, `<table>`, `<nav>` counts match their closing tags
4. **No broken CSS**: no color values with spaces, no unclosed rules
5. Tell the user the file path and briefly describe what each section covers

## Quality checklist

- [ ] Read the source / fetched URL before drawing (no invented details)
- [ ] Each SVG has a `viewBox`, `role="img"`, and `aria-label`
- [ ] Arrowhead markers defined in `<defs>`, not repeated inline
- [ ] Color palette consistent across all SVGs
- [ ] Zero external script/style loads
- [ ] Tag balance verified (section/svg/table open = close)
- [ ] File opens correctly in browser with no console errors
- [ ] Prose is accurate — code identifiers and file paths match source

## Defaults

- **Language**: Chinese (中文) primary, English for code symbols — unless user specifies otherwise
- **Theme**: dark
- **Diagrams**: pure SVG/CSS, no Mermaid, no D3 — so the file is truly offline
- **Output location**: project root (or user-specified)
- **Scope**: cover the whole system at overview level, then zoom into the parts the user asked about most
