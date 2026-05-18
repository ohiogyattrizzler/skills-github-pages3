# Contributing — Update Workflow

This repo uses a **staging branch** system to batch updates before publishing to the live GitHub Pages site.

## Branches

- **`main`** — The live site. Deployed automatically to GitHub Pages.
- **`staging`** — Queued updates. Changes here do NOT go live until published.

## How to Make Changes

1. **Push changes to the `staging` branch** (or create a PR targeting `staging`).
2. All queued changes are visible in the open draft PR: `staging → main`.
3. When ready to publish, tell the session owner to say **"publish"** — this merges staging into main and deploys to the live site.

## Commands (for Devin sessions)

| Command | What it does |
|---------|-------------|
| *(describe changes)* | Devin makes changes on the `staging` branch |
| **"review update"** | Devin deploys a temporary preview site for review |
| **"publish"** | Devin merges `staging` → `main`, deploying to the live GitHub Pages site |

## Auto-Merge Behavior

- **Draft PRs** are skipped by auto-merge — they accumulate changes.
- **Non-draft PRs** targeting `staging` are auto-merged immediately.
- When a `staging → main` draft PR is marked "Ready for review", it auto-merges and deploys.
- After merge, the `staging` branch is reset to match `main` for the next batch.

## Live Site

**https://ohiogyattrizzler.github.io/skills-github-pages3/**

## Important

- Do NOT push directly to `main`. All changes go through `staging`.
- The draft PR on GitHub shows all queued changes and their descriptions.
