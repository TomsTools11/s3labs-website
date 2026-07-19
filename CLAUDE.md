# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

The marketing site for **S3 Labs** (s3labs.tech), a software studio. Plain static site — no framework, no build step, no package.json, no tests. Deployed via Vercel from the repo root; `vercel.json` enables clean URLs (`/projects`, `/library`).

## Commands

Preview locally (there is no build):

```
python3 -m http.server 8000   # then open http://localhost:8000/
```

## Architecture

Three pages at the repo root, implemented from a Claude Design handoff:

- **`index.html`** — home: hero, stats band, featured DropDoc card with dropzone mock, "The Lab" product grid, contact CTA, footer.
- **`projects.html`** — project grid with Live / In progress filter buttons.
- **`library.html`** — curated software library: ~130 tool cards with category filters and live search. Card logos live in `assets/img/lib/`.

Shared foundation:

- **`assets/css/styles.css`** — the only stylesheet: `@font-face` for Lato (from `fonts/*.ttf`), keyframes, `.hv*` numbered hover classes, and attribute-selector media queries that override inline `grid-template-columns` for responsiveness. Page/layout styles are **inline `style` attributes in the HTML** (design-tool export idiom) — keep that pattern when editing.
- **`assets/js/main.js`** — one IIFE shared by all pages: `[data-reveal]` scroll reveals (IntersectionObserver + no-JS/fallback paths), `[data-count]` animated counters, `[data-filterbar]`/`[data-card]` category filters with optional `[data-search]` live search, and the home-page DropDoc dropzone mock (`#mockDrop`).

## Conventions & gotchas

- **Fonts are split**: Lato is bundled locally in `fonts/*.ttf`; Geist and Fira Code come from the Google Fonts CDN via a `<link>` in each page's head.
- **The page is locked to a dark palette** (bg `#0B0C10`, brand blues `#5C9BE8`/`#2E6BB0`). There is no light theme.
- **Favicon is cache-busted** with `?v=N` on the `<link rel="icon">` href (`assets/img/favicon.png`) — bump `N` when replacing the file.
- **Internal links use `*.html` hrefs** so the site works under `python3 -m http.server`; in production Vercel's `cleanUrls` redirects `/projects.html` → `/projects`.
- The contact CTA is a `mailto:` link; there is no form and no backend anywhere on the site.
- Product links: DropDoc → `https://dropdoc.sh`, StyleSnap → `https://stylesnap.design`, Persona → `https://personalab.im`.
