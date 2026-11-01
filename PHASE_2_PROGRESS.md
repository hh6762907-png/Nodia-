# PHASE 2 PROGRESS — Nodia Sample Paper Extraction

Checkpoint file (updated after each batch). Session date: 2026-11-01.

## Completed setup
- Repository `/home/user/Nodia-`, branch `arena/7d4f68ab-nodia` (clean at start).
- `PROJECT_HANDOFF_NODIA_EXTRACTION.md` read in full (637 lines). Phase-1 history understood:
  - Paper_01.pdf = old book's CBSE Exam Paper 2026 (15 pp, 576x792), Paper_02.pdf = 2025 paper (17 pp).
  - Both are redaction-based question-only extracts; solutions removed but whitespace left -> excessive gaps (the defect to fix).
  - Old source `CBSE 12th Mathematics.pdf` (599 pp) is NOT in this repo; not required: the two outputs
    retain full page geometry (they are copies of source pages with answer regions redacted), so layout
    compaction can be done from the outputs themselves, using the handoff's redaction/segmentation notes.
- Visual reference screenshot inspected: Paper_01 p1 shows Q1 / big gap / Q2(a)(b) bottom-left,
  Q2(c)(d) top-right, Q3 mid-right / gap below -> gaps = removed solutions.
- Python venv `/home/user/.venv` with PyMuPDF 2.0, pypdf 6.21.4, Pillow, numpy.
- qpdf / poppler / tesseract NOT installable (no apt network) -> integrity QA via PyMuPDF + pypdf.
- Per-page text of new source cached in `.nodia_work2/pages/0001.txt..0358.txt` (working dir, not committed).

## Source PDF
- File: `Maths 12th Sample Papers.pdf` (repo root, 14,688,300 bytes, MUST NOT modify).
- 358 pages; PDF 1.7; AES-128 (empty user pw opens fine); producer pdfsam-console/iText.
- Title page: "CBSE 2026 MATHEMATICS Class 12th - 20 SAMPLE PAPERS with Full Explanation" (Nodia Learning, Oct 2025).
- Contents page (PDF p4) lists SAMPLE PAPER 01..20 with printed page nos 5,21,39,55,71,85,101,115,129,
  145,159,173,189,207,221,239,253,267,285,299.
- Structure confirmed: each paper = title block (full width) + two-column question flow with
  INTERLEAVED solutions ("Sol :" marker, gray #939598, Euclid-Bold; text-extract shows 'SSol :' artifact).
  Ad pages interleaved (e.g. PDF p21), some image-only pages (e.g. PDF p5).
- Page geometry (content pages): 576 x 792 pt. Columns: L x=36..282, R x=297..543, gutter 282..297.
- Headers: even pages "SAMPLE PAPER NN" top-right (ArialNarrow gray); odd pages "page NN" + book title.
- Running-header scan done (even pages): SP01 p6-30, SP02 p32-48, SP03 p50-64, SP04 p66-80, SP05 p82-94,
  SP06 p96-120 (gap 110-118), SP07 p122-134, SP08 p136-148, SP09 p150-164, SP10 p166-178, SP11 p180-192,
  SP12 p194-218 (gap 198-206), SP13 p220-236, SP14 p238-250, SP15 p252-268, SP16 p270-282, SP17 p284-296,
  SP18 p298-324 (gap 302-310), SP19 p326-338, SP20 p340-356. Exact bounds TBD in mapping stage.

## Extraction strategy
- Per-paper reading-order stream of content items (spans/images/drawings): wide items, then L col, then R col.
- Block starts = bold question-number anchors (x=36/297 margin) + "Section - X" headers; blocks may
  straddle columns/pages (e.g. Q2 options A,B bottom-left + C,D top-right) and are repacked as units.
- Solutions: drop items from `SSol :` marker until next block anchor / choice marker / section header
  (question text never dropped). Choice markers (` O` / `\x01O`) resume the question iff another
  `SSol` follows before the next anchor (else they are solution separators and stay dropped).
- Repack blocks into fresh output pages (same geometry, same 2-col grid): cross-page reflow so freed
  space is reused -> no large blank gaps; blocks never split where avoidable; piece gap ~4pt, block gap ~9pt.
- Painting via `page.show_pdf_page(target_rect, src_doc, src_pno, clip=source_rect)` = clipped Form
  XObject -> fonts/math/vectors/images preserved exactly; no rasterization, no text reflow.
- Chrome (headers/footers/gutter watermark) preserved by copying template source page per output page,
  redacting only the content columns, then painting blocks; "page NN" numbers renumbered 1..N via
  redact+insert with the embedded font (page count changes => numbering must be updated consistently).
- Paper_01/Paper_02: same engine; blocks = anchor-to-anchor content (answers already redacted);
  sub-split block pieces at internal gaps >= ~30pt (remnants of removed mid-question solutions).

## Current stage
- ALL STAGES COMPLETE. 22 deliverables in `extracted_papers/` (Paper_01..22.pdf) validated
  (technical + visual spot checks), reports written (`extracted_papers/extraction_report.md`,
  `extracted_papers/phase_2_audit_report.md`). Paper_01/02 compacted 15→6 and 17→6 pages
  (white-masking leftovers identified as the gap source; see audit report §6).
- Final validation: all 22 parse clean, questions 1..38 present in every paper, no solution
  markers in any text layer.

### Stage-1 findings (verified)
- 358 pages: 312 content, 40 ad (4 blocks of 10: p15-24, p110-119, p197-206, p302-311), 4 front
  matter (p1-4), 2 blank (p5, p358). 20 papers x 38 questions confirmed on actual pages.
- **PDF page order is scrambled (booklet imposition)**; logical order recovered from question-anchor
  order + printed page numbers (both agree exactly). Per-page reading order = L column top->bottom,
  then R column top->bottom. Solved orders logged per paper in `.nodia_work2/log_spNN.json`.
- Solution marker uniform: bold gray `SSol :` (789x). Internal-choice markers: bold serif ` O` /
  `\x01O` rows with two roles: (a) between question alternatives (keep), (b) between the two worked
  solutions (drop). Rule: a marker inside a drop resumes the question IFF an `SSol` follows before
  the next question anchor (lookahead); otherwise it stays dropped. Verified on SP01/02/03/15/16/20
  (SP02/SP15 use pattern [Q(a)][SSol][sol(a)][O][Q(b)][SSol]; others use [Q(a) O Q(b)][SSol][sol(a) O sol(b)]).
- Chrome = header ("SAMPLE PAPER NN" odd positions / "page N" + book title even positions;
  ArialNarrow 11pt gray #939598 baseline y=44.008) + per-parity footer ad art (preserved via template
  page copy). Full-width items only on title pages (title + instructions + rule).
- Anchorless pages content-verified: p165 (SP09) = case-study sub-questions (keep region, correct
  slot after passage page); p30/p102/p120/p162/p348/p31/p353/p357 = solution continuations (drop).
- Page numbering: outputs renumbered 1..N in the original per-page format (source numbers were
  book-global; page counts change).

## Batch log
- Batch 1 (SP01-05 -> Paper_03..07): extracted, technical validation passed (no SSol/Sol/Ans markers,
  correct page size, pypdf+PyMuPDF parse OK). Visual QA done for Paper_03 (all 5 pages: order 1..38,
  sections A-E, OR choices attached, figures/case-study images/tables intact, chrome + renumbered
  "PAGE N" headers, footers preserved) + spot checks on Paper_04 (p1, p3 incl. fixed `Ans :` leak),
  Paper_06/07 first pages. Engine fixes applied en route (documented in "Engine notes").
- Engine notes (bugs found & fixed during batch 1): (a) dict-line fragment rows cut at keep/drop
  boundaries -> visual-line clustering (band-overlap, per column) + sol-splits; (b) clip bands
  re-painted dropped rows (leaks) and cross-column pieces double-painted (title duplicate) ->
  per-group clip slabs with x-aware y-cuts against dropped rows; (c) pieces packed by source column
  broke reading order -> sequential L->R flow with column translation; (d) R-column start ignored
  wide-piece advance; (e) header renumber must use uppercase "PAGE  N  " (subset font maps lowercase
  to caps in the source itself); (f) rare solution marker `\x01Ans :` (5x in book) added to SOL_RE.

## Remaining tasks
- [x] Stage 1 page-boundary map + per-paper audit table
- [x] Stage 2-3 extract + validate SP01-05 (Paper_03..07) — 5-6 pp each, QA'd
- [x] Stage 4-5 extract + validate SP06-10 (Paper_08..12) — incl. SP09 case-study page QA
- [x] Stage 6-7 extract + validate SP11-15 (Paper_13..17) — incl. pattern-B OR QA (Paper_17)
- [x] Stage 8-9 extract + validate SP16-20 (Paper_18..22) — incl. SP20 case studies QA
- [x] Stage 10 spacing correction Paper_01/02 (15→6, 17→6 pages; watermark preserved)
- [x] Stage 11 final validation all 22 PDFs (integrity, questions 1..38, answer exclusion, visual)
- [x] Stage 12 reports (extraction_report.md, phase_2_audit_report.md) + commit + push

## Known issues / notes
- qpdf absent -> use PyMuPDF + pypdf strict parse for integrity checks.
- Source pages 1-4 front matter; 5 image-only (classification in mapping stage).
