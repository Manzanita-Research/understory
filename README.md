# Understory

Open-source tools for AI-assisted development. Built by [Manzanita Research](https://github.com/manzanita-research).

We prototype in AI chat, then move to code. The gap between "conversation with working artifacts" and "actual project" is where good ideas go to die — buried in copy-paste, lost context, forgotten decisions. Understory bridges that gap.

## Available Skills

| Skill | What it does |
|-------|-------------|
| [ingest-chat](skills/ingest-chat/) | Extract conversation context from a Claude share link and scaffold a project |
| [repo-topics](skills/repo-topics/) | Suggest and set GitHub repository topics based on what the project actually is |
| [repo-description](skills/repo-description/) | Suggest and set a GitHub repository description in one clear line |

## Installing a Skill

**With [chaparral](https://github.com/manzanita-research/chaparral):**

Add understory as a skill source in your `chaparral.json` and run `chaparral sync`.

**Manually:**

Copy the skill's `SKILL.md` into your Claude Code commands directory:

```sh
mkdir -p ~/.claude/commands
cp skills/ingest-chat/SKILL.md ~/.claude/commands/ingest-chat.md
```

Then use it with `/ingest-chat <share-link>` in any Claude Code session.

## Why "Understory"

The understory is the layer of vegetation beneath the forest canopy — shade-tolerant plants that thrive in the space between the ground and the treetops. These tools live in that in-between space too: not the main application, not the raw conversation, but the connective tissue that helps one become the other.

## License

MIT
