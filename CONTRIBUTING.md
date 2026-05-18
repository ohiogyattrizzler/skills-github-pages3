# Contributing — Update Workflow

This repo uses a **staging branch** system to batch updates before publishing to the live GitHub Pages site.

## Branches

- **`main`** — The live site. Deployed automatically to GitHub Pages.
- **`staging`** — Queued updates. Changes here do NOT go live until published.

## Live Site

**https://ohiogyattrizzler.github.io/skills-github-pages3/**

---

## AI Session Instructions

**Read this entire section before doing anything.** This is the exact workflow you must follow for every task.

### Step 1: Make Changes on `staging`

1. Clone the repo and check out the `staging` branch: `git checkout staging`
2. Make the requested code changes to `index.html` (the entire app is in this single file).
3. Commit your changes to the `staging` branch.
4. Push to `origin staging`: `git push origin staging`
5. Do NOT push to `main`. Ever. All changes go through `staging`.

### Step 2: Deploy a Preview Site

After pushing to staging, **always** deploy a preview so the user can test before publishing:

1. Copy the deployable files (`index.html`, `favicon.jpg`) to a temporary directory.
2. Use the `deploy` tool with `command="frontend"` and the temp directory to deploy a preview.
3. Share the preview URL with the user so they can review and test the changes.

Example:
```
mkdir -p /tmp/deploy-preview
cp index.html favicon.jpg /tmp/deploy-preview/
# Then use the deploy tool: command="frontend", dir="/tmp/deploy-preview"
```

### Step 3: Wait for User Feedback

- The user will test on the preview site.
- If they request more changes, go back to Step 1.
- If they say **"publish"**, proceed to Step 4.

### Step 4: Publish (only when user says "publish")

When the user says "publish", merge staging into main and deploy to GitHub Pages:

1. Check out `main`: `git checkout main`
2. Merge staging: `git merge staging`
3. Push to main: `git push origin main`
4. After push, GitHub Pages will automatically deploy from `main`.
5. Reset staging to match main: `git checkout staging && git reset --hard main && git push origin staging --force-with-lease`
6. Confirm to the user that the live site is updated: https://ohiogyattrizzler.github.io/skills-github-pages3/

### Commands Reference

| User says | What to do |
|-----------|-----------|
| *(describes changes)* | Make changes on `staging`, push, deploy preview site, share URL |
| **"review update"** or **"preview"** | Deploy the current staging branch to a preview site and share the URL |
| **"publish"** | Merge `staging` → `main`, push, confirm live site is updated |

### Important Rules

- **NEVER push directly to `main`** — all changes go through `staging` first.
- **ALWAYS deploy a preview** after making changes, before the user says "publish".
- **ALWAYS share the preview URL** with the user after deploying.
- The app is a single `index.html` file — all code (HTML, CSS, JS) lives there.
- The draft PR (`staging → main`) on GitHub shows all queued changes.
- There is also a `favicon.jpg` that should be included in any deployment.

## Auto-Merge Behavior (GitHub Actions)

- **Draft PRs** are skipped by auto-merge — they accumulate changes.
- **Non-draft PRs** targeting `staging` are auto-merged immediately.
- When a `staging → main` draft PR is marked "Ready for review", it auto-merges and deploys.
- After merge, the `staging` branch is reset to match `main` for the next batch.
