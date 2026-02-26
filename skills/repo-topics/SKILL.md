---
name: repo-topics
description: Suggest and set GitHub repository topics based on what the project actually is. Reads the repo to understand it, proposes topics, then applies them with gh. Use when the user mentions GitHub topics, tagging a repo, discoverability, improving how a project appears in GitHub search, or setting up a new repo's metadata.
---

You help set GitHub repository topics for the current repo. Topics should be discoverable, accurate, and useful for people browsing GitHub — they're how someone finds your project when searching, so every topic should be something a real person would type into GitHub search.

## Step 1: Understand the repo

Read the README, package.json or go.mod, and any other top-level files that reveal what this project is — its language, framework, domain, and purpose. Don't read deeply into source code unless the top-level files are missing or unclear.

If the repo belongs to an org, glance at sibling repos' topics (via `gh repo list <org> --json name,repositoryTopics --limit 10`) to see if there are org-wide conventions worth following.

## Step 2: Check current topics

Run:

```bash
gh repo view --json repositoryTopics,description
```

Note what's already set so you don't duplicate or lose anything intentional. Existing topics were chosen for a reason — keep them unless they're clearly wrong or redundant.

## Step 3: Propose topics

Suggest 4-8 topics. Good topics are:

- **Language/framework**: `go`, `react`, `typescript`, `bubbletea`, `tailwind`
- **Domain**: `audio`, `music-production`, `developer-tools`
- **Type of thing**: `cli`, `tui`, `component-library`, `web-audio`
- **Ecosystem**: `claude-code`, `partykit`

Bad topics are generic filler that nobody searches for: `awesome`, `open-source`, `tool`, `app`, `best`, `fast`, `simple`. Don't add those.

Order matters — GitHub displays topics in the order they're added. Put the most important and discoverable ones first (usually domain and type, then language/framework).

When presenting to the user, also briefly mention topics you considered but rejected and why — this helps them make better decisions about what to keep.

Present the proposed topics to the user and wait for approval. They may want to add, drop, or change some.

## Step 4: Apply

Once approved, set them:

```bash
gh repo edit --add-topic topic1,topic2,topic3
```

If there were existing topics that should be removed, use:

```bash
gh repo edit --remove-topic old-topic
```

Confirm the final state by running `gh repo view --json repositoryTopics` and showing the result.

## Troubleshooting

If `gh` commands fail, check that the GitHub CLI is installed and authenticated (`gh auth status`). If it's not available, show the user what topics you'd recommend and give them the commands to run manually.
