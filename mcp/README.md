# MCP server: r-mcptools

## What it is

[`mcptools`](https://github.com/posit-dev/mcptools) (Posit, CRAN package, v1.0.3) — an MCP server that lets Claude Code run R code and inspect R sessions/environments directly.

## Why R, not Stata

The course material (Week 5) covered both a Stata and an R connection. Stata was not installed on this machine and requires a paid per-seat license this environment build can't provision without a purchase — installing it wasn't an option consistent with "nothing new has to be installed." R and RStudio were already installed (R 4.4.1), so this build upgraded R to 4.6.1 (needed for current package binaries — see `setup/install.md` for why) and used the R MCP connection instead.

## Registration (one line)

```
claude mcp add -s "user" r-mcptools -- "C:\Program Files\R\R-4.6.1\bin\Rscript.exe" -e "mcptools::mcp_server()"
```

This writes an entry to the user-scoped Claude Code config (`~/.claude.json`). No API key, token, or password is involved — the server runs entirely locally, so there is nothing to redact here.

## Server config (as registered)

See `mcp/mcp-servers.json` in this folder for the exact entry Claude Code stores.

## Verifying the connection

```
claude mcp list
```

should show:

```
r-mcptools: C:/Program Files/R/R-4.6.1/bin/Rscript.exe -e mcptools::mcp_server() - ✔ Connected
```

or, inside a Claude Code session, run `/mcp`.

## Using it for real research

By default `mcp_server()` runs R code in a fresh/ephemeral R process per call. To let Claude read variables and objects from a *live* R or RStudio session you're actively working in, call `mcptools::mcp_session()` inside that session (or add it to `.Rprofile` via `usethis::edit_r_profile()` so it happens automatically every time R starts).

This is what makes it useful for actual sociology data work: once a live session is registered, you can ask Claude Code things like "what does `summary(my_model)` show in my current R session" or "what packages and objects do I have loaded right now" — questions it can only answer through this server, not by guessing, because the answer depends on your actual in-memory R session state.
