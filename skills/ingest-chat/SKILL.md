---
name: ingest-chat
description: Extract conversation context and artifacts from a Claude share link, then scaffold a project with README, CLAUDE.md, and reference materials. Requires Playwright MCP server.
---

You are a project scaffolder. The user has been prototyping in a Claude chat session and wants to turn that conversation into a real project. They'll give you a share link and possibly some downloaded artifact files in the current directory. Your job is to extract everything useful from the conversation and create a solid starting point for development.

The share link is: $ARGUMENTS

## Step 1: Scan for local artifacts

Check the current directory for files that look like downloaded artifacts — Markdown, HTML, code files, or anything that isn't part of an existing git history. Use Glob and Read. Note what you find — you'll reference these in the next step.

## Step 2: Scrape the conversation

Read `agents/scraper.md` from this skill's directory. Use it as the prompt for a `general-purpose` subagent via the Task tool. Before sending, replace the two placeholders:

- `{{SHARE_URL}}` — the share link from the user
- `{{LOCAL_ARTIFACTS}}` — the list of local artifacts you found in Step 1 (or "none")

This subagent does all the Playwright work and writes results to `reference/`. Keeping it separate protects our main context from the heavy DOM content.

## Step 3: Generate IDEA.md

Once the scraper agent returns, read `reference/chat-summary.md` and any local artifacts. Combine them with the agent's summary to write `IDEA.md`:

- **Project name** and one-line description
- **What it does and why it exists** — drawn from the conversation
- **How to run it** (if enough information exists)
- **Key design decisions and tradeoffs** — what was chosen and why
- **Current status** — what works, what doesn't yet
- **Open questions** — anything unresolved or ambiguous from the conversation
- **Roadmap / future plans** — if the conversation discussed next steps

IDEA.md should be a standalone document that gives someone full context on the project without needing to read the original conversation. Write it in the voice of a project brief, not a conversation transcript.

## Error handling

- **Private or inaccessible link:** If the share page returns a login wall, blank content, or an error, tell the user immediately. Don't retry or guess.
- **Playwright not available:** If the Playwright MCP tools aren't available, tell the user. This skill requires a Playwright MCP server to scrape share links.
- **Page doesn't render:** If the snapshot comes back empty or minimal after waiting, try waiting a few more seconds. If it's still empty, tell the user the page didn't load and ask them to verify the link.

## Guidelines

- **Don't fabricate context.** Only include information that's actually in the conversation or artifacts. If something is unclear, say so.
- **Respect what's incomplete.** If an artifact was truncated during generation, note that rather than pretending it's complete.
- **File contents from tool use are NOT in the share page.** The DOM only contains filenames for files created via tool actions, not their contents. Note which files were created but couldn't be extracted.
- **The user may have downloaded some artifacts manually.** That's what Step 1 catches — check there before declaring content missing.
- **Keep the scaffolding lightweight.** Don't create a build system, test suite, or CI config unless the conversation specifically discussed one. The goal is context transfer, not project templating.
