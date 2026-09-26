# SOC 910 — Environment Build

**Course:** SOC 910, How to Use AI for Sociological Research, Fall 2026 — Assignment 1
**Repo:** `soc910-env-fatema`

## What this environment is

A portable copy of the Claude Code + git + MCP setup used for this course's sociology research project (a readings/notes wiki on labor markets, precarious work, and the platform economy — see `project/README.md` for how that side is organized). Cloning this repo and following `setup/install.md` should rebuild the same setup on another machine.

## Install summary

1. Install Claude Code, Git, Python, Node.js, VS Code, GitHub CLI (`setup/versions.txt` has exact versions).
2. Install R + RStudio, then the `mcptools` R package, then register it as an MCP server with Claude Code (`mcp/README.md`).
3. Copy `claude/project-CLAUDE.md` (this project's CLAUDE.md, already at the repo root once cloned) and `claude/commands/convert-pdf.md` into place; copy the two Claude settings files noted below.
4. Verify with `claude mcp list` / `/mcp` and by running `/convert-pdf` on a PDF.

Full steps, including a real dependency snag hit during this build and its fix: `setup/install.md`.

**Note on two files not yet in `claude/`:** `claude/user-settings.json` (the machine's global `~/.claude/settings.json`) and `claude/project-settings.local.json` (this project's `.claude/settings.local.json`) still need to be copied in by hand — an automated safety check in this environment blocked copying config files sourced from outside the repo/from `.claude/` into a file destined for git, so a person needs to do that copy step deliberately. Both files are small; see `mcp/README.md` and `claude/README.md` for what's expected to be in them.

## What's in this repository

| Path | What it is |
|---|---|
| `setup/` | `versions.txt`, `install.md` |
| `claude/` | Portable copies of CLAUDE.md, settings, and the `/convert-pdf` slash command |
| `mcp/` | The `r-mcptools` (R) MCP server config and registration command |
| `project/` | How the research folder itself is organized: `.gitignore`, `structure.txt`, `last-20-commits.txt` |
| `screenshots/` | Four required screenshots — **not yet added**, see `screenshots/README.md` |
| Everything else at the root | The actual sociology readings/notes wiki this environment supports |

## Screenshots

_(To be embedded here once added — see `screenshots/README.md` for exactly what's needed.)_

---

## Build report

### 1. What machine is this, and was anything unusual about it?

_(answer here)_

### 2. What did you install, and what is each piece for?

_(answer here)_

### 3. What broke, what did the error actually say, and how did you fix it?

_(answer here — note: `setup/install.md` already documents the R/rlang binary-compatibility error hit during this build, in case that's useful raw material for this answer)_

### 4. Which MCP server did you choose, why does it fit your research, and what did you ask the agent that it could answer only through that server?

_(answer here)_

### 5. How is your project folder organized, what does your CLAUDE.md tell the agent, and what did you keep out of git?

_(answer here)_

### 6. When you clone this repository onto another of your machines and follow your install.md, what do you get, and what still has to be done by hand?

_(answer here)_

### 7. What did you customize, and what problem does it solve?

_(answer here)_
