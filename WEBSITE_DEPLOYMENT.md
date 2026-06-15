# Website: Local Testing & GitHub Pages Deployment

> **This guide covers two things:** previewing the docs site on your machine, and publishing it to GitHub Pages as a standalone public repo (separate from the private Crucible codebase).

---

## Part 1: Test Locally

### Prerequisites

- Python 3.9+
- `pip` (comes with Python)

### Steps

```bash
# 1. Navigate to the website directory
cd website

# 2. Install MkDocs + Material theme (one-time)
pip install mkdocs-material

# 3. Start the local dev server
mkdocs serve
```

Open **http://127.0.0.1:8000** in your browser.

That's it. The dev server **auto-reloads** — edit any `.md` file in `website/docs/` and the browser updates instantly.

### Optional: Change Port

```bash
mkdocs serve -a 0.0.0.0:9000
```

### Optional: Build Static Site (Without Serving)

```bash
mkdocs build
# Output goes to website/site/
```

---

## Part 2: Deploy to GitHub Pages

### Step 1: Create a New Public Repository

Go to [github.com/new](https://github.com/new) and create a repo. Example name: `crucible-docs`.

Leave it **empty** (no README, no .gitignore, no license).

### Step 2: Initialize and Push

```bash
# From the Crucible project root
cd website

# Initialize a fresh git repo inside website/
git init
git remote add origin git@github.com:<your-username>/crucible-docs.git

# Add everything
git add .
git commit -m "Initial docs site"

# Push
git push -u origin main
```

### Step 3: Deploy with One Command

```bash
# Still inside website/
mkdocs gh-deploy
```

This command:
1. Builds the static site from `website/docs/` + `mkdocs.yml`
2. Creates (or updates) a `gh-pages` branch
3. Pushes that branch to your remote

### Step 4: Enable GitHub Pages (First Time Only)

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under **Source**, select: **Deploy from a branch**
3. Branch: `gh-pages` / `/ (root)`
4. Click **Save**

Your site will be live at:
```
https://<your-username>.github.io/crucible-docs/
```

Wait 1-2 minutes for the first deployment to propagate.

---

## Part 3: Updating the Site

Whenever you update documentation in the main Crucible repo:

```bash
# 1. From Crucible root, sync docs to website (preserving website-only files)
#    Copy changed files manually, or use:
xcopy /s /y docs\*.md website\docs\

# 2. Go to website directory
cd website

# 3. Test locally
mkdocs serve
# Check http://127.0.0.1:8000 — verify changes look good

# 4. Deploy
mkdocs gh-deploy

# 5. Commit the source changes too
git add .
git commit -m "Update docs"
git push
```

> **Important:** The `website/docs/` directory contains some **website-only files** (`index.md`, `TECHNICAL_OVERVIEW.md`, `FEATURE_GUIDE.md`, `DESIGN_DECISIONS.md`, and 4 extra case studies) that do NOT exist in the main `docs/` folder. When syncing, do not delete these files.

---

## Quick Reference

| Task | Command |
|---|---|
| Install MkDocs | `pip install mkdocs-material` |
| Preview locally | `mkdocs serve` |
| Build static site | `mkdocs build` |
| Deploy to GitHub Pages | `mkdocs gh-deploy` |
| Check deployed site | `https://<user>.github.io/<repo>/` |

---

## Troubleshooting

| Issue | Fix |
|---|---|
| `mkdocs: command not found` | Run `pip install mkdocs-material` again, or use `python -m mkdocs serve` |
| Mermaid diagrams show as code | Already fixed in `mkdocs.yml` — ensure `pymdownx.superfences` has the `custom_fences` config |
| 404 on GitHub Pages | Check Settings → Pages → Source is set to `gh-pages` branch |
| Changes not appearing | Clear browser cache, or wait 2-3 minutes for GitHub CDN propagation |
| `git push` rejected | Ensure you pushed to the correct remote (`git remote -v` to check) |
