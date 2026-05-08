# wod-wiki-preview

GitHub Pages deployment project for the wod-wiki playground.

## What this repo does

- Builds the wod-wiki playground from a selected source branch
- Deploys the playground bundle to GitHub Pages
- Supports manual branch selection
- Supports automatic dispatch from the wod-wiki repo on pushes to `dev`

## Triggers

### Manual
Run the workflow in this repo and choose a branch:
```bash
gh workflow run preview.yml -f branch=feature/my-branch
```

### Automatic from wod-wiki
The wod-wiki repo dispatches this repository on pushes to `dev`.
The dispatch payload includes the source branch name.

## Pages base path

This repo publishes a GitHub Pages project site, so the playground must be built with:
- `/wod-wiki-preview/`

That base path is injected by the workflow before building the playground.

## Deployment target

The published site is the playground app, not Storybook.

GitHub Pages URL:
- `https://sergeigolos.github.io/wod-wiki-preview/`
- `https://wod.wiki/` is the source project; this repo is only the preview host

## Source build details

The workflow clones:
- `https://github.com/SergeiGolos/wod-wiki.git`

Then it runs the playground build command from that repo:
- `bun run build:app`

## Requirements

To enable automatic dispatch from the source repo, add a repository secret in `wod-wiki`:
- `PREVIEW_REPO_PAT` with permission to trigger repository dispatch events on `wod-wiki-preview`
