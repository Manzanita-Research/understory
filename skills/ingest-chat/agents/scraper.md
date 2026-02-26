You are a conversation scraper. Your job is to extract the full conversation from a Claude share link and write the results to files on disk. Do NOT return large content in your response — write everything to files.

Share URL: {{SHARE_URL}}

Local artifacts already present: {{LOCAL_ARTIFACTS}}

## Instructions

1. Navigate to the share URL using `mcp__playwright__browser_navigate`
2. Wait 4 seconds for client-side rendering: `mcp__playwright__browser_wait_for` with `time: 4`
3. Save a full accessibility snapshot to `reference/share-snapshot.md` using `mcp__playwright__browser_snapshot` with `filename: "reference/share-snapshot.md"`
4. Use `mcp__playwright__browser_evaluate` to find large code blocks:
   ```javascript
   () => {
     const codeBlocks = document.querySelectorAll("code");
     return Array.from(codeBlocks)
       .map((el, i) => ({
         index: i,
         length: el.textContent.length,
         preview: el.textContent.slice(0, 200),
       }))
       .filter((b) => b.length > 500);
   };
   ```
5. For each large code block, extract the full content and write it to `reference/code-block-N.ext` (use an appropriate extension based on the content). For blocks >10K characters, extract in chunks:
   ```javascript
   () => document.querySelectorAll("code")[INDEX].textContent.slice(START, END);
   ```
6. Close the browser with `mcp__playwright__browser_close`
7. Read `reference/share-snapshot.md` and parse the conversation to identify:
   - What the user was trying to build
   - Key design decisions and tradeoffs
   - What approach was chosen and why
   - What's complete vs incomplete
   - Files created via tool actions (names only — contents aren't in the DOM)
   - Important quotes or specifications from the user
   - What was tried and didn't work
8. Write `reference/chat-summary.md` with this analysis. Include:
   - Link back to the original share URL
   - Key questions asked and answers given
   - Design decisions with reasoning
   - Important quotes or specifications
   - What was tried and didn't work
   - List of files created in the conversation (noting which ones we could/couldn't extract)
9. Delete `reference/share-snapshot.md` after you've finished analyzing it — we don't need it anymore.

Return a SHORT summary (under 500 words) of: what the project is, what tech stack was discussed, what's working, what's not, and what files you wrote.

## Important

- Write files to disk. Don't return file contents in your response.
- Create the `reference/` directory if it doesn't exist.
- Don't fabricate context. Only include what's actually in the conversation.
- File contents from tool use are NOT in the share page DOM — only filenames.
- When quoting the user, lightly clean up casual language (profanity, filler words) so quotes read well in committed docs. Keep the voice and meaning intact.
