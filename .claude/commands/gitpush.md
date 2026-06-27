Follow these steps in order. Complete each step fully before moving to the next.

## Step 1 — Security scan

Before touching git, scan the working directory for sensitive data. Check every tracked and untracked file for:
- API keys, tokens, secrets (patterns like `sk-`, `ghp_`, `Bearer `, `Authorization:`, `api_key`, `apiKey`, `secret`, `password`, `passwd`, `private_key`)
- `.env` files or files named `*.env`, `*.pem`, `*.key`, `*.p12`, `*.pfx`
- Hardcoded credentials, connection strings, or database URLs
- AWS/GCP/Azure credentials or config files

Use Grep to search the project files. If ANY sensitive data is found:
- Stop immediately and report exactly which file and line contains the issue.
- Do NOT proceed with the push until the user has resolved it.

If the scan is clean, report "Security scan passed — no sensitive data detected." and continue.

## Step 2 — Ensure git is initialised and remote is configured

Check whether a git repo exists (`git status`). If not, run `git init`.

Check whether a remote named `origin` exists (`git remote -v`). If not, ask the user for the GitHub repository URL before proceeding.

## Step 3 — Stage and push all code

1. Stage everything: `git add -A`
2. Check `git status` — if there is nothing to commit, skip the commit and note that the repo is already up to date.
3. If there are changes, ask the user for a commit message or auto-generate a concise one that describes what changed (look at the diff to decide).
4. Commit and push: `git commit -m "<message>" && git push -u origin main`

## Step 4 — Create or update the README

Read the current `README.md` (if it exists). Decide whether it needs to be created or meaningfully improved based on the current state of the project.

A good README must include:
- Project name and one-line description
- Live site URL (if GitHub Pages is set up — use `https://<owner>.github.io/<repo>/`)
- Features list (derive from the actual code)
- How to run locally
- Deployment section referencing the GitHub Actions workflow (if present)

Write the README using the Bash `cat >` heredoc approach (not the Write tool) to guarantee clean UTF-8 encoding with no BOM. Then stage and push: `git add README.md && git commit -m "Update README" && git push`

Skip this commit if README content did not change.

## Step 5 — Create the GitHub Actions Pages workflow

Check whether `.github/workflows/deploy.yml` already exists.

If it does not exist, create it with this exact content:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deploy.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v5

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: .

      - name: Deploy to GitHub Pages
        id: deploy
        uses: actions/deploy-pages@v4
```

Then commit and push: `git add .github/workflows/deploy.yml && git commit -m "Add GitHub Actions Pages deployment" && git push`

If the file already exists, skip this step.

After pushing, remind the user to complete the one-time manual step in GitHub:
> Go to **github.com/<owner>/<repo>/settings/pages** → set Source to **GitHub Actions** → Save.

## Step 6 — Update repo About (description + website)

Determine the repo owner and name from `git remote get-url origin`.

Try to update the repo metadata using the `gh` CLI:
```
gh repo edit --description "<short description>" --homepage "https://<owner>.github.io/<repo>/"
```

If `gh` is not installed or not authenticated, instruct the user to do it manually:
> On **github.com/<owner>/<repo>**, click the ⚙ gear icon next to "About" and set:
> - Description: `<short description derived from the project>`
> - Website: `https://<owner>.github.io/<repo>/`

## Step 7 — Final report

Print a summary of every action taken:
- Security scan result
- Files committed (or "nothing to commit")
- README status (created / updated / unchanged)
- Workflow status (created / already existed)
- Repo About status (updated via gh / manual step required)
- Live site URL
