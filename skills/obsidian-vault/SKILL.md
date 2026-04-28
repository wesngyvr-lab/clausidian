---
name: obsidian-vault
description: Use when the user asks Claude to read, write, edit, or navigate notes inside an Obsidian vault — including creating daily notes, project MOCs, templates, wikilinks, callouts, or any file within a directory that contains a `.obsidian/` folder. Also activates when the user references Obsidian-specific syntax such as `[[wikilinks]]`, `![[embeds]]`, dataview queries, or frontmatter tags in a vault context.
---

# Obsidian Vault Skill

## Detecting a vault

An Obsidian vault is any directory containing a `.obsidian/` subdirectory. Before editing notes, verify you are operating inside a vault root. If the path is ambiguous, ask the user to confirm the vault location or look for `.obsidian/app.json`.

## How Obsidian Flavored Markdown differs from standard Markdown

### Wikilinks
Internal links use double brackets: `[[Note Title]]`. The display text can be piped: `[[Note Title|display text]]`. Wikilinks are case-sensitive and must match the exact filename (without the `.md` extension).

```
[[Daily Notes List]]
[[Projects/Onyx|Onyx project]]
```

**Do not convert wikilinks to standard Markdown links** (`[text](path.md)`) unless the user explicitly asks. Obsidian resolves wikilinks relative to the vault root; standard links break portability.

### File embeds
Embed the content of another note or attachment with `![[filename]]`. This works for Markdown files, images, PDFs, and audio.

```
![[Daily.base]]
![[Attachments/screenshot.png]]
```

### Callouts
Obsidian callouts are blockquotes with a type tag on the first line:

```markdown
> [!note]
> This is a note callout.

> [!warning] Custom title
> Warning content here.

> [!tip]+ Foldable callout (open by default)
> Content.

> [!todo]- Foldable callout (closed by default)
> Content.
```

Common types: `note`, `tip`, `warning`, `danger`, `info`, `success`, `question`, `todo`, `abstract`, `example`, `quote`.

### Frontmatter
YAML frontmatter sits between `---` fences at the top of the file:

```yaml
---
tags:
  - daily
  - project
date: 2026-04-28
aliases: [My Note, Alt Title]
---
```

- `tags` can be a list or inline: `tags: [daily, project]`
- `aliases` lets Obsidian find the note by alternate names
- Custom properties are valid and used by Dataview and Bases

**Do not rewrite or reorder existing frontmatter** unless the user explicitly asks. Only add or modify the specific keys requested.

### Tags
Tags appear in frontmatter (`tags: [daily]`) or inline in note body (`#daily`). Nested tags use slashes: `#project/active`.

### Dataview queries
Dataview is a community plugin that lets notes embed live queries:

````markdown
```dataview
TABLE date, tags FROM "Daily"
WHERE date >= date(today) - dur(7 days)
SORT date DESC
```
````

When writing or editing dataview blocks, preserve the exact code fence syntax. Do not convert them to static lists.

### Block references and heading links
Link to a specific heading: `[[Note Title#Heading]]`
Link to a specific block: `[[Note Title#^block-id]]`

### Obsidian Bases
`.base` files are Obsidian's native database views. They are referenced via embeds (`![[MyBase.base]]`). Do not edit `.base` files as plain text — use the `obsidian-bases` skill.

## Tone and editing conventions

- **Preserve the user's voice.** These are personal notes. Do not rephrase sentences, restructure paragraphs, or "clean up" prose unless asked.
- **Preserve all wikilinks.** Never silently remove or alter `[[wikilinks]]`.
- **Preserve frontmatter.** Add keys surgically; never rewrite the entire block.
- **File naming.** Follow the vault's existing naming convention. Common patterns: `YYYY-MM-DD Title.md` for dated notes, `Topic - Subtopic.md` for reference notes. Match what already exists.
- **Templates.** If the vault has a `Templates/` folder, check it for relevant templates before creating new notes from scratch.

## Composing with other skills

- `obsidian-markdown` — broader Obsidian Markdown editing guidance
- `obsidian-cli` — interact with the vault via the Obsidian URI protocol or `obsidian-cli` tool
- `obsidian-bases` — create and edit `.base` database view files

Use these skills when the task goes beyond reading and writing plain Markdown.
