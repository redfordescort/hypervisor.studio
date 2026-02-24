# Hypervisor Studio Landing Page — Design

## Overview

Company landing page for hypervisor.studio, served via GitHub Pages. A dark, minimal site showcasing a gallery of projects, with an about page and contact link.

## Tech Stack

**Current:** Plain HTML/CSS, zero dependencies, no build step.

**Future consideration:** If the project list grows significantly, migrate to a static site generator (11ty or Hugo) for templated content management and markdown-driven project pages.

## Site Structure

```
hypervisor.studio/
├── index.html          # Homepage with project gallery
├── about.html          # About page
├── css/style.css       # Single stylesheet
├── images/             # Gallery card images and assets
├── diagrams/           # Excalidraw layout files
├── CNAME               # GitHub Pages custom domain
└── docs/plans/         # Design docs
```

## Visual Design

- **Background:** near-black (#0a0a0a or similar)
- **Text:** off-white body, white headings
- **Accent:** single muted color for hover states (TBD via mockup)
- **Logo font:** Helvetica — "Hypervisor Studio" in white
- **Body font:** Inter (Google Fonts) — clean, free, web-optimized
- **Layout:** centered container, max-width ~1200px, responsive

## Pages

### Header (shared)

Logo left, nav right (Home, About). Static positioning.

### Homepage

Responsive gallery grid: 1 column mobile, 2 columns desktop. Large cards — each has a full-width image on top, title + subtitle beneath on a dark card surface. Subtle hover effect (lift or border glow). With 2 initial items, cards are roughly 500-600px wide.

### About

Centered readable column (~700px max-width). Same header/footer. Content TBD.

### Footer (shared)

Centered, minimal. mailto link to contact@hypervisor.studio. Copyright line.

## Initial Gallery Items

1. **gg! newsletter** — readgg.com
2. **AI Disclosure Framework** — details TBD

## Adding New Projects

Drop an image in `images/`, add a card `<div>` to `index.html` with image path, title, subtitle, and optional link. A Claude skill will be provided to automate this.

## Collaboration

Layout mockups in `diagrams/` as `.excalidraw` files. Edit in excalidraw.com or VS Code extension, commit back for iteration.
