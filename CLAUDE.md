# CLAUDE.md — AI Assistant Guide for Portafolio

## Project Overview

Personal portfolio website for **Felipe Moena**, a Civil Construction Engineer (Constructor Civil) based in Santiago, Chile. The site showcases construction projects, Power BI dashboards, professional experience, and certifications.

**Live site type:** Static single-page HTML portfolio
**Languages:** Bilingual (Spanish / English)

## Architecture

This is a **zero-dependency, single-file project** with no build system, no package manager, and no framework.

```
Portafolio/
├── index.html        # Entire application (HTML + CSS + JS, ~1267 lines)
├── CLAUDE.md         # This file
└── .git/
```

### File Structure Within `index.html`

| Lines     | Content                                         |
|-----------|-------------------------------------------------|
| 1–7       | Document head, meta tags, title                 |
| 8–649     | Embedded `<style>` block (all CSS)              |
| 650–670   | Navigation bar with language switcher           |
| 672–708   | Hero section (title, stats)                     |
| 710–843   | Construction projects section (#proyectos)      |
| 846–953   | Power BI portfolio section (#powerbi)           |
| 955–1093  | Experience / career timeline (#experiencia)     |
| 1095–1160 | About section with certifications (#sobre-mi)   |
| 1162–1199 | Contact section (#contacto)                     |
| 1201–1205 | Footer                                          |
| 1207–1267 | Embedded `<script>` block (all JavaScript)      |

## Technology Stack

- **HTML5** — Semantic sections, `data-*` attributes for i18n
- **CSS3** — Custom properties, Flexbox, CSS Grid, media queries, animations
- **Vanilla JavaScript (ES6)** — No frameworks or libraries
- **Google Fonts** — Inter font family (CDN)
- **Cloudflare Email Protection** — Obfuscated email address

## Key Conventions

### CSS

- **CSS Custom Properties** defined in `:root`:
  - `--primary: #0a0a0a` (black)
  - `--secondary: #666666` (gray)
  - `--accent: #FF6B35` (orange)
  - `--bg: #ffffff`, `--bg-alt: #f8f8f8`, `--border: #e0e0e0`
- **Class naming:** Kebab-case (e.g., `.project-card`, `.hero-content`, `.nav-center`)
- **Layout:** Flexbox for nav/hero, CSS Grid for project/Power BI cards
- **Responsive breakpoint:** Single breakpoint at `768px`
- **Animations:** `fade-in` class with Intersection Observer; transitions use `0.3s` default

### Internationalization (i18n)

The bilingual system uses **HTML `data-lang` attributes** — no i18n library.

**Pattern:** Duplicate elements with `data-lang="es"` and `data-lang="en"`:
```html
<h2 data-lang="es">Texto en español</h2>
<h2 data-lang="en">English text</h2>
```

**CSS visibility toggle** based on `<html lang="...">`:
```css
[data-lang]:not([data-lang=""]) { display: none; }
[lang="es"] [data-lang="es"],
[lang="en"] [data-lang="en"] { display: block; }
```

**Language state** is stored in `localStorage` under key `preferredLanguage`. Default: `es`.

**When adding new content:** Always provide both `data-lang="es"` and `data-lang="en"` variants.

### JavaScript

- Language switcher: Click handlers on `[data-lang-switch]` elements
- Scroll animations: `IntersectionObserver` with `.fade-in` / `.visible` classes
- Smooth scroll: Event listener on `nav a[href^="#"]` links
- Mobile menu: Toggle `.active` class on `.nav-center`
- No state management library — `localStorage` only

### Navigation (Hash-based)

| Hash           | Section                   |
|----------------|---------------------------|
| `#proyectos`   | Construction Projects     |
| `#powerbi`     | Power BI Portfolio        |
| `#experiencia` | Professional Experience   |
| `#sobre-mi`    | About / Certifications    |
| `#contacto`    | Contact Information       |

## Development Workflow

### Running Locally

No build step required. Open `index.html` directly in a browser, or use any static server:

```bash
# Python
python3 -m http.server 8000

# Node.js (if npx available)
npx serve .
```

### Making Changes

1. All edits go into `index.html` — there is no multi-file structure
2. CSS changes: Edit the `<style>` block (lines 8–649)
3. Content changes: Edit HTML sections (lines 650–1205)
4. Behavior changes: Edit the `<script>` block (lines 1207–1267)

### Deployment

Static file hosting. No build artifacts, no CI/CD pipeline. Compatible with:
- GitHub Pages
- Netlify
- Vercel
- Any static web host

## Content Sections

### Projects (5 cards)
1. Hospital Buin Paine — Healthcare project management
2. Enel 420MW Solar Plant — Photovoltaic civil works
3. 12-Story Building (126 apartments) — High-rise finishing
4. Telecommunications Infrastructure — Mining monopole installations
5. Santiago Metro Line 6 — Tunnel construction (ITO)

### Power BI Dashboards (4 cards)
1. Hospital Management Dashboard
2. Solar Plant Analysis
3. BJJ Academy Financial Model
4. Construction Project Control

### Experience (6 roles, 2014–Present)
Chronological career timeline from ITO at Santiago Metro through current hospital project management.

### Certifications
- Civil Construction Engineer (USACH, 2015)
- Construction Technologist (USACH, 2008)
- PMP Certification (in progress)
- Microsoft Power BI (certified)
- Microsoft Project (certified)
- Advanced Excel (certified)

## Important Notes for AI Assistants

1. **Single-file architecture**: Do not split into multiple files unless explicitly requested. The current monolithic structure is intentional for simplicity.
2. **Always bilingual**: Every user-visible text must have both `data-lang="es"` and `data-lang="en"` variants.
3. **No build tools**: Do not introduce npm, webpack, vite, or other tooling unless requested.
4. **Inline CSS/JS**: Styles and scripts are embedded in `index.html`, not in separate files.
5. **Cloudflare email protection**: The email in the contact section uses Cloudflare's obfuscation script. Do not replace with a plain `mailto:` link.
6. **Gradient backgrounds**: Project cards use CSS gradients as placeholder images (no actual image files).
7. **Emoji icons**: Sections use emoji characters as icons (not icon libraries).
8. **No testing infrastructure**: There are no tests. Manual browser testing is the verification method.
9. **Personal data**: The site contains real contact information (phone, LinkedIn, address). Handle with care.
