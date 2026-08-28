# shiftmask.com

Marketing site for **ShiftMask** — a desktop app that builds a safe local copy of Excel, CSV and SQL data (relations intact, dates shifted, values masked) so the data can be used with AI tools without exposing real records.

Static site, no build step. Hosted on GitHub Pages at `https://shiftmask.com`.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole site. All CSS is inline; only web fonts are external. |
| `CNAME` | Custom domain for GitHub Pages. Do not delete. |
| `favicon.svg`, `icon-180.png`, `icon-512.png` | Icons. |
| `og.png` | 1200×630 social card. |
| `robots.txt`, `sitemap.xml` | Crawling. Update `lastmod` when the page changes. |
| `.nojekyll` | Serves files as-is, skipping Jekyll processing. |
| `CLAUDE.md` | Project context for Claude Code — product, glossary, constraints, settled decisions. |
| `DESIGN-BRIEF.md` | Design brief, audit of the current page, and the redesign direction. Read before touching design. |
| `SETUP.md` | One-time deployment: repo, DNS, HTTPS, `.eu` redirect. |

## Before going live

Search `index.html` for `TODO` and replace four placeholders:

1. Download link (nav button and hero button)
2. Payment link for the Project Pass
3. Privacy policy URL
4. Contact URL

## Editing

Open `index.html` and edit. Commit to `main` and GitHub Pages redeploys in about a minute.

Design tokens (colours, type) live in the `:root` block at the top of the file and match the ShiftMask brand guide. Coral `#FF5F45` is for fills only — for coral **text** on a light background use `--coral-text` (`#C63A1F`), which meets WCAG AA.

## Licence

Content and branding © 2026 ShiftMask. Not open source.
