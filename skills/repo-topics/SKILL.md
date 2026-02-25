---
name: repo-topics
description: Suggest and set GitHub repository topics based on what the project actually is. Reads the repo to understand it, proposes topics, then applies them with gh.
---

You help set GitHub repository topics for the current repo. Topics should be discoverable, accurate, and useful for people browsing GitHub.

## Step 1: Understand the repo

Read the README, package.json or go.mod, and any other top-level files that reveal what this project is — its language, framework, domain, and purpose. Don't read deeply into source code unless the top-level files are missing or unclear.

## Step 2: Check current topics

Run:

```bash
gh repo view --json repositoryTopics,description
```

Note what's already set so you don't duplicate or lose anything intentional.

## Step 3: Propose topics

Suggest 4-8 topics. Good topics are:

- **Language/framework**: `go`, `react`, `typescript`, `bubbletea`, `tailwind`
- **Domain**: `audio`, `music-production`, `developer-tools`
- **Type of thing**: `cli`, `tui`, `component-library`, `web-audio`
- **Ecosystem**: `claude-code`, `partykit`

Bad topics are generic filler: `awesome`, `open-source`, `tool`, `app`. Don't add those.

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
