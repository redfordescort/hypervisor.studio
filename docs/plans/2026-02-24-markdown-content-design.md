# Markdown Content System — Design

## Overview

Add markdown-based content authoring to the Hypervisor Studio site. Content lives as `.md` files in `content/`, Claude skills convert them to HTML pages using the site's template (header, nav, footer, GA, styles).

## Content Directory Structure

```
content/
├── about.md                              # About page
├── blog/
│   ├── 2026-02-24-ai-disclosure-framework.md   # Blog posts
│   └── ...future posts
└── ai-disclosure/
    ├── index.md                          # Framework homepage
    └── ...future subpages
```

## How It Works

- Author writes/edits `.md` files in `content/`
- Each file has YAML frontmatter (title, subtitle, date, excerpt — varies by type)
- Claude skills read the markdown, convert to HTML, wrap in site template, write `.html` output
- Blog index page regenerated on each post addition

## Skills

- **update-page** — Converts a single markdown file to its HTML page (about, framework pages)
- **add-blog-post** — Creates a blog post from markdown, regenerates the blog index
- **add-project** — Already exists, unchanged

## Navigation

Header: Home | Blog | About (on all pages)

## New Pages

- `/blog/index.html` — Post listing with title, date, excerpt
- `/blog/YYYY-MM-DD-slug.html` — Individual blog posts
- `/ai-disclosure/index.html` — Framework homepage
- `/ai-disclosure/*.html` — Framework subpages

## CSS Additions

- `.post-list` — Blog index styling
- `.post-meta` — Date display
- `.post-content` / `.page-content` — Prose column styling (extending existing .about-content pattern)

## Markdown Features

Standard markdown converted by Claude: headings, paragraphs, bold/italic, links, lists, code blocks, images. No library needed — Claude parses markdown natively.

## Future

If the volume of content makes skill-based conversion cumbersome, migrate to a static site generator (11ty or Hugo) or a Python build script. See original design doc for notes.
