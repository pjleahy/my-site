# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static personal site for Pat Leahy deployed at `https://pjleahy.github.io/` via GitHub Pages (the repo is named `pjleahy.github.io`, so it serves from the domain root with no path prefix). Home lives at `/` (`index.html`) and resume lives at `/resume/` (`resume/index.html`) — the folder-index pattern is what gives the clean `.html`-free URL. Shared stylesheet is `css/style.css`. No build system, no dependencies, no tests.

## Local preview

Must serve the directory (don't open files directly) — all links/assets use absolute paths (`/css/...`, `/images/...`, `/resume/`) that only resolve correctly behind a server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Structure conventions

- **Absolute paths** — every internal href and asset src starts with `/` (e.g. `/css/style.css`, `/images/sunset.JPG`, `/resume/`). Don't use relative paths; they break differently depending on which page references them.
- **Two-page navigation** — both pages render the same `<header><nav>` with `/` and `/resume/` links. The current page's nav link must carry `class="active"` so the bold-underline style applies. To add a new page, create `newpage/index.html` (so its URL is `/newpage/`) and update the nav on every page.
- **Shared stylesheet** — all styling lives in `css/style.css`. The palette is just two CSS custom properties on `:root`: `--ink` (#262a28, obsidian dark green) for all text/borders and `--paper` (#faf8f3, cream) for all backgrounds. Use these variables rather than hard-coded colours.
- **Entry styling is deliberately minimal** — `.job-entry`, `.education-entry`, and `.voluntary-entry` share a single rule: a 2px `--ink` left border, no background fill, no accent colours. Don't reintroduce per-category accent colours. `.summary-text` and `.contact-details` are plain blocks with no border or background.
- **Resume entries** use the `article.<type>-entry > img.entry-logo + div.entry-content` shape, with `h3`, `p.dates`, `span.role`, then a description `<p>` inside `entry-content`. Logos live in `images/` and are referenced directly.
- **Footer year** is hand-maintained in each HTML file — keep them in sync when editing.
