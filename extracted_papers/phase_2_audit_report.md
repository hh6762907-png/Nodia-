# Phase 2 Audit Report — Nodia Sample Paper Extraction

Date: 2026-11-01 · Engine: `.nodia_work2/scripts/extract.py`
Everything below is labeled **VERIFIED** (evidence produced in this session) or
**ASSUMED** (reasonable but not directly proven). Nothing is claimed without one
of those labels.

## 1. Source mapping (VERIFIED)

- `Maths 12th Sample Papers.pdf`: 358 pages, 576×792 pt, AES-128 (empty user pw).
  Page classification from per-page text dumps + geometry:
  312 content pages, 40 advertisement pages (4 blocks of 10: 15–24, 110–119,
  197–206, 302–311), 4 front-matter pages (1–4), 2 blank/image-only (5, 358).
- Contents page lists SAMPLE PAPER 01..20 at printed pages 5,21,39,55,71,85,101,
  115,129,145,159,173,189,207,221,239,253,267,285,299 (VERIFIED from text).
- Actual pages inspected contain exactly 38 question anchors (1..38) per paper
  (VERIFIED by anchor-stream scan, all 20 papers).

## 2. Page-order recovery (VERIFIED)

- PDF page order within a paper is booklet-imposed and scrambled. Logical order =
  the unique order in which question anchors run 1..38 monotonically, consistent
  with printed page numbers (printed = logical position + constant per paper).
  VERIFIED: the solved order's anchor stream is exactly 1..38, once each, for
  every paper (`.nodia_work2/scripts/extract.py probe`); page orders logged in
  `.nodia_work2/log_spNN.json`.
- Per-page reading order: full-width items first, left column top→bottom, then
  right column top→bottom (VERIFIED against solution-text continuity in dumps).
- **ASSUMED**: where anchorless continuation pages had more than one legal slot,
  the slot chosen (pdf-adjacency preference) is the intended one. All 5
  unprinted anchorless pages were content-inspected: 4 are solution
  continuations (slot choice is content-safe), 1 (p165) holds case-study
  sub-questions and its verified slot places it in the question region.

## 3. Marker taxonomy (VERIFIED)

- Solution marker: bold gray `SSol :` (Euclid-Bold, #939598) — 789 occurrences,
  uniform. Rare variant `Ans :` with the same styling — 5 occurrences
  (pp. 35, 66, 69×2, 82, 86), each verified as a solution heading after MCQ
  options.
- Internal-choice separator: bold serif standalone ` O` / `\x01O` rows, two
  roles: (a) between question alternatives — keep; (b) between the two worked
  solutions — drop. Rule implemented: a separator inside a dropped region
  resumes the question iff another solution marker follows before the next
  question anchor (lookahead), else it stays dropped. VERIFIED against concrete
  contexts in SP01, SP02, SP03, SP15, SP16, SP20 (both layout patterns occur).
- False markers ("Solving", "solution of", "Solve:", "Very Short Answer") are
  plain prose and are never treated as solutions (VERIFIED regex behavior).
- Section headings `SECTION - A..E` (5 papers use the capitalized variant) are
  kept and end the drop state (VERIFIED).

## 4. Extraction integrity (VERIFIED)

- Every question anchor 1..38 present in every delivered PDF (bold number spans
  at both column margins), all 22 files.
- No `SSol` / `Sol :` / `Ans :` text anywhere in the delivered PDFs (text-layer
  scan of all pages). Painted content is clip-restricted per visual-line group,
  with y-band cuts at dropped rows that x-overlap, so dropped text cannot appear
  even as clipped/hidden text.
- Page boxes 576×792 pt, pypdf + PyMuPDF parse clean on all 22 files.
- MCQ options kept attached to their questions; questions that start in one
  column and continue in the next keep left→right reading order (VERIFIED by
  renders of Paper_01 p1/p2, Paper_03 p1–p5, Paper_04 p3, Paper_11 p6,
  Paper_17 p3, Paper_22 p5).

## 5. Preservation (VERIFIED / ASSUMED)

- Fonts/math/vectors/images: preserved as clipped Form XObject references of the
  original pages (translate-only); VERIFIED visually (fractions, integrals,
  matrices, determinants, vector arrows, colored case-study photos, graph
  figures, LPP diagrams all render identically to the source).
- Headers/footers/margins/two-column grid: copied from each paper's own template
  pages (VERIFIED in renders; footer ad banners intentionally preserved as part
  of the original page design).
- **ASSUMED acceptable**: footer advertisement banners are retained (they are
  part of the book's page chrome; the user asked for original formatting to be
  kept). Removing them would alter the page design.
- Page numbering: renumbered 1..N in the original per-page format and font
  (VERIFIED in renders; the new-source subset maps lowercase to capitals in the
  source itself, so the header renders "PAGE N" exactly like the source style).
  The source numbering was book-global and is meaningless after re-pagination;
  consistent 1..N numbering applied to all 22 files.
- Source files unmodified (VERIFIED: only `extracted_papers/`, `.nodia_work2/`
  (working), `PHASE_2_PROGRESS.md` and these reports written).

## 6. Old papers (Paper_01 / Paper_02) — VERIFIED

- Excessive gaps traced to (a) removed-solution whitespace and (b) Phase-1 white
  masking rectangles left in the content stream (invisible white-fill drawings,
  up to 125pt tall, which also blocked vertical compaction). VERIFIED by drawing
  inspection on Paper_01 p1 and by the fact that excluding them collapsed the
  papers 15→6 and 17→6 pages at question-only density consistent with the 20 new
  papers (5–6 pages each).
- Blocks treated as units; internal gaps ≥30pt inside a block closed (remnants of
  removed mid-question solutions). Reading order preserved (left→right flow);
  MCQ options rejoin their questions when the source had split them across
  columns (VERIFIED: Paper_01 Q2 (A)–(D) together in the output p1 render).
- The gutter "NODIA" watermark: originals carry it on alternating pages at
  varying heights (VERIFIED span scan: Paper_01 pp. 2,5,7,9,11,12,14; Paper_02
  pp. 2,5,7,9,11,12,14,16). Reproduced as rotated Helvetica-Bold #ff073a text on
  the same page indices (within the new page count) at the same heights.
  **ASSUMED**: this per-page placement is the right convention after reflow.

## 7. Residual risks (disclosed)

- **ASSUMED low risk**: a very tall stacked math glyph overhanging the opposite
  side of a solution marker by more than a line could theoretically be trimmed
  by the y-band clip cuts. No such case was observed in visual QA.
- Visual QA covered every page of Paper_03 and representative pages (first /
  middle / last / marker-heavy) of the rest plus both old papers' first pages.
  A page-by-page human pass over all 122 pages is the only stronger check.
- "Internal choice" prose (instruction 8) exists; the printed separators found
  are the ` O` / `\x01O` rows. Papers whose choices are phrased inline in prose
  show no separate separator rows (VERIFIED: marker counts per paper, e.g.
  SP02/SP04/SP13/SP15 use the pattern where the separator sits inside the
  solution region and is resolved by the lookahead rule; others use paired
  separators around alternatives).

## 8. Corrections made during the run (transparency)

1. Fragment rows cut at keep/drop boundaries → visual-line grouping (band
   overlap per column) + sol-row splits.
2. Clip bands re-painted dropped rows (leaked `SSol` in early drafts) and
   cross-column pieces double-painted title text → per-group clip slabs with
   x-aware y-cuts; title preamble forced into one wide block.
3. Pieces packed by source column scrambled reading order → sequential L→R flow
   with column translation (dx = 0 / ±261 pt).
4. R-column restart ignored the wide block's cursor advance (content overlapped
   the title) → cursor-aware column switch.
5. Header renumber rendered lowercase invisible (subset font maps lowercase to
   capitals) → uppercase "PAGE  N  " matching the source's rendered style.
6. Rare `Ans :` solution marker (5 occurrences) added to the solution regex after
   a visual QA leak was found and traced (Paper_04 p3).
7. Old-paper compaction blocked by white masking rectangles → invisible drawing
   groups excluded from re-painting.

Each correction was followed by re-extraction and re-validation of the affected
papers (final state of all 22 files passes everything in section 4).
