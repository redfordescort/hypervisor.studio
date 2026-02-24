# Hypervisor Studio Landing Page — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a dark, minimal GitHub Pages site with a project gallery homepage, about page, and contact footer.

**Architecture:** Plain HTML/CSS, no build step. Two HTML pages sharing a stylesheet. Inter font from Google Fonts. Gallery uses CSS Grid. Responsive via media queries. GitHub Pages serves from `main` branch with custom domain.

**Tech Stack:** HTML5, CSS3, Google Fonts (Inter)

---

### Task 1: CSS Foundation

**Files:**
- Create: `css/style.css`

**Step 1: Create the stylesheet with reset, variables, typography, and layout**

```css
/* Reset & base */
*, *::before, *::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    --bg: #0a0a0a;
    --surface: #141414;
    --border: #222222;
    --text: #d4d4d4;
    --text-heading: #ffffff;
    --text-muted: #777777;
    --accent: #4a9eff;
    --max-width: 1200px;
    --content-width: 700px;
}

html {
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

body {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    background-color: var(--bg);
    color: var(--text);
    line-height: 1.6;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

a {
    color: var(--accent);
    text-decoration: none;
    transition: opacity 0.2s;
}

a:hover {
    opacity: 0.8;
}

/* Header */
.header {
    padding: 1.5rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: var(--max-width);
    width: 100%;
    margin: 0 auto;
}

.logo {
    font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
    font-size: 1.25rem;
    font-weight: 700;
    color: var(--text-heading);
    text-decoration: none;
    letter-spacing: -0.02em;
}

.nav {
    display: flex;
    gap: 2rem;
}

.nav a {
    color: var(--text-muted);
    font-size: 0.9rem;
    transition: color 0.2s;
}

.nav a:hover,
.nav a.active {
    color: var(--text-heading);
}

/* Main content */
main {
    flex: 1;
    max-width: var(--max-width);
    width: 100%;
    margin: 0 auto;
    padding: 2rem;
}

/* Gallery grid */
.gallery {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2rem;
    margin-top: 1rem;
}

.card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    transition: transform 0.2s, border-color 0.2s;
}

.card:hover {
    transform: translateY(-4px);
    border-color: #333333;
}

.card a {
    color: inherit;
    text-decoration: none;
}

.card-image {
    width: 100%;
    aspect-ratio: 16 / 10;
    object-fit: cover;
    display: block;
}

.card-body {
    padding: 1.5rem;
}

.card-title {
    font-size: 1.25rem;
    font-weight: 600;
    color: var(--text-heading);
    margin-bottom: 0.25rem;
}

.card-subtitle {
    font-size: 0.95rem;
    color: var(--text-muted);
}

/* About page */
.about-content {
    max-width: var(--content-width);
    margin: 0 auto;
}

.about-content h1 {
    font-size: 2rem;
    font-weight: 700;
    color: var(--text-heading);
    margin-bottom: 1.5rem;
}

.about-content p {
    margin-bottom: 1rem;
}

/* Footer */
.footer {
    padding: 2rem;
    text-align: center;
    color: var(--text-muted);
    font-size: 0.85rem;
}

.footer a {
    color: var(--text-muted);
    transition: color 0.2s;
}

.footer a:hover {
    color: var(--accent);
}

.footer-sep {
    margin: 0 0.5rem;
}

/* Responsive */
@media (max-width: 768px) {
    .gallery {
        grid-template-columns: 1fr;
    }

    .header {
        padding: 1rem 1.25rem;
    }

    main {
        padding: 1.25rem;
    }
}
```

**Step 2: Commit**

```bash
git add css/style.css
git commit -m "feat: add base stylesheet with dark theme and gallery grid"
```

---

### Task 2: Homepage

**Files:**
- Create: `index.html`

**Step 1: Create the homepage with header, gallery, and footer**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hypervisor Studio</title>
    <meta name="description" content="Hypervisor Studio — projects at the intersection of technology, media, and AI.">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header class="header">
        <a href="/" class="logo">Hypervisor Studio</a>
        <nav class="nav">
            <a href="/" class="active">Home</a>
            <a href="/about.html">About</a>
        </nav>
    </header>

    <main>
        <div class="gallery">
            <div class="card">
                <a href="https://readgg.com" target="_blank" rel="noopener">
                    <img src="images/gg-newsletter.png" alt="gg! newsletter" class="card-image">
                    <div class="card-body">
                        <div class="card-title">gg! newsletter</div>
                        <div class="card-subtitle">A newsletter about games, tech, and culture.</div>
                    </div>
                </a>
            </div>

            <div class="card">
                <a href="#">
                    <img src="images/ai-disclosure.png" alt="AI Disclosure Framework" class="card-image">
                    <div class="card-body">
                        <div class="card-title">AI Disclosure Framework</div>
                        <div class="card-subtitle">A practical framework for transparent AI use.</div>
                    </div>
                </a>
            </div>
        </div>
    </main>

    <footer class="footer">
        <a href="mailto:contact@hypervisor.studio">contact@hypervisor.studio</a>
        <span class="footer-sep">&middot;</span>
        &copy; 2026 Hypervisor Studio
    </footer>
</body>
</html>
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add homepage with project gallery"
```

---

### Task 3: About Page

**Files:**
- Create: `about.html`

**Step 1: Create the about page with placeholder content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>About — Hypervisor Studio</title>
    <meta name="description" content="About Hypervisor Studio.">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <header class="header">
        <a href="/" class="logo">Hypervisor Studio</a>
        <nav class="nav">
            <a href="/">Home</a>
            <a href="/about.html" class="active">About</a>
        </nav>
    </header>

    <main>
        <div class="about-content">
            <h1>About</h1>
            <p>Hypervisor Studio builds projects at the intersection of technology, media, and AI.</p>
            <p>More details coming soon.</p>
        </div>
    </main>

    <footer class="footer">
        <a href="mailto:contact@hypervisor.studio">contact@hypervisor.studio</a>
        <span class="footer-sep">&middot;</span>
        &copy; 2026 Hypervisor Studio
    </footer>
</body>
</html>
```

**Step 2: Commit**

```bash
git add about.html
git commit -m "feat: add about page with placeholder content"
```

---

### Task 4: Placeholder Images

**Files:**
- Create: `images/gg-newsletter.png` (placeholder)
- Create: `images/ai-disclosure.png` (placeholder)

**Step 1: Generate simple placeholder images**

Create two 1600x1000 placeholder PNGs with centered text on a dark background using Python + Pillow (or similar). These are temporary — user will replace with real images.

If Pillow is not available, create minimal SVG placeholders instead:

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="1600" height="1000" viewBox="0 0 1600 1000">
  <rect width="1600" height="1000" fill="#1a1a1a"/>
  <text x="800" y="500" text-anchor="middle" dominant-baseline="middle"
        font-family="Inter, sans-serif" font-size="48" fill="#444">
    gg! newsletter
  </text>
</svg>
```

Save as `.svg` and update `index.html` references if using SVG instead of PNG.

**Step 2: Commit**

```bash
git add images/
git commit -m "feat: add placeholder gallery images"
```

---

### Task 5: GitHub Pages Config

**Files:**
- Create: `CNAME`

**Step 1: Create CNAME for custom domain**

```
hypervisor.studio
```

**Step 2: Commit**

```bash
git add CNAME
git commit -m "feat: add CNAME for custom domain"
```

**Step 3: Push to GitHub and enable Pages**

```bash
git push -u origin main
```

Then the user configures GitHub Pages in repo settings (Source: main branch, root directory) and DNS records for `hypervisor.studio` pointing to GitHub Pages IPs.

---

### Task 6: Claude Skill for Adding Projects

**Files:**
- Create: `.claude/skills/add-project.md`

**Step 1: Create the skill file**

The skill should:
- Ask for project title, subtitle, image filename, and optional link URL
- Add the image to `images/`
- Insert a new card `<div>` into the gallery in `index.html`
- Commit the changes

See design doc for card HTML structure.

**Step 2: Test the skill by invoking it**

Verify it produces valid HTML and inserts in the right location.

**Step 3: Commit**

```bash
git add .claude/skills/add-project.md
git commit -m "feat: add Claude skill for creating new project cards"
```

---

### Task 7: Final Review & Push

**Step 1: Open `index.html` in browser to verify**

Check: dark background, gallery layout, hover effects, responsive on mobile width, links work, footer mailto works.

**Step 2: Open `about.html` in browser to verify**

Check: same header/footer, centered content column, nav active state correct.

**Step 3: Final commit if any tweaks needed, then push**

```bash
git push origin main
```
