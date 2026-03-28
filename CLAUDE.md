# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Farinha** is a free software platform for managing permanent archives and collections in cultural institutions. This repository contains the marketing website for the project.

## Development

The project is a **single HTML file** (`index.html`) with no build step. Run a local server to preview:

```bash
python -m http.server 8080
# then open http://localhost:8080/index.html
```

The original source lives in `SiteFarinha_2026.zip`. The working copy is `NovoSite/`, which is also the git repository published at `git@github.com:rsandrade/site-farinha.info.git`.

## File Structure

```
NovoSite/
├── index.html              # entire site (single file)
└── img/
    ├── logo.svg            # Farinha logo (used in navbar); viewBox="47 52 805 207"
    ├── carrossel1.png
    ├── carrossel2.png
    ├── caracteristicas.png # Section image for Características
    ├── objetos-digitais.png # Section image for Objetos Digitais
    ├── ricardo.png
    ├── pablo.png
    ├── beatriz.png
    └── cristian.png
```

## Architecture

Everything is in `index.html`:

- **Tailwind CSS** via CDN; custom config inline in `<script id="tailwind-config">` (colors, fonts, dark mode)
- **No JS framework** — vanilla JS handles: carousel, smooth scroll, active nav highlighting, lazy image fade-in, i18n, mobile menu
- **Images** in `img/` referenced with `./img/`

Page sections in order: sticky glass-morphism nav → hero carousel (4 slides) → Características (`id="atuacao"`, 8 feature cards) → Objetos Digitais (`id="objetos"`, 4 cards) → Equipe de Desenvolvimento (`id="equipe"`, 4 team cards) → CTA/Comece agora (`id="comecar"`) → Contato (`id="contato"`) → footer.

## Carousel Implementation

The carousel uses `transform: translateX` on a `.carousel-track` flex container — **not** `scrollTo` or `overflow-x: auto`. This is intentional; the scroll-based approach had layout and interaction bugs.

```
<div class="relative h-[600px]">           ← fixed height, reference for button positioning
  <div class="overflow-hidden rounded-3xl h-full">
    <div class="carousel-track flex h-full">  ← animated via style.transform
      <!-- 4 slides, each flex-none w-full -->
    </div>
  </div>
  <button class="carousel-btn-prev absolute left-4 top-1/2 -translate-y-1/2 ...">
  <button class="carousel-btn-next absolute right-4 top-1/2 -translate-y-1/2 ...">
</div>
```

**Critical**: buttons must be **outside** the `overflow-hidden` div but **inside** the `relative h-[600px]` div. Placing them inside `overflow-hidden` causes GPU compositing conflicts during the CSS transition.

**Critical**: never add `style.transform` to carousel buttons via JS — it overwrites Tailwind's `-translate-y-1/2` and permanently displaces the buttons.

## Multilingual Support (i18n)

The site supports **PT-BR, EN, ES and RO**. Implementation:

- All translatable elements have a `data-i18n="key"` attribute; `aria-label` uses `data-i18n-aria="key"`
- The `translations` object in the `<script>` block contains all 4 language sets
- `setLanguage(lang)` updates all elements, `<html lang>`, `<title>`, and the active state of language buttons
- Language preference is persisted in `localStorage` under `farinha-lang`; browser language is auto-detected on first visit
- **Desktop**: language switcher (`PT | EN | ES | RO`) in the navbar
- **Mobile**: language switcher inside the hamburger menu

**Terminology conventions:**
- PT: Nobrade (for fonds/arrangement), ISDIAH (for institutions), ISAD(g) not used
- EN/ES/RO: ISAD(g) replaces Nobrade in carousel slide 2 and Multiacervos card; ISDIAH used for Multi-institucional card

## Mobile Navigation

A hamburger menu (`id="mobile-menu"`) slides down from the top on mobile (`md:hidden`). It contains:
- All nav links (same anchors as desktop)
- Download button
- Language switcher

The hamburger button (`id="hamburger-btn"`) calls `toggleMobileMenu()`. Tapping a link or language closes the menu via `closeMobileMenu()`. The backdrop also closes it.

**Critical**: the sticky sidebar (title + image column in Características and Objetos Digitais) uses `lg:sticky lg:top-32` — NOT `sticky top-32`. On mobile, sticky causes the sidebar to block the cards scrolling underneath.

## Design System ("The Precision Architect")

- **No 1px borders** — use background color shifts for separation
- Primary teal: `#006970`; Surface: `#fbf9f8`
- Headlines: Plus Jakarta Sans (`font-headline`); Body: Inter (`font-body`)
- Transitions: `cubic-bezier(0.4, 0, 0.2, 1)` at 0.3s
- Section spacing: `py-32`

## Known Pitfalls

- `button { transition: all }` and `button:active { transform: scale(...) }` in global CSS break carousel button positioning — use `transition-colors` on buttons and avoid global transform on `:active`.
- Any JS that sets `this.style.transform` on buttons (e.g. click feedback) will override Tailwind transform utilities and displace absolutely-positioned buttons permanently.
- The logo SVG (`img/logo.svg`) viewBox is `47 52 805 207` — trimmed to remove whitespace. Do not reset to the original `0 0 900 314.66`.
- Carousel overlay gradient: `from-on-surface/90 via-on-surface/40 to-on-surface/10` — high opacity needed because carousel images 1 and 2 are predominantly white; white text on white background requires a strong dark overlay.

## Git

Remote: `git@github.com:rsandrade/site-farinha.info.git` (branch: `master`)
Tag `v1.0-pre-hamburger` marks the state before the hamburger menu refactor.

## Content Update Workflow

Edit `NovoSite/index.html` directly. When updating text, update both the static HTML (default PT content) and the corresponding key in all 4 language blocks of the `translations` object. After edits, commit and push.
