# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Jekyll-based personal portfolio site for Johannes Jasper (https://www.johannesjasper.de). Ruby/Bundler only — no Node.js.

## Commands

```bash
# Install dependencies
bundle install

# Local development server
jekyll serve --watch

# Production build
JEKYLL_ENV=production bundle exec jekyll build --destination ~/www/www.johannesjasper.de
```

## Architecture

- `_layouts/` — Page templates (default, page, post)
- `_includes/` — Shared partials (head, footer)
- `_sass/` — SCSS source files; `styles.scss` is the entry point
- `_bibliography/citations.bib` — Academic citations (jekyll-scholar)
- `_config.yml` — Site config: title, social links, markdown/highlight settings

Templates use Liquid. Content is Markdown (kramdown). Syntax highlighting via Rouge.
