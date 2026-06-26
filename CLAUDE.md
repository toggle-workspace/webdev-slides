# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # start dev server at localhost:3030 with hot reload
npm run build    # build static output to dist/
npm run export   # export slides to PDF/PNG
```

## Architecture

This is a [Slidev](https://sli.dev/) presentation project — a Markdown-driven slide deck for toggle.solutions B2B case studies.

**Content lives in `slides.md`** — all slides are defined here as Markdown separated by `---`. Each slide can declare frontmatter (layout, class, transition) and use inline Vue/HTML with Tailwind utility classes.

**Theme and styling**: Uses `slidev-theme-light-icons`. Global overrides are in `styles/custom.css`, which is imported at the top of `slides.md`. The design system is dark (`#0d0d0d` background, `#4F8EF7` accent blue, Inter font).

**Layouts used**: `center` (hero/title slides), `two-cols` (detail slides with `::right::` slot divider).

**Custom Vue components** go in `components/` and are auto-imported into slides. `snippets/` holds reusable code snippets.

**Images** are served from `image/` at the project root (referenced as `/image/...` in slides). Do NOT move images into `public/` — Slidev compiles image references into ES module imports, which Vite can only resolve from the project root, not from `public/`.

**Deployment**: Deployed to GitHub Pages via `.github/workflows/deploy.yml`. The build uses `--base ./` (relative) so that assets load correctly and hash-mode routing URLs don't double up the repo name. `vercel.json` and `netlify.toml` are present but not the active deployment targets.

## Skills

Always invoke these skills before starting the relevant work:

- **Building new slides or layouts**: use the `slidev` skill (`skills/slidev/SKILL.md`)
- **Writing or editing slide copy**: use the `copywriting` skill (`skills/copywriting/SKILL.md`)

## Slide structure pattern

Each case study follows a two-slide pattern:
1. **Hero slide** (`layout: center`) — client name, category tag, headline metrics
2. **Detail slide** (`layout: two-cols`) — left: narrative + bullet list with `.value-props` class, right: stat cards
