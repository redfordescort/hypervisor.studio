# Markdown Content System — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add blog section, content/ directory for markdown authoring, CSS for prose/blog pages, Claude skills for markdown-to-HTML conversion, and update nav on all pages.

**Architecture:** Markdown files with YAML frontmatter live in `content/`. Claude skills read the markdown, convert to HTML, and write complete HTML pages using the site's shared template (head imports, header, footer, GA). Blog index is regenerated from all post frontmatter when a post is added.

**Tech Stack:** HTML5, CSS3, Markdown (authored by user, converted by Claude)

---

### Task 1: Update Nav on All Pages

**Files:**
- Modify: `index.html`
- Modify: `about.html`

**Step 1: Update nav in index.html**

Change the nav section from:
```html
    <nav class="nav">
      <a href="/" class="active">Home</a>
      <a href="/about.html">About</a>
    </nav>
```
To:
```html
    <nav class="nav">
      <a href="/" class="active">Home</a>
      <a href="/blog/">Blog</a>
      <a href="/about.html">About</a>
    </nav>
```

**Step 2: Update nav in about.html**

Change from:
```html
    <nav class="nav">
      <a href="/">Home</a>
      <a href="/about.html" class="active">About</a>
    </nav>
```
To:
```html
    <nav class="nav">
      <a href="/">Home</a>
      <a href="/blog/">Blog</a>
      <a href="/about.html" class="active">About</a>
    </nav>
```

**Step 3: Commit**

```bash
git add index.html about.html
git commit -m "feat: add Blog to nav on all pages"
```

---

### Task 2: Add CSS for Prose and Blog Pages

**Files:**
- Modify: `css/style.css`

**Step 1: Add prose content styles after the existing .about-content section (after line 167)**

These styles handle rendered markdown content on blog posts, framework pages, and the about page. Add after the `.about-content p` rule:

```css
/* Page content (prose pages - blog posts, framework, etc.) */
.page-content {
  max-width: var(--content-width);
  margin: 0 auto;
}

.page-content h1 {
  font-size: 2rem;
  font-weight: bold;
  color: var(--text-heading);
  margin-bottom: 0.5rem;
}

.page-content h2 {
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-heading);
  margin-top: 2rem;
  margin-bottom: 0.75rem;
}

.page-content h3 {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--text-heading);
  margin-top: 1.5rem;
  margin-bottom: 0.5rem;
}

.page-content p {
  margin-bottom: 1rem;
}

.page-content ul,
.page-content ol {
  margin-bottom: 1rem;
  padding-left: 1.5rem;
}

.page-content li {
  margin-bottom: 0.25rem;
}

.page-content blockquote {
  border-left: 3px solid var(--border);
  padding-left: 1rem;
  color: var(--text-muted);
  margin-bottom: 1rem;
}

.page-content code {
  background: var(--surface);
  padding: 0.15rem 0.4rem;
  border-radius: 4px;
  font-size: 0.9em;
}

.page-content pre {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 1rem;
  overflow-x: auto;
  margin-bottom: 1rem;
}

.page-content pre code {
  background: none;
  padding: 0;
  border-radius: 0;
}

.page-content img {
  max-width: 100%;
  border-radius: 8px;
  margin-bottom: 1rem;
}

.page-content strong {
  color: var(--text-heading);
}

.page-content a {
  color: var(--accent);
}

.page-content a:hover {
  opacity: 0.8;
}

/* Post meta (date, etc.) */
.post-meta {
  color: var(--text-muted);
  font-size: 0.9rem;
  margin-bottom: 2rem;
}

/* Blog index - post list */
.post-list {
  list-style: none;
  padding: 0;
}

.post-list li {
  border-bottom: 1px solid var(--border);
  padding: 1.5rem 0;
}

.post-list li:last-child {
  border-bottom: none;
}

.post-list a {
  color: inherit;
  text-decoration: none;
  display: block;
}

.post-list a:hover .post-list-title {
  color: var(--accent);
}

.post-list-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--text-heading);
  margin-bottom: 0.25rem;
  transition: color 0.2s;
}

.post-list-date {
  font-size: 0.85rem;
  color: var(--text-muted);
  margin-bottom: 0.5rem;
}

.post-list-excerpt {
  font-size: 0.95rem;
  color: var(--text);
}
```

**Step 2: Commit**

```bash
git add css/style.css
git commit -m "feat: add CSS for prose content and blog post list"
```

---

### Task 3: Create Content Directory with About Markdown

**Files:**
- Create: `content/about.md`

**Step 1: Create the about markdown file with frontmatter**

```markdown
---
title: About
description: About Hypervisor Studio.
---

Hypervisor Studio builds projects at the intersection of technology, media, and AI.

More details coming soon.
```

This mirrors the current about.html content. The update-page skill will use this as the source of truth going forward.

**Step 2: Commit**

```bash
git add content/about.md
git commit -m "feat: add content directory with about page markdown"
```

---

### Task 4: Create Blog Index Page

**Files:**
- Create: `blog/index.html`

**Step 1: Create an empty blog index page**

This is the initial blog landing page with no posts yet. It will be regenerated by the add-blog-post skill each time a post is added.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Blog — Hypervisor Studio</title>
  <meta name="description" content="Blog posts from Hypervisor Studio.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="/css/style.css">
  <!-- Google tag (gtag.js) -->
  <script async src="https://www.googletagmanager.com/gtag/js?id=G-SHYSENGR1Z"></script>
  <script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-SHYSENGR1Z');
  </script>
</head>
<body>
  <header class="header">
    <a class="logo" href="/">Hypervisor Studio</a>
    <nav class="nav">
      <a href="/">Home</a>
      <a href="/blog/" class="active">Blog</a>
      <a href="/about.html">About</a>
    </nav>
  </header>

  <main>
    <div class="page-content">
      <h1>Blog</h1>
      <p class="post-meta">No posts yet.</p>
    </div>
  </main>

  <footer class="footer">
    <a href="mailto:contact@hypervisor.studio">contact@hypervisor.studio</a><span class="footer-sep">&middot;</span>&copy; 2026 Hypervisor Studio
  </footer>
</body>
</html>
```

Note: CSS and JS paths use absolute paths (`/css/style.css`) since blog pages are in a subdirectory.

**Step 2: Commit**

```bash
git add blog/index.html
git commit -m "feat: add blog index page"
```

---

### Task 5: Create update-page Skill

**Files:**
- Create: `.claude/skills/update-page.md`

**Step 1: Create the skill**

The skill should:
- Accept a path to a markdown file in `content/` (or prompt for one)
- Read the markdown file and its frontmatter
- Determine the output HTML path:
  - `content/about.md` → `about.html`
  - `content/ai-disclosure/index.md` → `ai-disclosure/index.html`
  - `content/ai-disclosure/foo.md` → `ai-disclosure/foo.html`
- Convert the markdown body to HTML (headings → h tags, paragraphs → p tags, bold/italic, links, lists, code blocks, blockquotes, images)
- Wrap in the site template: head (with correct title from frontmatter, description, Google Fonts, stylesheet using absolute path if in subdirectory, GA tag), header with nav (no active class on nav unless matching), main with `div.page-content`, footer
- Write the HTML file
- Commit

**Step 2: Commit**

```bash
git add .claude/skills/update-page.md
git commit -m "feat: add update-page skill for markdown to HTML conversion"
```

---

### Task 6: Create add-blog-post Skill

**Files:**
- Create: `.claude/skills/add-blog-post.md`

**Step 1: Create the skill**

The skill should:
- Accept a path to a markdown file in `content/blog/` (or prompt for one)
- Read the markdown file. Expected frontmatter:
  ```yaml
  ---
  title: Post Title
  date: 2026-02-24
  excerpt: A short description of the post.
  ---
  ```
- Determine output path: `content/blog/YYYY-MM-DD-slug.md` → `blog/YYYY-MM-DD-slug.html`
- Convert markdown body to HTML
- Wrap in site template with `.page-content` container. Include `.post-meta` div showing the formatted date above the content
- Write the post HTML file
- Regenerate `blog/index.html`: read all `.md` files in `content/blog/`, extract frontmatter (title, date, excerpt), sort by date descending, build the index page with `ul.post-list` containing an `li` per post with `.post-list-title`, `.post-list-date`, `.post-list-excerpt`, each linking to the post HTML
- Commit both the post HTML and updated blog index

**Step 2: Commit**

```bash
git add .claude/skills/add-blog-post.md
git commit -m "feat: add blog post skill with index regeneration"
```

---

### Task 7: Update AI Disclosure Card Link

**Files:**
- Modify: `index.html`

**Step 1: Update the AI Disclosure Framework card link**

Change the card's href from `#` to `/ai-disclosure/` so it links to the framework section once it exists:

```html
      <div class="card">
        <a href="/ai-disclosure/">
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: link AI Disclosure card to framework section"
```

---

### Task 8: Update add-project Skill

**Files:**
- Modify: `.claude/skills/add-project.md`

**Step 1: Update the nav template in the skill**

The card HTML template in the skill doesn't need changes (cards don't have nav). But add a note that the nav on all pages is now: Home | Blog | About. Any new standalone HTML page must include Blog in the nav.

**Step 2: Commit**

```bash
git add .claude/skills/add-project.md
git commit -m "chore: update add-project skill with current nav structure"
```
