---
name: update-page
description: Convert a markdown file from content/ to its HTML page. Use when updating the about page, framework pages, or any content page from markdown source.
user_invocable: true
---

# Update Page from Markdown

Convert a markdown file in `content/` into a full HTML page using the site template.

## Steps

### 1. Identify the markdown file

The user specifies which file to convert (e.g., `content/about.md`). If not specified, ask. The file must be a `.md` file inside `content/`.

### 2. Read and parse the markdown file

Read the file. Extract YAML frontmatter (the block between the opening `---` and closing `---` at the top). Pull out:
- `title` — used in `<title>` and can be used as page heading
- `description` — used in `<meta name="description">`

Everything after the closing `---` is the markdown body.

### 3. Determine output path

Strip the `content/` prefix and change `.md` to `.html`:

| Source | Output |
|---|---|
| `content/about.md` | `about.html` |
| `content/ai-disclosure/index.md` | `ai-disclosure/index.html` |
| `content/ai-disclosure/principles.md` | `ai-disclosure/principles.html` |

General rule: `content/PATH.md` → `PATH.html`

### 4. Convert markdown to HTML

Transform the markdown body into HTML elements:

- `# Heading` → `<h1>Heading</h1>` (and `##` → `<h2>`, `###` → `<h3>`, etc.)
- Paragraphs (text blocks separated by blank lines) → `<p>text</p>`
- `**bold**` → `<strong>bold</strong>`
- `*italic*` → `<em>italic</em>`
- `[text](url)` → `<a href="url">text</a>`
- `- item` or `* item` → wrap consecutive items in `<ul><li>item</li></ul>`
- `1. item` → wrap consecutive items in `<ol><li>item</li></ol>`
- `` `code` `` → `<code>code</code>`
- Code blocks (triple backtick) → `<pre><code>content</code></pre>`
- `> quote` → `<blockquote><p>quote</p></blockquote>`
- `![alt](src)` → `<img src="src" alt="alt">`

Process inline formatting (bold, italic, links, inline code) within block elements like paragraphs, list items, and headings.

### 5. Wrap in site template

Build the full HTML page using this exact template. Replace `TITLE`, `DESCRIPTION`, and `CONVERTED_HTML` with the values from the markdown file.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TITLE — Hypervisor Studio</title>
  <meta name="description" content="DESCRIPTION">
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
      <a href="/blog/">Blog</a>
      <a href="/about.html">About</a>
    </nav>
  </header>

  <main>
    <div class="page-content">
      CONVERTED_HTML
    </div>
  </main>

  <footer class="footer">
    <a href="mailto:contact@hypervisor.studio">contact@hypervisor.studio</a><span class="footer-sep">&middot;</span>&copy; 2026 Hypervisor Studio
  </footer>
</body>
</html>
```

Template rules:
- **TITLE**: from frontmatter `title`
- **DESCRIPTION**: from frontmatter `description`
- **CSS path**: always use absolute path `/css/style.css` regardless of page depth
- **About page nav link**: if the output file is `about.html`, add `class="active"` to the About nav link: `<a href="/about.html" class="active">About</a>`
- All asset and nav paths use absolute paths (starting with `/`) so pages work at any directory depth

### 6. Write the HTML file

Write the assembled HTML to the output path determined in step 3.

### 7. Commit

Commit the changed file with message: `content: update PAGE_NAME from markdown`

where PAGE_NAME is a human-readable name for the page (e.g., "about page", "AI disclosure index").
