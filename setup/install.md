# Install steps — SOC 910 environment

Written for a Windows 11 machine with nothing installed. Versions referenced are in `versions.txt`.

## 0. Operating system

Windows 11 (Home or Pro). Steps below use PowerShell and the `winget` package manager, which ships with Windows 11 by default. Adjust package manager commands if you're on macOS/Linux (Claude Code, git, Python, Node, and VS Code are all cross-platform; R/RStudio/mcptools steps are identical).

## 1. Core tools

```powershell
winget install --id Git.Git -e
winget install --id Python.Python.3.13 -e
winget install --id OpenJS.NodeJS.LTS -e
winget install --id Microsoft.VisualStudioCode -e
winget install --id GitHub.cli -e
```

Restart the terminal after install so `PATH` picks up the new entries.

## 2. Claude Code

Install per the official instructions at https://docs.claude.com/claude-code (native installer or `npm install -g @anthropic-ai/claude-code`). Then:

```powershell
claude --version    # confirm it runs
```

Open the project folder in VS Code and use the Claude Code extension/CLI from an integrated terminal — this is "Claude Code runs inside VS Code" from the grading checklist.

## 3. GitHub auth

```powershell
gh auth login
```

Follow the interactive prompts (GitHub.com, HTTPS, browser login).

## 4. R + RStudio (needed for the MCP server)

```powershell
winget install --id RProject.R -e
winget install --id Posit.RStudio -e
```

**Known snag:** if the R version winget installs is more than ~1-2 minor releases behind current, CRAN may no longer publish Windows *binary* packages for it, and `install.packages()` will try to compile from source — which fails with an error like:

```
Error in loadNamespace(i, ...) :
  namespace 'rlang' 1.2.0 is being loaded, but >= 1.3.0 is required
```

Fix: install the current R release from https://cran.r-project.org/bin/windows/base/ (it installs side-by-side with any existing version; no need to remove the old one) and use its `Rscript.exe` for the steps below. Do not try to fix this by installing Rtools/a compiler toolchain unless you actually want to compile packages from source — upgrading R is the cheaper fix.

## 5. mcptools (R MCP server)

```powershell
& "C:\Program Files\R\R-<version>\bin\Rscript.exe" -e 'install.packages("mcptools", repos="https://cran.r-project.org")'
```

If you get a "library is not writable" warning, create a personal library directory first and pass it explicitly:

```powershell
mkdir "$env:LOCALAPPDATA\R\win-library\<Rmajor.minor>"
& "C:\Program Files\R\R-<version>\bin\Rscript.exe" -e 'install.packages("mcptools", repos="https://cran.r-project.org", lib="C:/Users/<you>/AppData/Local/R/win-library/<Rmajor.minor>")'
```

Then register the server with Claude Code (one line — full path to `Rscript.exe` is required on Windows):

```powershell
claude mcp add -s "user" r-mcptools -- "C:\Program Files\R\R-<version>\bin\Rscript.exe" -e "mcptools::mcp_server()"
```

Verify:

```powershell
claude mcp list
```

You should see `r-mcptools: ... - ✔ Connected`. Inside a Claude Code session, run `/mcp` to confirm the same thing from the client side.

To let Claude read variables from a *live* R session (not just run fresh code), call `mcptools::mcp_session()` inside that R/RStudio session, or add it to `.Rprofile` via `usethis::edit_r_profile()` so every session registers automatically.

## 6. Copy the portable config onto the new machine

```powershell
# User-level Claude settings
Copy-Item claude\settings.json "$env:USERPROFILE\.claude\settings.json"

# Project-level config — clone this whole repo, then from inside it:
Copy-Item claude\commands\*.md .claude\commands\ -Force
```

(`claude/CLAUDE.md` is this project's own `CLAUDE.md` — it's already at the repo root when you clone; nothing to copy.)

## 7. Check it worked

1. `claude --version` runs, and Claude Code opens inside VS Code's integrated terminal.
2. `claude mcp list` shows `r-mcptools` connected; `/mcp` inside a session shows the same.
3. `/convert-pdf` (from `claude/commands/convert-pdf.md`) appears as an available slash command.
4. `git log --oneline` in the cloned repo shows this project's commit history.
5. Ask the agent something that requires the R server (e.g. "what R packages are loaded in my current session, and what's `sessionInfo()` say") — it should answer via `r-mcptools`, not by guessing.

## What does not travel with this repo

- Your GitHub login / `gh auth login` session (accounts don't clone).
- Your Claude Code account/API authentication.
- Any paid software licenses (this environment deliberately avoids requiring one — see the MCP server note above about Stata vs. R).
- Machine-specific absolute paths (e.g. `C:\Program Files\R\R-4.6.1\...` — the version number will differ on a new machine; adjust the commands above accordingly).
- OneDrive sync state / the specific `C:\Users\<you>\OneDrive\...` path this repo happens to live under on this machine.
