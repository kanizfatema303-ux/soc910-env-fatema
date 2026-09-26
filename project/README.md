# How this research folder is organized

(Moved here from the old top-level `README.md` — see the root `README.md` for the Assignment 1 build report; this file is item 5, "project/", from that assignment.)

This workspace is organized as an accuracy-first research wiki for sociology reading, theory building, and literature synthesis.

## Purpose

The goal is not to produce fast summaries. The goal is to build a durable citation trail that stays source-faithful, transparent, and easy to verify.

Design principles:

- Source-first verification
- Five-layer note architecture
- Separate literature notes, concept notes, and claim notes
- Project-based synthesis without drift
- Clear indexing and retrieval structure

## Folder structure

- `references/` — source-faithful notes for papers and chapters
- `concepts/` — concepts, theories, and methods
- `claims/` — synthesized permanent notes
- `projects/` — project-specific work and analysis (plural — not to be confused with this `project/` folder, which is the Assignment 1 deliverable)
- `indexes/` — master navigation files
- `templates/` — reusable markdown note templates
- `docs/` — verification and accuracy protocols
- `memory/` — durable project and research rules
- `scripts/` — local maintenance or indexing utilities

Full two-level structure: see `structure.txt` in this folder.

## Core principles

1. Read the paper before writing anything about it.
2. Separate source summaries from your own interpretation.
3. Keep claims explicit and traceable to a literature or concept base.
4. Leave gaps blank instead of guessing.
5. Use citations only when the page exists and the source is verified.

See `PHILOSOPHY.md` (repo root) for the reasoning behind this, and `QUICKSTART.md` for the step-by-step workflow.

## .gitignore

`.gitignore` in this folder is a copy of the one actually in effect at the repo root — see it there for the live version. It excludes OS junk, editor state, local/machine-specific Claude Code settings, secrets, and scratch output. It deliberately does **not** exclude the PDFs/markdown — those are the point of this repository.

## Commit history

`last-20-commits.txt` in this folder is a sample of real use — see that file for the current list. This repository's git history starts 2026-09-26 (it wasn't tracked before then), so early on that list will be shorter than 20; it'll fill in as work continues.
