# Extraction Report — Nodia Sample Papers (Phase 2)

Date: 2026-11-01 · Branch `arena/7d4f68ab-nodia`

## Deliverables (22 PDFs, all in `extracted_papers/`)

| File | Source | Pages | Status |
|---|---|---|---|
| Paper_01.pdf | Old book, CBSE Exam Paper 2026 (spacing-compacted from repo-root Paper_01.pdf) | 6 | verified |
| Paper_02.pdf | Old book, CBSE Exam Paper 2025 (spacing-compacted from repo-root Paper_02.pdf) | 6 | verified |
| Paper_03.pdf | `Maths 12th Sample Papers.pdf` SAMPLE PAPER 01 (source pp. 6–31) | 5 | verified |
| Paper_04.pdf | SAMPLE PAPER 02 (pp. 32–49) | 6 | verified |
| Paper_05.pdf | SAMPLE PAPER 03 (pp. 50–65) | 5 | verified |
| Paper_06.pdf | SAMPLE PAPER 04 (pp. 66–81) | 5 | verified |
| Paper_07.pdf | SAMPLE PAPER 05 (pp. 82–95) | 5 | verified |
| Paper_08.pdf | SAMPLE PAPER 06 (pp. 96–121, ad block 110–119 excluded) | 6 | verified |
| Paper_09.pdf | SAMPLE PAPER 07 (pp. 122–135) | 5 | verified |
| Paper_10.pdf | SAMPLE PAPER 08 (pp. 136–149) | 5 | verified |
| Paper_11.pdf | SAMPLE PAPER 09 (pp. 150–165) | 6 | verified |
| Paper_12.pdf | SAMPLE PAPER 10 (pp. 166–179) | 5 | verified |
| Paper_13.pdf | SAMPLE PAPER 11 (pp. 180–193) | 5 | verified |
| Paper_14.pdf | SAMPLE PAPER 12 (pp. 194–219, ad block 197–206 excluded) | 6 | verified |
| Paper_15.pdf | SAMPLE PAPER 13 (pp. 220–237) | 6 | verified |
| Paper_16.pdf | SAMPLE PAPER 14 (pp. 238–251) | 6 | verified |
| Paper_17.pdf | SAMPLE PAPER 15 (pp. 252–269) | 5 | verified |
| Paper_18.pdf | SAMPLE PAPER 16 (pp. 270–283) | 5 | verified |
| Paper_19.pdf | SAMPLE PAPER 17 (pp. 284–297) | 5 | verified |
| Paper_20.pdf | SAMPLE PAPER 18 (pp. 298–325, ad block 302–311 excluded) | 5 | verified |
| Paper_21.pdf | SAMPLE PAPER 19 (pp. 326–339) | 5 | verified |
| Paper_22.pdf | SAMPLE PAPER 20 (pp. 340–357) | 5 | verified |

Total: 22 PDFs. Source PDF `Maths 12th Sample Papers.pdf` and repo-root
`Paper_01.pdf` / `Paper_02.pdf` are **unmodified**.

## Method (native PDF editing, no retyping)

- Question content is copied page-area by page-area via clipped Form XObjects
  (`page.show_pdf_page(rect, src, pno, clip=rect)`), translate-only: all fonts,
  math (math-font glyph runs), vectors, tables and images are preserved exactly
  as rendered in the source. Nothing is rasterized; nothing is rebuilt from text.
- Output pages = copies of the source paper's own pages (chrome preserved:
  running headers "SAMPLE PAPER NN" / "page N" + book title, per-parity footer
  ad banners, margins, two-column grid) with the content band replaced by the
  reflowed question content.
- Solutions removed at `SSol :` markers (bold gray, 789 occurrences) and the rare
  `Ans :` variant (5 occurrences), by coordinate/dict-line analysis; question
  content never dropped for containing math; internal-choice separators
  (` O` / `\x01O` bold serif) handled with a lookahead rule that keeps question
  alternatives and drops solution separators (verified against SP01/02/03/15/16/20
  layouts).
- PDF page order in the new source is booklet-imposed (scrambled); logical reading
  order was recovered from question-anchor order and printed page numbers and
  cross-verified: stream anchors run 1..38 exactly once for every paper.
- Reflow: sequential two-column reading flow, 8pt between question blocks,
  4pt between pieces of the same block; blocks (question + options + figures +
  case-study text + internal choices) never split where avoidable.
- Page numbering renumbered 1..N consistently per output ("PAGE  N  " in the
  source's own ArialNarrow header style for new papers; "Page  N " in Euclid for
  the old papers), as permitted since page counts changed.
- Old papers (Paper_01/02): compaction of the Phase-1 outputs themselves; the
  Phase-1 white masking rectangles (invisible vector leftovers of the removed
  solutions) were identified and excluded, which removed the excessive gaps;
  internal gaps ≥30pt inside a question block = removed-solution remnants and
  were closed; blocks otherwise kept intact. The gutter "NODIA" watermark is
  preserved (re-set in Helvetica-Bold red, same style/position convention as the
  originals, on the pages whose originals carried it).

## Validation performed (all 22)

1. PyMuPDF + pypdf (strict=False) parse every page; page size 576×792 pt exact.
2. Text-layer leak scan: no `SSol`, `Sol :`, `Ans :` markers anywhere (no hidden
   solution text layers; painting is clip-restricted per content group).
3. Completeness scan: question anchors 1..38 present in every paper (both column
   margins), verified via bold numbering spans.
4. Visual checks (page renders): all 5 pages of Paper_03 inspected in full;
   Paper_04 p1/p3, Paper_05 p1/p2, Paper_06–07 first pages, Paper_08 p1,
   Paper_11 p6 (case-study sub-questions incl. internal choice), Paper_17 p3
   (pattern-B OR alternatives), Paper_22 p5 (both case studies with diagrams),
   Paper_01 p1/p2 and Paper_02 p1 in full. Checks cover reading order,
   question/option attachment, section headings, OR choices, figures/tables/
   color images, headers/footers, renumbering, watermark.

## Known limitations (disclosed, not invented)

- Visual QA is spot-check-based (every page of some papers, representative pages
  of the rest) plus the technical scans above; not every one of the 122 pages was
  individually eyeballed.
- The old papers' NODIA watermark is re-set as live text; the originals placed it
  at varying heights on alternating pages. It is reproduced on the same page
  indices as the originals (where within range) at the original per-page height.
- Old-paper question blocks that originally spanned both columns may now sit in a
  single column (reading order preserved; the two-column grid preserved).
- Word "Answer"/"Ans" inside question prose is untouched; only standalone marker
  rows are treated as solutions.

## Files

- Engine + audits: `.nodia_work2/scripts/extract.py`, `.nodia_work2/scripts/map_source.py`,
  `.nodia_work2/source_map.json`, `.nodia_work2/log_spNN.json` (working dir, not committed).
- Checkpoint: `PHASE_2_PROGRESS.md` (repo root).
- Audit detail: `extracted_papers/phase_2_audit_report.md`.
