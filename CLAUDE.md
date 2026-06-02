# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Jeff's personal article collection ("深度思考集") — a static HTML site of long-form essays in Simplified Chinese (`lang="zh-CN"`). There is no build system, no package manager, and no tests. Articles are hand-authored, self-contained HTML files served as-is.

## Architecture

- `index.html` — landing page. Acts as the article index: each article gets an `<article class="article-card">` block linking to its own HTML file. Styles are inline in a `<style>` block; the visual language here (purple gradient header, card grid, sans-serif stack with `Noto Sans SC`) is intentionally simpler than the article pages.
- `saas-zhi-si.html` — example of an article page. Each article is a single self-contained file with:
  - A `<section class="hero">` cover with grid/particle animations.
  - A `<main class="article">` body split into numbered `<div class="section">` blocks (`section-number` + `section-title` + prose).
  - Reusable visual components defined in the same inline `<style>` block: `.quote-block`, `.info-card`, `.terminal` (mock CLI output with `.terminal-bar`/`.terminal-body`/`.prompt-symbol`/`.output`), `.comparison`, `.spell` (highlighted term), `.ending`, `.footer`.
  - A design-token `:root` block (`--ink`, `--paper`, `--accent`, `--accent2`, `--gold`, `--code-bg`, `--code-green`, `--card-bg`, `--border`) — reuse these variables when adding styles rather than hardcoding colors.
  - Google Fonts link for `Noto Serif SC`, `Noto Sans SC`, `JetBrains Mono`.

Each article ships as one file — CSS, markup, and any JS live inline. There is no shared stylesheet or template, so a new article starts by copying an existing one and keeping the same component class names so the look stays consistent.

## Adding a new article

1. Copy an existing article file (e.g. `saas-zhi-si.html`) to a new kebab-case filename — pinyin-based names are the established convention (`saas-zhi-si.html` = "SAAS之死").
2. Update `<title>`, hero text, and the numbered `.section` blocks.
3. Keep the `:root` CSS variables and component class names unchanged so styling stays consistent across articles.
4. Add a new `<article class="article-card">` entry to `index.html` pointing at the new file, with Chinese title, excerpt, and tag.

## Preview

No build step — open `index.html` directly in a browser, or serve the directory:

```
python3 -m http.server 8000
```

## Git workflow

Active development branch for this session: `claude/add-claude-documentation-1yeEC`. Commit messages in history are short imperative English (e.g. "Add SAAS之死 article with index page"); match that style.
