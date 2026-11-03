# AGENTS.md

Guidance for AI coding agents working in this repository.

## Project Goal

German Slidev presentation for the finance course (Prof. Dr. Juliane Wolf), group 1:
**Profit as a corporate objective vs. Shareholder Value** based on Rappaport (1999), *Shareholder Value*, pp. 15–24.

The assignment asks for 1–2 content slides that:

- explain the shortcomings of profit as a corporate objective and why it is still popular,
- explain why profit and shareholder value do not always lead to the same decisions,
- back the arguments with examples.

## Files

- `slides.md` – the deck (cover, 2 content slides, closing, appendix).
- `VORTRAG.md` – speaker script and Q&A preparation.
- `docs/COMPONENT_API.md` – available layouts/components; use these before writing new ones.
- `literature.txt` – local OCR of the source text (git-ignored, copyrighted; do not commit).

## Rules

- Write in German. Keep numbers consistent with Rappaport (1999) and cite page numbers.
- Preserve the frontmatter schema (`presentationInfo`, authors, chapters); layouts depend on it.
- Validate with `npm run build` after content changes and `npm run lint` after component changes.
