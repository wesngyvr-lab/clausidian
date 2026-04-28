# Common Claude + Obsidian Workflows

Practical recipes for getting Claude Code to help with your vault. These assume you have `CLAUDE.md` in your vault root and the `obsidian-vault` skill installed.

---

## Writing a daily note

**Prompt:**
> "Create today's daily note using the template in Templates/Daily Note Template.md"

Claude will:
1. Read your template
2. Substitute today's date into frontmatter and the filename
3. Create the file in `Daily/` with the correct naming pattern
4. Leave placeholder sections for you to fill in

**Tip:** Keep your daily note template minimal. The more structure you bake in, the more friction you create on low-energy days.

---

## Creating a project MOC

A Map of Content (MOC) is an index note that links to all notes related to a topic. It replaces folder-based organization with a flat, wikilink-based graph.

**Prompt:**
> "Create a new MOC for my TileBuddy project. Link to the spec, PRD, meeting notes from April 2026, and any notes tagged #tilebuddy."

Claude will:
1. Search your vault for relevant files using the patterns you describe
2. Create a new MOC file in `Categories/` (or wherever your MOCs live)
3. Populate it with wikilinks to the found notes, grouped logically
4. Add frontmatter with a `moc` tag

**Review before saving:** Claude may miss notes it can't find by pattern. Always eyeball the wikilinks before committing.

---

## Refactoring tag taxonomy

Over time, tags accumulate inconsistencies: `#project`, `#projects`, `#project/active`, `#active-project` — all meaning roughly the same thing.

**Prompt:**
> "List all unique tags used across my vault and identify duplicates or near-duplicates. Suggest a clean, consistent tag hierarchy."

Then, once you've agreed on the new taxonomy:

> "Update all notes in Projects/ to replace #projects with #project/active and #project/done with #project/archived"

Claude will:
1. Scan frontmatter and inline tags across the target folder
2. Make the substitutions in each file
3. Report what changed

**Use `git diff` after** to review every change before committing.

---

## Summarizing a week of daily notes

**Prompt:**
> "Read my daily notes from April 21–27, 2026 and give me a bullet-point summary of recurring themes, decisions made, and open threads."

Claude will read each file and synthesize across them. Useful for weekly reviews.

---

## Extracting tasks from a note

**Prompt:**
> "Find all unchecked tasks (- [ ]) in my April 2026 daily notes and consolidate them into a single list, grouped by theme."

---

## Moving notes from Inbox to permanent locations

**Prompt:**
> "Look at the notes in 00 Inbox/ and suggest which folder each should go in and what the permanent filename should be."

Claude will propose a migration plan. You approve each move before Claude executes.

---

## Writing a new note in your voice

**Prompt:**
> "Draft a new note called 'Consulting Intake Process.md' in Resources/. Structure it as a checklist for onboarding a new consulting client. Match the tone and formatting of my existing notes."

Claude will read a sample of existing notes first (if you point it at examples) to calibrate tone.

---

## Tips

- **Always point Claude at examples.** "Match the style of Templates/Daily Note Template.md" produces better output than generic requests.
- **Use `git diff` as your review layer.** Claude edits many files silently; `git diff` makes every change visible.
- **Keep sessions focused.** One workflow per session produces cleaner results than "reorganize everything."
- **`CLAUDE.md` is living documentation.** Update it when your folder structure or conventions change — Claude will adapt automatically.
