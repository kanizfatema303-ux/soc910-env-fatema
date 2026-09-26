---
description: Rename a PDF to the course filename convention (if needed) and create its full-text .md conversion
---

Convert the PDF given in $ARGUMENTS to this project's full-text markdown format, following the rules in this project's CLAUDE.md. Specifically, in order:

1. **Check the filename convention.** Files should be named `Author (Year) Title.ext` — first author's last name only (add "and Second Author" or "et al." for multiple authors), year in parentheses, then the title, with `:` and `?` replaced by ` - `.
   - If the current filename already matches, skip to step 3.
   - If it does not match (scanned PDF, DOI-style name, ProQuest export, etc.), extract the real title/author/year with `pdftotext -layout` and/or PDF metadata first. If that's not conclusive, do a web search against a real bibliographic database (Crossref, journal site, Google Scholar). Never guess a citation from the filename pattern alone.
   - Rename the file to match the convention once verified.

2. Confirm the rename before moving on — show the old and new filename.

3. **Extract the source text** with `pdftotext -layout "<renamed file>.pdf" -`.

4. **Reformat into markdown**, using the same base filename with a `.md` extension, structured like the existing conversions in this repo (e.g. `Kalleberg and Sorensen (1979) The Sociology of Labor Markets.md`):
   - Title / author / journal citation at the top
   - Section headers matching the paper's own structure
   - Block quotes for direct excerpts
   - A full References list at the end, taken from the source document — never invented

5. **Never fabricate** any author, year, title, journal, or citation. If something in the source can't be read cleanly (bad OCR, missing pages), say so in the markdown rather than filling the gap with a guess.

6. Read back the finished `.md` file against the extracted source text once before finishing, to catch misattributed quotes or dropped sections.
