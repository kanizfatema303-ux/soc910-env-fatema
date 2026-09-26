# SOC 910 — Environment we are building

Readings folder for a sociology course (SOC 910) on labor markets, precarious work, and the platform/gig economy — journal articles, book chapters, and a couple of the user's own slide decks (`Causal_Inference_and_ML_Summary.pptx`, `Popan and Anaya-Boig (2022) The Intersectional Precarity of Platform Cycle Delivery Workers.pptx`).

## Filename convention for articles

Article files (PDF/PPTX) in this folder are named `Author (Year) Title.ext` — e.g. `Kalleberg and Sorensen (1979) The Sociology of Labor Markets.pdf`.

- First author's last name only (add "and Second Author" or "et al." for 2/3+ authors), year in parentheses, then the paper/chapter/book title, with colons and question marks replaced by " - " since Windows filenames disallow `:` and `?`.
- When a file's real title/author/year isn't recoverable from the filename (scanned PDFs with no text layer, DOI-style names, ProQuest exports), verify via `pdftotext`/PyMuPDF text+metadata extraction first, then a web search against known bibliographic databases — do not guess.
- Non-article files (the user's own slide decks/summaries) are left alone; only published articles/chapters/books get renamed.

## Known duplicate

`Schor et al. (2020) Dependence and Precarity in the Platform Economy.pdf` and `...(duplicate).pdf` are the same *Theory and Society* article (previously saved twice under different names: `11186_2020_Article_9408.pdf` and `Schor et al 2020.pdf`). Not yet deleted — user hasn't said whether to remove it.

## Full-text markdown conversions

Some PDFs have a companion `.md` file with the full article text reformatted: title/author/journal citation up top, then section headers, block quotes for excerpts, and a full References list at the end. Created so far:
- `Kalleberg and Sorensen (1979) The Sociology of Labor Markets.md`
- `van Doorn (2017) Platform Labor - On the Gendered and Racialized Exploitation of Low-Income Service Work in the On-Demand Economy.md`

When asked to convert another PDF to `.md`, follow the same structure. Use `pdftotext -layout` to extract the source text, then manually reformat — not a raw OCR dump.

**Order of operations when asked to "transfer/convert a PDF to md":**
1. If the PDF isn't already named per the filename convention above, rename it first.
2. Then create the `.md` file using that *same* base filename (just swap the extension), following the full-text conversion structure above.

## Working with these files

- When the user references "the van Doorn one," "the Kalleberg one," etc., they mean by first-author surname per the naming convention above.
- When asked to summarize any file in this folder, always read the actual file first — never summarize from memory or assumption — then recheck the summary against the source before sharing it with the user.
- **Never fabricate references/citations.** Every author, year, title, journal, or citation used in a summary, a converted `.md`, or a renamed filename must come from the actual source document (or a verified web search against real bibliographic records) — never invented or guessed from a pattern. If something can't be verified, say so instead of making it up.
