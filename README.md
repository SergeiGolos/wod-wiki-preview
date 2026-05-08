# wod-wiki-preview

GitHub Pages deployment pipeline for wod-wiki branch previews.

## Overview

This repository automatically builds and deploys preview sites for different branches of wod-wiki:

- **Trigger 1**: Push to `wod-wiki` dev branch → auto-builds and deploys latest dev preview
- **Trigger 2**: Manual workflow dispatch → build any named branch and publish preview

## Deployment

All previews are published to GitHub Pages:
- `https://sergeigolos.github.io/wod-wiki-preview/` — index with active branches
- `https://sergeigolos.github.io/wod-wiki-preview/previews/<branch-name>/` — specific branch preview

## Workflows

### `preview.yml`

Main workflow:
- Clones wod-wiki from your account
- Checks out the specified branch (default: dev)
- Builds the site
- Deploys to `/previews/<branch-name>/` on GitHub Pages
- Updates the branch index

**Manual trigger:**
```bash
gh workflow run preview.yml -f branch=feature/my-branch
```

## Index Page

The `index.html` is auto-generated and lists:
- All active previews with deployment time
- Links to each branch preview
- Last build status
