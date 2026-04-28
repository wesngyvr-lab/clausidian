# clausidian

A starter kit for wiring Claude Code to your Obsidian vault. Includes a bundled Claude skill that understands Obsidian Flavored Markdown, and a `CLAUDE.md` template you drop into your vault root so every future Claude session picks up your vault's conventions automatically.

For developers and knowledge workers who use Obsidian as a second brain and want Claude to edit notes without mangling wikilinks, frontmatter, or embeds.

---

## Prerequisites

- [Obsidian](https://obsidian.md/) with an existing vault
- [Claude Code](https://claude.ai/code) (the CLI)
- Git (optional but recommended — see [Why your vault should be a git repo](#why-your-vault-should-be-a-git-repo))

---

## Quickstart

**Step 1 — Add the vault template to your vault root**

```bash
cp templates/CLAUDE.md /path/to/your/vault/CLAUDE.md
```

Open the file and fill in the placeholders:

| Placeholder               | Replace with                                          |
|---------------------------|-------------------------------------------------------|
| `{{VAULT_NAME}}`          | Your vault's name (e.g. `My Notes`)                  |
| `{{VAULT_PATH}}`          | Path relative to home (e.g. `Obsidian/My Notes`)     |
| `{{DAILY_NOTE_PATTERN}}`  | Your daily note filename pattern (e.g. `YYYY-MM-DD`) |
| `{{ATTACHMENTS_FOLDER}}`  | Folder for images/PDFs (e.g. `Attachments`)          |

Edit the folder structure section to match your actual vault layout.

**Step 2 — Install the obsidian-vault skill**

```bash
# Option A: symlink (updates automatically when you pull)
mkdir -p ~/.claude/skills
ln -s /path/to/clausidian/skills/obsidian-vault ~/.claude/skills/obsidian-vault

# Option B: copy
cp -r skills/obsidian-vault ~/.claude/skills/obsidian-vault
```

That's it. Open Claude Code with your vault as the working directory and ask it to work on your notes.

---

## Why your vault should be a git repo

Obsidian Sync and iCloud are convenient, but neither gives you the control that git does. Here's why it's worth the one-time setup:

**Version history.** Every time Claude edits a batch of notes, `git diff` shows you exactly what changed before you commit. You can revert any edit with a single command.

**Multi-device sync via GitHub.** Push to a private GitHub repo and pull on any machine. Works alongside Obsidian Sync if you already use it — just `.gitignore` the workspace state files.

**Recovery from sync conflicts.** Obsidian Sync and iCloud occasionally create duplicate files. Git's conflict resolution tools handle these cleanly; a corrupted sync does not.

**Claude review of changes.** With git, you can ask Claude to `git diff` and explain what it changed, or to `git log` and summarize recent activity in your vault.

**Setup:**

```bash
cd /path/to/your/vault
git init
git remote add origin git@github.com:yourname/your-vault.git
echo ".obsidian/workspace*" >> .gitignore
echo ".obsidian/graph.json" >> .gitignore
git add .
git commit -m "Initial vault commit"
git push -u origin main
```

Keep your vault repo private unless you specifically want to publish it.

---

## Example workflows

### Writing a daily note

> "Create today's daily note using the template in Templates/Daily Note Template.md"

Claude reads your template, substitutes today's date, creates the file in `Daily/`, and leaves placeholder sections for you to fill in.

### Creating a project MOC

A Map of Content is an index note that wikilinks to everything related to a project — replacing rigid folder hierarchies with a flat, navigable graph.

> "Create a new MOC for the Onyx project. Link to the spec, meeting notes from April 2026, and any notes tagged #onyx."

Claude searches for relevant files, creates a `Categories/Onyx MOC.md`, and populates it with grouped wikilinks.

### Refactoring tag taxonomy

> "List all unique tags across my vault and identify near-duplicates. Then update all notes in Projects/ to use the agreed-on tags."

Claude audits your frontmatter, proposes a clean hierarchy, and makes the substitutions. Review with `git diff` before committing.

---

## Composing with community skills

clausidian bundles the `obsidian-vault` skill, which covers the core conventions. It composes with:

- [`obsidian-markdown`](https://github.com/wesngyvr-lab/clausidian) — broader Obsidian Markdown editing
- [`obsidian-cli`](https://github.com/wesngyvr-lab/clausidian) — Obsidian URI protocol and CLI interactions
- [`obsidian-bases`](https://github.com/wesngyvr-lab/clausidian) — `.base` database view files

Install any of these the same way: copy or symlink the skill directory into `~/.claude/skills/`.

---

## Repo structure

```
clausidian/
├── skills/
│   └── obsidian-vault/
│       └── SKILL.md          # the bundled Claude skill
├── templates/
│   ├── CLAUDE.md             # drop into your vault root
│   └── obsidian-claude-setup.md  # Obsidian note documenting the integration
└── docs/
    └── workflows.md          # common Claude + Obsidian workflows
```

---

## License

MIT. See [LICENSE](LICENSE).

## Contributing

Issues and PRs welcome. This is a small, focused tool — keep contributions scoped to Claude + Obsidian integration patterns. No dependencies, no build step.
