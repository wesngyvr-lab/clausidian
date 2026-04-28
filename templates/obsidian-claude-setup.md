---
tags:
  - meta
  - setup
created: {{date}}
---

# Claude Code + Obsidian Setup

This note documents how Claude Code is configured for this vault. Keep it in your vault root or `Resources/` folder as a reference.

## What's installed

- **CLAUDE.md** — in vault root; Claude Code reads this automatically at session start
- **obsidian-vault skill** — at `~/.claude/skills/obsidian-vault/SKILL.md`; activates when Claude detects vault context

## How it works

When you open a Claude Code session with your vault as the working directory, Claude:
1. Reads `CLAUDE.md` to learn your folder structure, file-naming conventions, and Obsidian syntax rules
2. Loads the `obsidian-vault` skill when you ask it to work with notes
3. Preserves wikilinks, embeds, callouts, and frontmatter without mangling them

## Common commands to try

```
# Create today's daily note
"Create today's daily note using my template"

# Write a new project MOC
"Create a new MOC for [[Project Name]] in the Projects folder"

# Refactor tags
"Find all notes tagged #inbox and suggest which permanent tags to apply"

# Summarize recent notes
"Summarize my daily notes from this week"

# Clean up a note
"Tidy up the structure of [[Note Title]] without changing the content"
```

## Related skills

- [[obsidian-markdown]] — if installed; handles broader Markdown editing conventions
- [[obsidian-cli]] — if installed; Obsidian URI protocol and CLI interactions
- [[obsidian-bases]] — if installed; `.base` database view files

## Source

Installed from the [clausidian](https://github.com/wesngyvr-lab/clausidian) starter kit.
