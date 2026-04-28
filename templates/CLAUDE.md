# CLAUDE.md — {{VAULT_NAME}} Obsidian Vault

This file tells Claude Code how to work in this vault. Drop it in your vault root so every Claude session picks up these conventions automatically.

---

## Vault overview

**Vault name:** {{VAULT_NAME}}
**Vault root:** `~/{{VAULT_PATH}}/`
**Git-synced:** yes — commit often; use `git status` before and after changes

### Folder structure

```
{{VAULT_NAME}}/
├── Daily/              # Daily notes, one file per day
├── Projects/           # Project-specific notes and specs
├── Content/            # Writing, drafts, social content
├── Templates/          # Note templates (Obsidian template plugin)
├── Attachments/        # Images, PDFs, audio embeds ({{ATTACHMENTS_FOLDER}})
├── Categories/         # MOC (map of content) index notes
├── References/         # Clippings, reading notes, external sources
└── 00 Inbox/           # Unprocessed captures and quick notes
```

Adjust these to match your actual folders.

---

## File naming conventions

| Note type     | Pattern                          | Example                        |
|---------------|----------------------------------|--------------------------------|
| Daily note    | `{{DAILY_NOTE_PATTERN}}`         | `2026-04-28.md`                |
| Meeting note  | `YYYY-MM-DD HHmm Title.md`       | `2026-04-28 0900 Sync.md`      |
| Project note  | `Project Name - Subtopic.md`     | `Onyx - V1 Spec.md`            |
| MOC           | `Topic MOC.md`                   | `Research MOC.md`              |
| Template      | `Topic Template.md`              | `Daily Note Template.md`       |

---

## Obsidian Markdown conventions

This vault uses **Obsidian Flavored Markdown**. Key differences from standard Markdown:

- **Wikilinks:** `[[Note Title]]` — do not convert to standard links
- **Embeds:** `![[filename]]` — embeds another note or file inline
- **Callouts:** `> [!note]`, `> [!warning]`, `> [!tip]`, etc.
- **Frontmatter:** YAML between `---` fences at the top of each file
- **Tags:** in frontmatter (`tags: [daily]`) or inline (`#project/active`)
- **Dataview:** some notes contain `dataview` code fences — preserve them as-is

**Never rewrite wikilinks to standard Markdown links.**
**Never reorder or reformat frontmatter unless explicitly asked.**

---

## Daily notes

Daily notes live in `Daily/` and follow the pattern `{{DAILY_NOTE_PATTERN}}`.

The template is at `Templates/Daily Note Template.md`. When creating a daily note:
1. Copy the template
2. Set `date:` in frontmatter to today's date
3. Place the file in `Daily/`

---

## Skills

When working in this vault, use the **obsidian-vault** skill. Install it by copying or symlinking `skills/obsidian-vault/` from the clausidian repo into `~/.claude/skills/`.

Related community skills that compose well:
- `obsidian-markdown` — broader Obsidian Markdown editing
- `obsidian-cli` — Obsidian URI protocol and CLI interactions
- `obsidian-bases` — `.base` database view files

---

## Git workflow

This vault is tracked in git. Suggested workflow:

```bash
# Before making changes
git status

# After Claude edits
git add -p          # review changes interactively
git commit -m "vault: <what changed>"

# Sync with remote
git pull --rebase
git push
```

Commit granularity: one commit per logical unit of work (one note created, one section refactored, one batch of daily notes).

---

## What Claude should NOT do

- Rewrite prose in notes unless asked
- Remove or alter wikilinks
- Add frontmatter keys not explicitly requested
- Create files outside the vault root
- Delete files without explicit confirmation
