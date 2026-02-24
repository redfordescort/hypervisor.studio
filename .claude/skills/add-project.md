---
name: add-project
description: Add a new project card to the Hypervisor Studio gallery. Use when adding a project to the homepage.
user_invocable: true
---

# Add Project to Gallery

Add a new project card to the homepage gallery at `index.html`.

## Site Nav

All pages use this nav: **Home | Blog | About**. If creating a standalone HTML page for a project, use this header:

```html
<nav class="nav">
  <a href="/">Home</a>
  <a href="/blog/">Blog</a>
  <a href="/about.html">About</a>
</nav>
```

## Process

1. **Gather information.** Ask the user for:
   - **Title** (required): The project name
   - **Subtitle** (required): A short description (one sentence)
   - **Image**: Either a path to an existing image file OR ask if they want a placeholder SVG generated
   - **Link URL** (optional): Where the card should link to. If not provided, use `#`
   - **External link?**: If the URL is external, the link gets `target="_blank" rel="noopener"`

2. **Handle the image.** Either:
   - Copy/move a provided image to `images/` (rename to kebab-case matching the project title)
   - Generate a placeholder SVG at `images/<kebab-name>.svg`:
     ```svg
     <svg xmlns="http://www.w3.org/2000/svg" width="1600" height="1000" viewBox="0 0 1600 1000">
       <rect width="1600" height="1000" fill="#1a1a1a"/>
       <text x="800" y="500" text-anchor="middle" dominant-baseline="middle"
             font-family="Inter, sans-serif" font-size="120" font-weight="bold" fill="#444">
         PROJECT TITLE
       </text>
     </svg>
     ```

3. **Insert the card.** Read `index.html` and insert a new card `<div>` inside `div.gallery`, after the last existing card and before the closing `</div>` of the gallery. Use this exact structure:

   For external links:
   ```html
         <div class="card">
           <a href="URL" target="_blank" rel="noopener">
             <img src="images/FILENAME" alt="TITLE" class="card-image">
             <div class="card-body">
               <div class="card-title">TITLE</div>
               <div class="card-subtitle">SUBTITLE</div>
             </div>
           </a>
         </div>
   ```

   For internal/no links:
   ```html
         <div class="card">
           <a href="URL_OR_HASH">
             <img src="images/FILENAME" alt="TITLE" class="card-image">
             <div class="card-body">
               <div class="card-title">TITLE</div>
               <div class="card-subtitle">SUBTITLE</div>
             </div>
           </a>
         </div>
   ```

4. **Add Google Analytics.** If creating a new HTML page (not just adding a card to index.html), include this in the `<head>` after the stylesheet link:
   ```html
   <!-- Google tag (gtag.js) -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=G-SHYSENGR1Z"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'G-SHYSENGR1Z');
   </script>
   ```

5. **Commit.** Stage the image file and `index.html`, then commit with message: `feat: add PROJECT_TITLE to gallery`
