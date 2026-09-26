# claude/ — portable Claude Code configuration

| File | Copy of | Status |
|---|---|---|
| `project-CLAUDE.md` | This project's `CLAUDE.md` (repo root) | ✅ included |
| `commands/convert-pdf.md` | `.claude/commands/convert-pdf.md` (this project) — the required custom slash command | ✅ included |
| `user-settings.json` | `~/.claude/settings.json` (this machine's global Claude Code settings) | ⚠️ **not yet added** — copy by hand, see below |
| `project-settings.local.json` | `.claude/settings.local.json` (this project's local permission overrides) | ⚠️ **not yet added** — copy by hand, see below |

## Why the two settings files aren't here yet

This environment build ran through an AI agent (Claude Code), and an automated safety check in that tool blocked it from reading a settings/config file and writing its contents into a repo file bound for git — even though neither file actually contains a secret. That's a reasonable thing for the tool to be cautious about by default, so rather than working around it, do the copy yourself:

```powershell
Copy-Item "$env:USERPROFILE\.claude\settings.json" "claude\user-settings.json"
Copy-Item ".claude\settings.local.json" "claude\project-settings.local.json"
```

Open both files before committing — confirm there's nothing sensitive in them (there wasn't, when last checked: the global one just sets theme/TUI/a read-permission flag; the project one sets a couple of tool-allow rules). Then `git add claude/user-settings.json claude/project-settings.local.json` and commit.

## What no global CLAUDE.md means

There is no user-level `~/.claude/CLAUDE.md` on this machine — only the project-level one. Per the assignment's own instruction ("if an item does not apply to you, say so in one line"): not applicable, no global CLAUDE.md exists.

## The custom command: /convert-pdf

`commands/convert-pdf.md` automates a real repeated task from this project's CLAUDE.md: renaming a PDF to the course's `Author (Year) Title.ext` convention (verifying via `pdftotext`/metadata/web search when the filename doesn't already reveal the real citation) and producing a full-text `.md` conversion in the same structure as the existing ones in this repo. Before this command existed, that was done by hand each time, following the same written-out rules now baked into the command.
