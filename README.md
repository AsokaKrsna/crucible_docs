# Crucible Documentation Website

This directory contains the source for the Crucible documentation website, built with [MkDocs](https://www.mkdocs.org/) and the [Material theme](https://squidfunk.github.io/mkdocs-material/).

## Quick Start

```bash
# Install MkDocs + Material theme
pip install mkdocs-material

# Build the site
mkdocs build

# Preview locally
mkdocs serve
# Open http://127.0.0.1:8000

# Deploy to GitHub Pages (if using a public repo)
mkdocs gh-deploy
```

## Deploying

1. Create a public GitHub repository for the website
2. Copy this `website/` directory into it (or the repo root)
3. Run `mkdocs gh-deploy` from the repo root
4. GitHub Pages will serve from the `gh-pages` branch at `https://<user>.github.io/<repo>/`

## Notes

- Most docs in `website/docs/` are copies from the main Crucible repo's `docs/` directory
- **New original docs** that only exist in `website/docs/` (not in the main repo):
  - `TECHNICAL_OVERVIEW.md` — System philosophy, architecture, design principles
  - `DESIGN_DECISIONS.md` — 15 key architectural decisions with rationale and tradeoffs
  - `PLUGIN_DEVELOPMENT.md` — Comprehensive plugin authoring guide
  - `FEATURE_GUIDE.md` — What each feature is, why it matters, how to use it
- `site/` is the build output — it is gitignored
- The main Crucible repo is private; only this website is public
