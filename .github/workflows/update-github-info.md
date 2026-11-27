---
name: update-github-info
description: Keep GitHub Info current with practical updates from official GitHub sources.
intent: Keep Mona's GitHub Info website current with practical, source-backed GitHub guidance.
on:
  schedule: daily
  workflow_dispatch:
  skip-if-match: 'is:pr is:open "gh-aw-workflow-id: update-github-info" in:body'
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
  model: gpt-5-mini
tools:
  edit: 
  web-fetch: 
strict: false
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    reviewers: [mona]
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the existing `site/content/github-info.md` before making changes.
Fetch `https://github.blog/latest/`, `https://github.blog/changelog/`, and
`https://awesome-copilot.github.com/workflows/`. Use Awesome Copilot workflows as an
additional source alongside the GitHub Blog and Changelog.

Select only recent, useful updates that help developers learn GitHub faster. Keep the
content short and practical, preserve its existing structure, and cite the relevant
official source link for every new fact. Do not invent details or copy long passages.
Edit only `site/content/github-info.md`.

If neither source has a useful new update, or the file needs no changes, use `noop`
with a brief reason. Otherwise, use the configured `create-pull-request` safe output
to open a review-ready pull request requesting Mona's review. Summarize the changes
and link the sources in the pull request description. Never write directly to `main`.
