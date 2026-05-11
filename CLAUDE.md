# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```sh
npm run dev       # Start dev server at localhost:4321
npm run build     # Build production site to ./dist/
npm run preview   # Preview the production build locally
npm run astro check  # TypeScript / Astro type checking
```

## Architecture

This is an **Astro 6 blog** site (tapasTech.ink) using the official blog starter template.

**Content layer** — Blog posts live in `src/content/blog/` as `.md` or `.mdx` files. The collection schema is defined in `src/content.config.ts` using Zod. Required frontmatter per post:

```yaml
title: string
description: string
pubDate: date        # ISO 8601
updatedDate: date    # optional
heroImage: image()   # optional, processed by Astro's Image pipeline
```

**Routing** — File-based via `src/pages/`. Blog listing is at `src/pages/blog/index.astro`; individual posts are rendered dynamically from the content collection. The RSS feed is at `src/pages/rss.xml.js`.

**Global config** — `src/consts.ts` holds `SITE_TITLE` and `SITE_DESCRIPTION`. The canonical site URL is set in `astro.config.mjs` (`site` field — currently `'https://example.com'`, should be updated to the real domain).

**Integrations** — `@astrojs/mdx`, `@astrojs/sitemap`, `@astrojs/rss`. No UI framework (React/Vue/etc.) is installed; components are `.astro` only.

**Fonts** — Local Atkinson Hyperlegible font (regular + bold) served from `src/assets/fonts/`, configured as `--font-atkinson` CSS variable in `astro.config.mjs`.

**Styling** — Global styles in `src/styles/global.css`; component-scoped `<style>` blocks inside `.astro` files. No CSS framework.
