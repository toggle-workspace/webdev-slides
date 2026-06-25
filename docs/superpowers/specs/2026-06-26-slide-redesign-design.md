# Slide Redesign — Asymmetric Editorial

**Date:** 2026-06-26  
**Goal:** Transform the flat centered layout into a bold, left-aligned editorial design that works both as a standalone link and a live presentation.

---

## Context

The current deck (`slides.md`) uses centered flex-col layouts throughout — every slide stacks content in the middle with equal visual weight. The color palette and content are strong, but the layout reads as generic. The audience is B2B prospects who may view solo or be walked through the deck live.

**Chosen direction:** Option A — Asymmetric Editorial. Left-align everything, make metrics massive, add editorial texture. Inspired by Bloomberg / Vercel marketing energy.

---

## Design Decisions

- **Motion:** Subtle only — slide transitions already exist, no complex click-reveal animations
- **Viewer context:** Standalone link AND live screenshare — must be self-explanatory without a presenter
- **No new dependencies** — all changes via Tailwind utilities + `styles/custom.css` additions

---

## Section 1: Global CSS

**File:** `styles/custom.css`

Add a dot-grid background texture to `.slidev-layout`:
- Radial-gradient dots, 1px, very low opacity (~8%) on `#0d0d0d` base
- Dot spacing: 24px grid
- Gives surface depth without noise

Boost `.value-props li::before` arrow color to full `#4F8EF7` (currently already set, verify it's not muted).

---

## Section 2: Title Slide

**Current:** Centered flex-col — logo, h1, subtitle.

**New layout:**
- Content left-aligned, anchored to lower-left third of slide (not exact center)
- Logo: absolute top-left, `h-10`
- "Case Studies" headline: `text-7xl font-bold`, left-aligned, with a `4px` solid `#4F8EF7` left-border accent spanning the full text height (use `border-l-4 border-[#4F8EF7] pl-6`)
- "Web Development" tag: small uppercase, left-aligned, below headline — same style as current but not centered

---

## Section 3: Hero Slides (6 slides — one per client)

**Current:** Centered flex-col — category tag, logos row, description, metrics row.

**New layout (left-aligned, no `items-center`):**

**Top strip (left-aligned):**
- Category tag: same pill style, but `self-start` (not centered)
- Logo pair (toggle × client): `flex items-center gap-8`, `justify-start`

**Description:**
- Left-aligned, `text-lg` (up from `text-sm`), `max-w-lg`

**Metrics block (dominant lower section):**
- Each metric number: `text-8xl font-black text-[#4F8EF7] leading-none`
- Labels: `text-[10px] uppercase tracking-widest text-[#555]`
- Arranged in a `flex gap-12` row, left-aligned
- Numbers are the visual — they should feel almost too large

**Ghost watermark:**
- Client name (or abbreviation) as absolute background text
- `text-[18rem] font-black text-white opacity-[0.04]`
- Positioned `absolute bottom-0 right-0` or slightly offset right
- `pointer-events-none`, `select-none`, `overflow-hidden`

---

## Section 4: Detail Slides (6 slides — two-cols "What we did")

**Current:** Left = text + bullets, right = small dark stat cards.

**Left column changes:**
- Add `border-l-4 border-[#4F8EF7] pl-6` to the column wrapper — the defining editorial mark
- "What we did" heading: `text-3xl` (up from `text-2xl`)
- Otherwise keep structure — description + bullet list

**Right column changes:**
- Remove all card containers (`bg-[#111]`, `border`, `rounded-lg`, padding boxes)
- Each stat rendered as bare text:
  - Number: `text-7xl font-black text-[#4F8EF7] leading-none`
  - Label: `text-[10px] uppercase tracking-widest text-[#555] mt-2`
  - Divider: `border-b border-[#1a1a1a] pb-6 mb-6` between stats (except last)
- Stats feel like editorial pull-quotes, not dashboard widgets
- Remove `border-l border-[#222]` from the right column wrapper (the card-less stats don't need a column separator — the left blue border provides enough structure)

---

## Section 5: Closing Slide

**Current:** Centered — logo, hr divider, tagline, contact links inline.

**New layout:**
- Logo: absolute top-left, `h-10` — consistent with title slide
- Remove the `<hr>` divider
- Tagline: `text-5xl font-bold text-white`, left-aligned, with `border-l-4 border-[#4F8EF7] pl-6` accent — mirrors the detail slide heading style
- Contact links: stacked vertically in bottom-left, each prefixed with `→ ` for consistency with bullet style, `text-sm` (up from `text-xs`)
- Vertical layout: tagline in center-left zone, links pinned to bottom-left using flex justify-between or absolute positioning

---

## What Stays the Same

- Color palette: `#0d0d0d` bg, `#4F8EF7` accent, `#e5e5e5` text
- Font: Inter
- Slide transitions: `slide-left` already set in headmatter
- Theme: `light-icons` — no theme change needed
- Content/copy: zero copy changes, layout only
- The `→` arrow on `.value-props` bullets

---

## Files to Change

1. `styles/custom.css` — dot-grid background
2. `slides.md` — all slide HTML (title, 6 hero slides, 6 detail slides, closing slide)
