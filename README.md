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

This is my own Windows 11 Home laptop (build 10.0.26200, x64) — not a university-managed machine, so I had normal admin permissions and no unusual restrictions to work around. It's an English-language system. The project folder lives inside a OneDrive-synced directory (`OneDrive\Desktop\SOC 910\...`), which isn't unusual exactly, but is worth noting since OneDrive sync can occasionally lock a file it's actively syncing — I didn't hit that, but it's the one machine-specific quirk of this setup. R and RStudio were already installed on this machine before I started (R 4.4.1), which turned out to matter — see question 3.

### 2. What did you install, and what is each piece for?

- **Claude Code** — the coding agent itself, run inside VS Code's integrated terminal.
- **Git** — version control for this repository.
- **GitHub CLI (`gh`)** — used to authenticate to GitHub and create/push this repo from the terminal instead of the web UI.
- **Python 3.13.14** and **Node.js** — runtime dependencies for tooling used during this build (e.g. `pdftotext`-adjacent scripting, Claude Code's own Node-based components).
- **VS Code** — the editor Claude Code runs inside.
- **R 4.6.1** (upgraded from the pre-existing 4.4.1) and the **`mcptools`** R package — these are what the MCP server (question 4) runs on.

### 3. What broke, what did the error actually say, and how did you fix it?

Installing the `mcptools` R package failed. R was already on this machine, but at an old-enough version (4.4.1) that CRAN no longer ships pre-built Windows binaries for it compatible with `mcptools`'s dependencies, so `install.packages()` tried to compile one of them (`httr2`) from source and failed with:

```
Error in loadNamespace(i, ...) :
  namespace 'rlang' 1.2.0 is being loaded, but >= 1.3.0 is required
```

Trying to install just `rlang` on its own hit the same wall — CRAN's Windows binary for R 4.4 tops out at `rlang` 1.2.0, and there was no compiler toolchain (Rtools) installed to build 1.3.0 from source. Rather than install a ~1.3GB compiler toolchain just to compile one package, I installed the current R release (4.6.1) side by side with the existing 4.4.1, which has current binaries available, and reinstalled `mcptools` against that version instead. That worked cleanly. Full details are in `setup/install.md`.

### 4. Which MCP server did you choose, why does it fit your research, and what did you ask the agent that it could answer only through that server?

I connected `r-mcptools`, an MCP server built on the `mcptools` R package, which lets Claude Code run R code and inspect live R session state. I originally planned to use the Stata connection from Week 5, but Stata isn't installed on this machine and I didn't want to buy a license just for this assignment, so I used R instead — R and RStudio were already installed, and R fits the quantitative side of sociology research (regression models, data cleaning) that this course also covers, even though the reading-notes project in this repo is qualitative/literature-based rather than a live dataset.

*(I still need to actually run a query through it before submitting — see the note below.)*

### 5. How is your project folder organized, what does your CLAUDE.md tell the agent, and what did you keep out of git?

The project folder is organized as a layered research wiki: `references/` for source-faithful notes on each paper, `concepts/` for theories and methods, `claims/` for my own synthesized/atomic claims, `projects/` for project-specific synthesis, `indexes/` for navigation, `templates/` for reusable note formats, `docs/` for the verification protocol, and `memory/`/`scripts/` for durable rules and utilities. The actual PDFs and their full-text `.md` conversions sit at the repo root. `project/README.md` and `project/structure.txt` in this repo describe this in more detail.

My CLAUDE.md tells the agent: the exact filename convention for articles (`Author (Year) Title.ext`, with a rule for how to verify the real citation when the filename doesn't already reveal it), how to handle the one known duplicate PDF in this collection, the structure to follow when converting a PDF to a full-text `.md` file, and — the rule that matters most — to never fabricate an author, year, title, journal, or citation; if something can't be verified, say so instead of guessing.

Kept out of git (`.gitignore`): OS junk files, editor/IDE state, this project's local machine-specific Claude Code settings (`.claude/settings.local.json`), any `.env`/key/credential files, and scratch/temp output. There's no participant or IRB-protected data in this project at all — everything here is published articles and my own notes on them — so that exclusion doesn't apply here, but I documented it in `.gitignore` anyway in case this workspace ever grows to include primary data.

### 6. When you clone this repository onto another of your machines and follow your install.md, what do you get, and what still has to be done by hand?

Cloning the repo gets me: the full readings/notes wiki, this project's `CLAUDE.md`, the `/convert-pdf` slash command, and written instructions for reinstalling Claude Code, Git, Python, Node, VS Code, R/RStudio, and the `mcptools` MCP server. What still has to be done by hand, because it doesn't travel with the repo: logging into GitHub (`gh auth login`) and Claude Code again on the new machine, re-registering the MCP server (the registration command is one line, but it has to be run locally — it's not something a cloned file can do for you), and adjusting the one machine-specific absolute path in the MCP registration command (the R version number in `C:\Program Files\R\R-<version>\...`) to match whatever's installed there. No paid licenses are involved in this setup, so there's nothing to re-purchase.

### 7. What did you customize, and what problem does it solve?

I wrote a slash command, `/convert-pdf` (`claude/commands/convert-pdf.md`), that automates turning a course reading into a full-text markdown copy while keeping both files side by side in the same folder.

Before this existed, every time I wanted a `.md` version of a PDF I had to redo the same three judgment calls by hand: first, check whether the PDF's filename already matched our convention (`Author (Year) Title.ext`) — and when it didn't, because it was a scanned PDF, a ProQuest export, or just a DOI-style name, dig through `pdftotext`/PDF metadata or search a bibliographic database to figure out the real author, year, and title before renaming it. Second, run `pdftotext -layout` to pull the text out. Third, manually reformat that raw text into our citation-header-plus-sections-plus-blockquotes-plus-references structure — the same structure decision every single time, with plenty of room to drift or skip a step under time pressure.

The command bundles all three steps into one invocation. It checks the filename against the convention first and only renames the PDF if it doesn't already match (verifying the real citation rather than guessing); once the PDF's name is settled, the `.md` file is created with that *same* base filename, just swapping the extension, so the two versions stay paired and are easy to find together in the folder. The `.md` file's top block carries the full citation — including the journal — even though the journal isn't part of the filename itself. The command also hard-codes the "never fabricate a citation" rule from my CLAUDE.md, so that check happens the same way every time instead of depending on me remembering to apply it.
