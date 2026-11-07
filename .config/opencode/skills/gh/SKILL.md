---
name: GitHub CLI (gh)
description: Use when working with GitHub repositories, pull requests, issues, releases, or GitHub Actions workflows via the `gh` CLI.
---

# GitHub CLI (`gh`)

Use the `gh` CLI for GitHub operations instead of scraping web pages or guessing API URLs.

## Pull Requests
- List open PRs: `gh pr list`
- View PR details & comments: `gh pr view <number> --comments`
- View PR diff: `gh pr diff <number>`
- Check CI status on a PR: `gh pr checks <number>`
- Checkout a PR locally: `gh pr checkout <number>`
- Create a PR (non-interactive):
  ```bash
  gh pr create --title "Title" --body "Description" --base main
  ```

## Issues
- List issues: `gh issue list`
- View issue details: `gh issue view <number> --comments`
- Create an issue:
  ```bash
  gh issue create --title "Title" --body "Description"
  ```

## Actions & CI Runs
- List recent workflow runs: `gh run list --limit 10`
- View a specific run and failed steps: `gh run view <run-id>`
- View logs only for failed steps: `gh run view <run-id> --log-failed`

## Custom API Queries
- For endpoints not covered by subcommands, use `gh api`:
  ```bash
  gh api repos/{owner}/{repo}/pulls/<number>/comments --jq '.[] | {path: .path, body: .body}'
  ```

## Best Practices
- Always pass explicit flags (`--title`, `--body`, `--yes`) rather than relying on interactive prompts.
- Prefer `--json <fields> --jq <expr>` when parsing output programmatically.
