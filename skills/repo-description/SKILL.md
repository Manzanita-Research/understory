---
name: repo-description
description: Suggest and set a GitHub repository description based on what the project actually is. Reads the repo to understand it, proposes a one-liner, then applies it with gh. Use when the user mentions setting a repo tagline, updating the GitHub one-liner, improving how a project looks in search results, or setting up a new repo's metadata.
---

You help set the GitHub repository description for the current repo. The description appears on the repo page and in search results — it should be short, clear, and tell someone what this thing is in one line.

## Step 1: Understand the repo

Read the README, PITCH.md, and any top-level files that reveal what this project does, who it's for, and what makes it distinct. Pay attention to taglines, opening lines, and any language the author already chose to describe the project — there may be a voice worth drawing from. Don't read deeply into source code.

## Step 2: Check current description

Run:

```bash
gh repo view --json description,homepageUrl
```

Note what's already set. It might be fine, empty, or stale. If the repo has a docs site or landing page and the homepage URL isn't set, mention it to the user as a bonus fix.

## Step 3: Propose a description

Write one line. Start with a single emoji that captures the project's spirit, followed by the description. Aim for under 100 characters (after the emoji), but don't sacrifice clarity to hit a number — GitHub allows up to 350.

Good descriptions:

- Say what the thing **does**, not what it **is** ("Spatial audio mixer in 3D" not "A web application")
- Use plain language, no marketing ("Semantic EQ for guitarists" not "Revolutionary AI-powered tone solution")
- Skip words like "A tool that..." or "An app for..." — just say the thing
- Draw from the project's own voice when it has one. If the README has a good tagline or poetic opener, let that inform the tone. A description can have personality — it doesn't have to read like a database entry.

**Example 1:**
README says: "The connective tissue between your projects."
Good: `🌿 The connective tissue between your projects — shared Claude Code skills via symlinks`
Bad: `A CLI tool for managing shared configuration files`

**Example 2:**
README says: "Semantic EQ — speak your tone into being."
Good: `🎸 Semantic EQ — speak your tone into being`
Bad: `An audio equalization tool using semantic descriptors`

Present the proposed description to the user and wait for approval. They may want to tweak the wording.

## Step 4: Apply

Once approved:

```bash
gh repo edit --description "the approved description"
```

Confirm by running `gh repo view --json description` and showing the result.

## Troubleshooting

If `gh` commands fail, check that the GitHub CLI is installed and authenticated (`gh auth status`). If it's not available, show the user what you'd recommend and give them the commands to run manually.
