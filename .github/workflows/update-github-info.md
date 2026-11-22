---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
tools:
  edit:
  web-fetch:
  bash: ["curl:*"]
  github:
    mode: gh-proxy
    toolsets: [repos]
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
---

# Update Mona's GitHub Info website

You keep Mona's GitHub Info website current with practical, source-backed GitHub updates.

## Sources

- Mona's notes: `notes/mona-notes.md`
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/
- Awesome Copilot workflows: https://awesome-copilot.github.com/workflows/

## How to read sources

- Read repository files such as `notes/mona-notes.md` and `site/content/github-info.md` with the GitHub repository API tools. Do not use terminal, CLI, or sandboxed shell commands to read repository guidance or reference files.
- Read external public pages (the GitHub Blog, the GitHub Changelog, and Awesome Copilot workflows) with the `web-fetch` tool.
- If the `web-fetch` tool is not available in your tool list, fetch those same public pages with `curl -sL <url>` in bash instead. Only use `curl` for the source URLs listed above; the firewall only allows github.com, github.blog, and awesome-copilot.github.com.

## Steps

1. Read `notes/mona-notes.md` before making changes and follow Mona's editorial guidance.
2. Read the current `site/content/github-info.md` to understand the existing content and structure.
3. Web fetch https://github.blog/latest/ and pick recent GitHub Blog stories that help developers learn GitHub faster.
4. Web fetch https://github.blog/changelog/ and pick recent GitHub Changelog entries worth highlighting.
5. Web fetch https://awesome-copilot.github.com/workflows/ and pick Awesome Copilot workflows that would help readers automate their repositories.
6. Update `site/content/github-info.md` with concise, practical updates for readers. Keep the existing sections, keep summaries short, and mention the source (GitHub Blog, GitHub Changelog, or Awesome Copilot, with a link) for every item you add.
7. Only edit `site/content/github-info.md`. Do not change any other file.

## Pull request for Mona to review

Open a pull request for Mona to review with your changes to `site/content/github-info.md`.
Use a pull request title that mentions Mona or GitHub Info, and summarize which GitHub Blog, GitHub Changelog, and Awesome Copilot items you added in the pull request body.
Do not write directly to `main`; rely on `safe-outputs` with `create-pull-request` so Mona can review everything before it goes live.

If nothing new and relevant is found, make no changes and do not open a pull request.
