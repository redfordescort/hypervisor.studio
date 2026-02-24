---
name: add-blog-post
description: Create a blog post from markdown and regenerate the blog index. Use when adding a new blog post.
user_invocable: true
---

# Add Blog Post

Create a blog post HTML page from a markdown source file and regenerate the blog index.

## Process

1. **Identify the markdown file.** Either:
   - The user specifies a path to an existing `.md` file in `content/blog/`
   - The user wants to write a new post — create the markdown file first at `content/blog/YYYY-MM-DD-slug.md`

   Expected filename format: `content/blog/YYYY-MM-DD-slug.md`

2. **Read the markdown file.** Parse the YAML frontmatter and body:
   ```yaml
   ---
   title: Post Title
   date: 2026-02-24
   excerpt: A short description of the post.
   ---
   ```
   Everything after the closing `---` is the markdown body.

3. **Convert markdown to HTML.** Apply these conversion rules to the body:
   - `# Heading` → `<h1>` through `###### Heading` → `<h6>`
   - Paragraphs (blank-line separated text) → `<p>`
   - `**bold**` → `<strong>`, `*italic*` → `<em>`
   - `[text](url)` → `<a href="url">text</a>`
   - Unordered lists (`- item`) → `<ul><li>`
   - Ordered lists (`1. item`) → `<ol><li>`
   - `` `inline code` `` → `<code>`
   - Fenced code blocks (triple backticks) → `<pre><code>`
   - `> blockquote` → `<blockquote>`
   - `![alt](src)` → `<img src="src" alt="alt">`

4. **Write the post HTML file.** Derive the output path from the markdown filename:
   `content/blog/YYYY-MM-DD-slug.md` → `blog/YYYY-MM-DD-slug.html`

   Format the date as human-readable (e.g., "February 24, 2026").

   Use this exact template:

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <title>POST_TITLE — Hypervisor Studio</title>
     <meta name="description" content="EXCERPT">
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
         <h1>POST_TITLE</h1>
         <div class="post-meta">DATE_FORMATTED</div>
         CONVERTED_HTML_CONTENT
       </div>
     </main>

     <footer class="footer">
       <a href="mailto:contact@hypervisor.studio">contact@hypervisor.studio</a><span class="footer-sep">&middot;</span>&copy; 2026 Hypervisor Studio
     </footer>
   </body>
   </html>
   ```

   Replace:
   - `POST_TITLE` with the title from frontmatter
   - `EXCERPT` with the excerpt from frontmatter
   - `DATE_FORMATTED` with the human-readable date (e.g., "February 24, 2026")
   - `CONVERTED_HTML_CONTENT` with the converted HTML from step 3

5. **Regenerate the blog index.** Read ALL `.md` files in `content/blog/`, extract frontmatter from each (title, date, excerpt), sort by date descending (newest first). Write `blog/index.html` using this template:

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
         <ul class="post-list">
           <!-- Repeat this <li> for each post, sorted by date descending (newest first) -->
           <li>
             <a href="/blog/YYYY-MM-DD-slug.html">
               <div class="post-list-title">Post Title</div>
               <div class="post-list-date">February 24, 2026</div>
               <div class="post-list-excerpt">The excerpt text.</div>
             </a>
           </li>
         </ul>
       </div>
     </main>

     <footer class="footer">
       <a href="mailto:contact@hypervisor.studio">contact@hypervisor.studio</a><span class="footer-sep">&middot;</span>&copy; 2026 Hypervisor Studio
     </footer>
   </body>
   </html>
   ```

   For each post:
   - Derive the HTML link from the markdown filename: `content/blog/YYYY-MM-DD-slug.md` → `/blog/YYYY-MM-DD-slug.html`
   - Format dates as "Month DD, YYYY" (e.g., "February 24, 2026")

6. **Commit.** Stage the markdown source file (if new), the post HTML file, and `blog/index.html`. Commit with message: `post: POST_TITLE`
