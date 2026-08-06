# AGENTS.md

Guidance for AI agents and contributors working on this repository.

## Overview

Personal portfolio website for **Subasantosh Yaparala** (DevOps Engineer), deployed as GitHub Pages from the `docs/` directory at `https://yaparlareddy.github.io/`. The design language is modeled on a "career observability dashboard": dark near-black surfaces, purple accent (`#7B6EF6`), 0.5px hairline borders, and status/operational motifs (pulse dots, process tree, deployment log).

## Project Structure

```
/                          repo root (AGENTS.md, README.md, .git)
docs/                      GitHub Pages site root (everything public)
  index.html               single-page portfolio (nav, status bar, hero, skills strip, about, experience, dashboard, projects, quote, footer)
  page1.html               blog post: "GitOps: The Myth" (Tailwind CDN + Chart.js, standalone)
  styles.css               all portfolio styles (shared by index.html)
  favicon.svg              site favicon
  robots.txt               crawl rules + sitemap reference
  sitemap.xml              sitemap for the two pages
  og.svg / og.png          Open Graph share image (source + rendered 1200x630)
```

- Site is plain HTML + CSS + vanilla JS — **no build step, no framework, no package manager**. Do not introduce one without asking.
- All URLs between pages are **relative** (`styles.css`, `page1.html`) — keep it that way so it works under GitHub Pages sub-paths.
- No external CDNs on `index.html` (icons are inline SVG; fonts fall back to system stacks).

## Run / Verify Locally

```bash
python3 -m http.server 8000 --directory docs
# open http://localhost:8000
```

There are no tests or linters. Verify by opening the page in a browser and checking the console.

## Conventions

### HTML (index.html)
- Layout follows the reference design: sticky nav → status bar → hero (left copy / right stats) → skills strip (expandable panel) → sections with `<p class="section-label">` → quote block → footer.
- Every `<section>` has an `id`; add nav links in the same order. Sections use `scroll-margin-top` instead of a scroll-spy offset hack.
- Icons are **inline SVGs** (stroke `currentColor`, `aria-hidden="true"`). No icon/font CDNs.
- The skills strip is **data-driven**: skill content lives in the `skillData` object at the bottom of the page; panels render from `toggleSkill(key)`. Add skills by adding a chip + a key in `skillData`.
- No comments in code unless explicitly requested.

### CSS (styles.css)
- Single file organized with the reference's conventions; variables live in `:root` (dark defaults) and are overridden in `html[data-theme="light"]`. Never hardcode colors.
- Palette: `--accent: #7B6EF6` (purple), `--accent2: #A89DF8`; status colors `--teal`, `--coral`, `--amber`, `--green` (each with a `-bg` companion). Surfaces: `--bg`, `--bg2`, `--bg3`; hairlines: `--border`, `--border2`.
- Reusable primitives: `.tag` (+ `-purple/-teal/-coral/-amber/-green`), `.lang-pill`, `.venture-row`, `.tl-row`, `.obs-card`, `.svc`, `.stat-row`.
- Keep `prefers-reduced-motion` support (pulse dots) and `:focus-visible` outlines intact.

### JS (inline in index.html)
- Vanilla JS only, no libraries. Theme preference persists in `localStorage('theme')`; the head script sets `data-theme` before paint to avoid flash.

## Content Placeholders

The following content is example/placeholder data the owner must verify or replace before considering the site final:
- **Certifications**: CKA, AWS SA-Associate, Terraform Associate — confirm each credential is actually held; add credential URLs/issuer links as desired.
- **Projects** (`#projects`): "Multi-Cloud IaC Foundation", "Fleet-Wide GitOps Platform", "Observability Stack" are template cards — replace with real repos/details.
- **Skills strip** (`skillData`): impact numbers mirror the site's claims — verify before editing them.
- Stats (10+ years, 300+ clusters, 99.9% uptime) are the owner's claimed results — verify before altering.

## Editing Rules

- Keep the design language consistent: dark-by-default (light theme toggle available), purple accent, hairline borders, mono font (`JetBrains Mono`/`Courier New` fallback) for numbers and labels.
- Never commit generated artifacts (e.g. `og.png`) via conversion scripts unless regenerating intentionally — `og.png` is rendered from `og.svg` (tracked) with `rsvg-convert -w 1200 -h 630 -o docs/og.png docs/og.svg`.
- Commit only when asked.
