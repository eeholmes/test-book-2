# AGENTS.md

Instructions for coding agents working in this repository. `CLAUDE.md` contains
only `@AGENTS.md`, so Claude Code reads this file too; edit `AGENTS.md`, not
`CLAUDE.md`.

Read `claude/handoff.md` first: it has the current state of the participant
guide, and points to the decision notes in `claude/notes/`.

## Project Overview

The Agent Coders Clinic participant guide. It is built on the NOAA Quarto book template (`type: book`) that renders to HTML, PDF (via LaTeX/TinyTeX), and docx. Uses the `nmfs-opensci/titlepage` Quarto extension for PDF/coverpage styling.

## Build Commands

```bash
# Render all formats (html, pdf, docx) to _book/
quarto render

# Render single format
quarto render --to html
quarto render --to titlepage-pdf
quarto render --to docx

# Live preview (HTML only, opens browser)
quarto preview
```

## Architecture

- **`_quarto.yml`** — Primary config: chapter order, format options, sidebar, bibliography. Add new chapters here under `book.chapters`.
- **`_frontmatter.yml`** — PDF/docx-specific overrides (titlepage, coverpage themes, geometry). Comment out the `metadata-files` entry in `_quarto.yml` if PDF builds fail.
- **`content/`** — All book chapters (`.qmd` files). `references.bib` lives here too.
- **`assets/`** — SCSS themes (`theme.scss`, `theme-dark.scss`), favicon, and `include-files.lua` (a Pandoc filter for transclusion via `{.include}` code blocks).
- **`_extensions/nmfs-opensci/titlepage/`** — Quarto extension providing `titlepage-pdf` format, coverpage Lua filters, and bundled fonts.
- **`cls/svmono.cls`** — LaTeX class file (Springer monograph), available but not used by default config.
- **`template.docx`** — Reference doc for docx styling.

## CI/CD

GitHub Actions (`.github/workflows/render-and-publish.yml`) triggers on push to `main`, renders all formats via `quarto-dev/quarto-actions/publish@v2`, and deploys HTML to `gh-pages` branch. Requires R packages `rmarkdown`, `knitr`, `jsonlite`. TinyTeX is installed for PDF builds.

## Key Conventions

- The PDF format is `titlepage-pdf`, not `pdf` — this comes from the titlepage extension.
- `execute.echo: false` is set globally — code blocks render output only by default.
- The `include-files.lua` filter enables file transclusion: use `{.include}` class on code blocks to inline external markdown files.
- Bibliography is at `content/references.bib`; add citations in `.qmd` files with `@key` syntax.
