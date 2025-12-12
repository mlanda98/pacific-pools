Purpose
-------
This file guides AI coding agents working on the `pacific-pools` repo. It contains the "big picture" of the project, important local conventions, preview/build workflow, and concrete examples from the codebase so an agent can be immediately productive.

Project overview
----------------
- Small static marketing website for a pool remodeling business.
- Key files/directories:
  - `index.html` — main landing page (hero, services, about preview, footer).
  - `styles.css` — global styles for the site.
  - `images/` — all image assets (logo, hero, service thumbnails).
- No build system, package.json, or server-side code detected. Edits should preserve static-site assumptions.

Important patterns & conventions
-------------------------------
- Asset locations: images live in `images/` and are referenced directly (e.g. `images/hero.png`, `images/logo.png`). Preserve filenames and extensions when editing assets.
- Links and paths:
  - HTML uses relative links to other pages (e.g. `about.html`, `services.html`, `quote.html`). These pages may be referenced before they exist; keep link format consistent.
  - Note `index.html` includes the stylesheet with a leading slash: `<link rel="stylesheet" href="/styles.css" />`. When running locally or hosting from a sub-path, prefer `href="styles.css"` to avoid root-path issues.
- Inline styles: the hero background is set inline in `index.html`: `style="background-image: url('images/hero.png')"`. When changing images, update both the file and any inline references.
- HTML structure examples (from `index.html`):
  - Navigation: `<nav class="navbar">` contains `.logo` and `.nav-links`.
  - Hero: `<section class="hero">` wraps `.hero-content`, `h1`, `p`, and `.hero-button` links.
  - Services grid: `.services-grid` contains `.service-card` elements; each card uses an inner `.service-card-content` with an `img`, `h3`, `p`, and action `<a>`.

Build / preview / debug
-----------------------
- No build step. To preview locally:
  - Quick static server (Python 3): `python3 -m http.server 8000` then open `http://localhost:8000/index.html`.
  - macOS quick open: `open index.html` (works but may not resolve root-path `href="/styles.css"`).
  - Alternatively install `serve` and run `npx serve` for more robust static hosting.
- Debugging hints:
  - Use browser DevTools Console / Network to identify 404s for missing images/CSS (common when paths use a leading `/`).
  - Check `images/` for exact filename (case-sensitive on some hosts).

Editing guidelines for agents
----------------------------
- Preserve existing file layout and filenames for images and referenced pages unless the change is accompanied by updates to all references.
- If adding new pages (e.g. `about.html`, `services.html`), follow the same structural patterns used in `index.html` (header nav, `section` blocks, `footer`) and reuse class names in `styles.css`.
- When changing `href` or image paths, test by spinning up a static server to ensure paths resolve.
- Avoid introducing a JS build system or Node tooling unless explicitly requested by the repo owner.

Integration points & external dependencies
-----------------------------------------
- No server-side or external build integrations found.
- External fonts are loaded from Google Fonts in `index.html` (example: Anton family). Keep external references minimal and explicit.

Examples of actionable prompts for this repo
-------------------------------------------
- "Add a responsive `about.html` page matching the `index.html` header/footer and using the existing `.about-preview` styles." 
- "Optimize images in `images/` for web — compress `hero.png` and ensure `images/logo.png` remains at the same path and filename." 
- "Fix stylesheet link so site works when previewed with `python3 -m http.server`: change `href="/styles.css"` to `href="styles.css"` and verify in browser." 

When merging or updating this file
---------------------------------
- If `.github/copilot-instructions.md` already exists, preserve any human-authored guidance and only add or refine details that are discoverable from the repository (e.g., exact filenames, examples from `index.html`).

Contact / next steps
--------------------
- After making changes, run the quick local preview and report any unresolved asset/path issues.
- Ask the repo owner if they want a basic preview script (`package.json` + `serve`) added — do not add without explicit approval.

End of instructions
