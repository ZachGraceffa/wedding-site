# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static multi-page wedding website for Zach & Ronnie's wedding, September 19th, 2026 in Chicago, IL. No build step, no framework — pure HTML, inline Tailwind (CDN), and a single shared `script.js`.

## Pages

- `index.html` — hero landing page with unique 3-column xl layout (side navs flank the title)
- `schedule.html`, `travel.html`, `faq.html`, `rsvp.html` — inner pages sharing a common header/nav pattern

## Styling

**Tailwind is loaded via CDN** (`https://cdn.tailwindcss.com`) in every HTML file with an inline `tailwind.config` block. The `npm run build:css` / `watch:css` scripts exist but the output is not currently referenced by any HTML file — changes to Tailwind classes only need to go in the HTML.

The Tailwind config is duplicated in every HTML `<script>` block. When changing design tokens, update all files.

**Design tokens:**
- Colors: `bg-cream` (`#e8e3d8`), `text-brown` (`#3d3531`), `text-red` (`#c74545`)
- Fonts: `font-baskerville` (Libre Baskerville, serif headings), `font-cormorant` (Cormorant Garamond, display), `font-mono` (Cutive Mono, nav/labels)

## Responsive layout

- Mobile/tablet: single-column, top nav bar
- `xl` (1280px+): 3-column grid on index with side navs; inner pages stay centered single-column
- Breakpoints used: `md:`, `xl:` — no `sm:` or `lg:` usage

## Images

Hero images live in `images/` as responsive WebP at 320/480/640/768/1024/1280/1536/1920px widths, used via `srcset`/`sizes="100vw"`. `resize.py` (requires Pillow) regenerates them from a source JPEG.

Heart divider (`images/heart-divider.png`) is used between sections with `mix-blend-mode: multiply` so it blends into the cream background.

## Serving locally

No dev server is bundled. Serve on port 3333:

```bash
python3 -m http.server 3333
```

Site available at `http://localhost:3333`.

`screenshot.mjs` assumes a server running on port 3333 and uses Playwright (not installed — install separately if needed).
