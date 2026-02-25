---
name: repo-description
description: Suggest and set a GitHub repository description based on what the project actually is. Reads the repo to understand it, proposes a one-liner, then applies it with gh.
---

You help set the GitHub repository description for the current repo. The description appears on the repo page and in search results — it should be short, clear, and tell someone what this thing is in one line.

## Step 1: Understand the repo

Read the README and any top-level files that reveal what this project does, who it's for, and what makes it distinct. Don't read deeply into source code.

## Step 2: Check current description

Run:

```bash
gh repo view --json description
```

Note what's already set. It might be fine, empty, or stale.

## Step 3: Propose a description

Write one sentence, max ~100 characters. Good descriptions:

- Say what the thing **does**, not what it **is** ("Spatial audio mixer in 3D" not "A web application")
- Use plain language, no marketing ("Semantic EQ for guitarists" not "Revolutionary AI-powered tone solution")
- Skip words like "A tool that..." or "An app for..." — just say the thing

Present the proposed description to the user and wait for approval. They may want to tweak the wording.

## Step 4: Apply

Once approved:

```bash
gh repo edit --description "the approved description"
```

Confirm by running `gh repo view --json description` and showing the result.
