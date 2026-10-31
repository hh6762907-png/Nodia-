# Nodia Sample Paper Extraction — Complete Project Handoff

**Purpose:** Single-document transfer of project history, requirements, technical decisions, validation evidence, current repository state, and safe instructions for a new AI-agent session.  
**Handoff created:** 2026-10-31 (local project date)  
**Repository path in the session that created this document:** `/home/user`  
**Important:** This file is a handoff aid, not a substitute for checking the actual connected Git repository. On a new session, inspect the repository and let its current state take precedence over historical descriptions below.

---

## 0. Executive handoff

The original task was to identify and extract every complete Nodia sample/examination question paper from a 599-page PDF, leaving out answer material while preserving original page appearance. The source contained two complete CBSE Class 12 Mathematics examination papers: 2026 and 2025. Both were extracted as separate, question-only PDFs. A subsequent independent audit revisited the entire source and all output pages and found no additional complete paper and no verified defect requiring PDF changes.

The local project currently has these deliverables under `extracted_papers/`:

1. `Paper_01.pdf` — 2026 paper, 15 pages.
2. `Paper_02.pdf` — 2025 paper, 17 pages.
3. `extraction_report.md` — initial extraction and validation report.
4. `second_audit_report.md` — independent second-audit report.

The local repository has two commits on `main`:

- `ff7bf1bed7eb11a7ff200d9039d09866411346ce` — `feat: extract all Nodia sample question papers into separate PDFs`
- `51cde6e13e1d8007e560e39a679938845d7c4773` — `docs: add independent second audit report`

**No Git remote is configured in the inspected workspace. No push was made.** These commits must not be represented as present on GitHub until a new agent verifies the actual connected repository and synchronization state.

The original source file is currently available in the inspected local workspace at `.nodia_work/source/CBSE 12th Mathematics.pdf`, but `.nodia_work/` is excluded from Git and is not a deliverable. A new clone or agent session may not contain that local source copy. The source originally resides in Google Drive; Drive is permitted **only as a read-only source** for that PDF.

At the time this document was written, before this new file was added, the local `main` working tree was clean. This handoff itself is intentionally **not committed**. After its creation, a normal `git status` should therefore report it as an untracked root-level file unless some external process stages or commits it.

**Project completion status:** extraction complete; independent audit complete; existing PDFs unchanged by the second audit; no known project correction is pending. The next session's primary job is to inspect its actual GitHub-connected repository, determine what commits/files are there, and carefully synchronize or recover only what is missing.

---

## 1. Evidence labels and how to read this document

To avoid conflating history with present truth, this handoff distinguishes:

- **Verified in the inspected local repository:** directly checked during creation of this handoff (branch, status, commits, paths, sizes, hashes, PDF page counts, qpdf checks, and currently installed tool versions).
- **Recorded in committed project reports:** details found in `extracted_papers/extraction_report.md` and `extracted_papers/second_audit_report.md`. These are project records and should be read directly if they are available.
- **Historical execution record:** information from the original agent's execution log and persistent local analysis artifacts. It describes what was performed in the original workspace; it does not prove that a different clone has those artifacts.
- **Unknown / must be checked in a new session:** any GitHub state, remote URL, user's actual repository identity, or Drive access/perms available to a different agent session.

The repository connected in a new conversation may have advanced, diverged, or be a different checkout. Its current state overrides this historical handoff where they disagree. Do not blindly reset, cherry-pick, overwrite, force-push, or copy files over newer work.

---

## 2. Original objective and project scope

### 2.1 Objective

Find every complete Nodia sample/examination question paper in one large PDF and create one separate, high-fidelity, question-only PDF per paper in `extracted_papers/`. The supplied source was approximately 40 MB and was stored in Google Drive because it exceeded repository upload limitations. The agent was allowed to use Drive exclusively to locate and download the original PDF; all PDF analysis, OCR, extraction, quality assurance, reporting, and Git work had to occur in the repository/workspace.

The user specifically required the work to include every paper instance, including duplicates or near-duplicates if any existed. Papers were not to be merged or deduplicated.

### 2.2 Original requirements — all remain binding

For every complete paper instance:

- Produce one PDF per paper, using sequential filenames such as `Paper_01.pdf`, `Paper_02.pdf`, and so forth.
- Include questions only. Exclude answers, answer keys, worked solutions, explanations, answer-revealing hints, teacher notes, and solution manuals.
- Preserve the original PDF appearance as closely as possible: page size and orientation, margins, fonts and font sizes, text positioning, columns, spacing, headers, footers, numbering, section labels, marks, and pagination.
- Preserve every question, subquestion, instruction, option, passage, case study, diagram, map, chart, table, equation, graph, and other question content.
- Preserve Hindi and English material and relevant mathematical notation. OCR is an analysis aid for scanned or sparse pages and must not be used to reconstruct digital question pages unnecessarily.
- Inspect the complete source, not merely likely paper ranges. Use text/layout/heading analysis, OCR where required, and visual review for ambiguous boundaries.
- Retain duplicate paper instances; never deduplicate based on similarity.
- Handle pages containing both questions and solutions carefully. Do not treat a whole mixed page as all-question or all-answer content without contextual inspection.
- Do not modify the original source PDF in Drive.
- Save final deliverables in `extracted_papers/`; investigate existing files before overwriting anything.
- Validate the actual PDFs—not just that files exist—using structural, text, and visual checks.
- Preserve unrelated repository files and existing user changes. Inspect branch/status before processing and stage only intentional deliverables.
- Commit verified deliverables safely on local `main`. Never force-push, invent a remote, claim that local commits were pushed, or overwrite remote work.
- Be explicit about limitations and anything that could not be verified.

### 2.3 Drive restriction for every future agent

Google Drive is **read-only and only for locating/downloading the source PDF**. The new agent must not:

- edit, overwrite, delete, rename, or move the original;
- create Drive folders or organize Drive contents;
- upload extracted PDFs, reports, scripts, temporary files, or anything else to Drive;
- access unrelated Drive documents.

Source filename: **`CBSE 12th Mathematics.pdf`**. The historical Drive file ID recorded in project metadata is `1D35QS2LrkK1H0ZwG-koV1_F2oY-1yAsR`; this is an identifier, not a guarantee that a future session has access. Do not assume the new agent inherits Drive authorization. If the source must be inspected again, use only the authorized read-only Drive connector available in that session. If permission/access is unavailable, state the exact limitation; do not ask the user to re-upload unnecessarily, and do not pretend a source re-check occurred.

---

## 3. Source document and verified identity

### 3.1 Exact source facts

| Property | Value | Evidence / status |
|---|---|---|
| Filename | `CBSE 12th Mathematics.pdf` | Verified in local source path and reports. |
| Original location | Google Drive | Recorded in extraction report; source was downloaded via read-only Drive operations. |
| Size | 47,655,270 bytes | Verified locally and against Drive metadata in the historical session. |
| Approximate size | About 40 MB as described in the task | User-provided approximate description; exact bytes are above. |
| Page count | 599 | Verified with PDF inspection and source metadata. |
| MD5 | `c663ba89e680784c605675e606580fc3` | Verified against Drive metadata at download time and locally. |
| SHA-256 | `d9a724fca3dd49bc5bb3b9ff32417b8b4467c33c4eff31a0446728b8673d1299` | Verified locally and recorded in reports. |
| PDF metadata title | `Processed by Nodia` | Read from source metadata. |
| Creator / producer | `nodia.in` / `Nodia PDF Processor v2.0` | Read from source metadata. |
| Encryption/permissions | Owner-password permission flags; empty user password works for reading | PyMuPDF opened it; qpdf checked it. Do not treat this as a reason to alter the source. |
| Local source copy now | `.nodia_work/source/CBSE 12th Mathematics.pdf` | Exists in the inspected workspace; excluded from Git. May not exist in another clone. |

Historical Drive metadata observed at initial download and re-check: MIME type `application/pdf`, file not trashed, size unchanged, and `modified_time = 2026-09-26T01:29:16.738Z`. Drive read/write history recorded **zero Drive writes**. Do not infer that this metadata is current in a new session without checking.

### 3.2 Facts versus initial-workspace history

- **Historically reported and recorded in `extraction_report.md`:** the initial supplied workspace contained no existing Git repository, project files, or remote; the agent initialized a local repository on branch `main` for the deliverables.
- **Verified now in the inspected workspace:** `/home/user` is a Git repository, on `main`, and has no configured remote. This is still only the local session repository, not proof of GitHub synchronization.
- **Unknown:** the actual repository URL/name and the contents of the user's GitHub repository. The new agent must discover these from the connected environment/user's setup rather than manufacture a remote URL.

---

## 4. Full-document analysis and paper classification

### 4.1 What was identified

Two complete CBSE Class 12 Mathematics examination papers were identified:

1. **CBSE Examination Paper 2026** — source begins at page 7.
2. **CBSE Examination Paper 2025** — source begins at page 33.

The remaining material is front matter, advertisements/back matter, and a chapter-wise solved question bank spanning 13 mathematics chapters. The chapter bank has questions organized by chapter/question type and solutions interleaved; it is not a set of separately complete examination papers.

### 4.2 Classification evidence

The analysis considered the complete source, including page text, page layout, headings, fonts, images, vector paths, question-number patterns, paper instructions, and OCR for sparse/image-heavy pages. Text/heading/keyword searches were treated as discovery aids rather than sole classification evidence.

Recorded scan findings:

- The table of contents on source page 5 lists only CBSE Examination Paper 2026 and CBSE Examination Paper 2025 before the chapter bank.
- “General Instructions,” `Time : 3 Hours`, `Max. Marks : 80`, and complete 38-question-paper structure identify source pages 7 and 33 as the only complete paper starts.
- There are 33 question-bearing pages across the two paper ranges; advertisement page 37 falls inside the nominal page span for the 2025 paper, and page 32 after the 2026 question pages is solution-only.
- The chapter bank starts at source page 52 and proceeds through 13 chapters, with question categories such as OBJECTIVE, VERY SHORT ANSWER, SHORT ANSWER, LONG ANSWER, and CASE BASED. Those categories do not make the bank a complete sample paper.
- A source-page 102 citation “OD Sample Paper 2023” occurs inside a chapter-bank solution/question context; it is not a separate paper.
- Other “sample” hits are uses such as “sample space” or “sample choice test”; “practice” hits are advertisement subject names; “previous year” hits are cover/advertisement language or a question context. These were reviewed in context.
- No additional complete model, mock, practice, sample, previous-year, or separately labelled paper was found in the 599-page source during the second audit.

### 4.3 Excluded page groups

| Source pages | Classification | Why not an extracted paper |
|---|---|---|
| 1–6 | Cover, promotional material, title/copyright/contents | Front matter and advertisements, not a question paper. |
| 10–19 | Advertisements | Promotional inserts between parts of the 2026 paper; no paper questions. |
| 32 | 2026 solution continuation | Answer/solution-only continuation after question-bearing source page 31; no remaining question text. |
| 37 | Advertisement | “Better than book” page inserted in the nominal 2025 span; not a paper page. |
| 51 | Advertisement | Nodia app promotion after the 2025 paper. |
| 52–598 | Chapter-wise question bank and interspersed ads | Chapter-organized questions/solutions, not independent complete papers. |
| 63–73 | Advertisement group within chapter-bank range | Promos for other classes/subjects/worksheets and “Better than book.” |
| 99, 125, 151, 177, 203, 229, 230, 256, 282, 308, 334, 360, 386, 412, 438, 464, 490, 516, 542, 568, 594 | Repeated advertisements | Promotional inserts, not question-paper content. |
| 599 | Purchase/back-cover advertisement | Back matter, not a question paper. |

Recorded chapter-bank starts: Chapter 1 p52; Chapter 2 p94; Chapter 3 p118; Chapter 4 p146; Chapter 5 p195; Chapter 6 p251; Chapter 7 p311; Chapter 8 p379; Chapter 9 p392; Chapter 10 p444; Chapter 11 p482; Chapter 12 p515; Chapter 13 p541.

### 4.4 Duplicate policy

The requirement was to retain every duplicate/near-duplicate paper instance. The audits found **no duplicate complete paper instances** in the source. This is why the reported duplicate count is zero; it was not a deduplication decision.

---

## 5. Extraction outputs and paper boundaries

### 5.1 `Paper_01.pdf`

- Paper: CBSE Class 12 Mathematics Examination Paper 2026.
- Source question-paper pages: 7–9 and 20–31.
- Source page 10–19 advertisements are omitted.
- Source page 32 is solution-only and omitted.
- Output: 15 pages, 294,331 bytes.
- SHA-256: `3bec38f885d5bea2fbb091870f99befa79cd47416770877ba989e1458a2a0990`.
- Q1–Q38 verified present.

### 5.2 `Paper_02.pdf`

- Paper: CBSE Class 12 Mathematics Examination Paper 2025.
- Source question-paper pages: 33–36 and 38–50.
- Source page 37 is a full-page advertisement and is omitted.
- Output: 17 pages, 332,732 bytes.
- SHA-256: `748febe7510d0eac7d4f369247571c6f2dfc3c8798996d64532b7cc84095e12a`.
- Q1–Q38 verified present.

### 5.3 Other deliverables

- `extracted_papers/extraction_report.md` — original extraction report, 8,216 bytes, 113 lines at handoff inspection.
- `extracted_papers/second_audit_report.md` — independent second-audit report, 17,373 bytes, 356 lines at handoff inspection.
- `PROJECT_HANDOFF_NODIA_EXTRACTION.md` — this transfer document; intentionally not committed by the session that created it.

Total extracted page count: **32** (15 + 17). Both output PDFs have page size `576 × 792 pt`, rotation 0, PDF 1.7, and are unencrypted.

---

## 6. Technical implementation

### 6.1 Tools actually used / tool availability

The original execution and final workspace inspection establish the following. Where a distinction matters, “used” means the scripts or reports show use; “installed” alone does not prove use in the extraction logic.

| Tool / library | Version found in inspected environment | Use / evidence |
|---|---|---|
| Python | 3.13.16 | Analysis, extraction, OCR orchestration, validation scripts. |
| PyMuPDF (`pymupdf` / `fitz`) | PyMuPDF 2.0; bound MuPDF 1.28.5 | **Core PDF library used** for source parsing, layout inspection, page rendering, copying, redactions, output inspection. |
| Tesseract | 5.5.0 | OCR engine used on sparse/image-heavy pages. |
| Tesseract languages | `eng`, `hin`, `osd` installed | OCR configured as `eng+hin`; the question papers themselves were digitally readable. Hindi OCR support was included for sparse source pages. |
| pytesseract | 0.3.13 | Python OCR wrapper used by scripts. |
| Pillow | 12.3.0 | Image conversion/handling and contact-sheet construction. |
| NumPy | 2.3.5 | Pixel/mask comparisons in validation scripts. |
| qpdf | 12.2.0 | `qpdf --check` integrity checks. |
| Poppler `pdfinfo` / `pdftoppm` | 25.03.0 | Utilities available and PDF metadata/page checks were performed; not the core page extraction engine. |
| pypdf | 6.21.4 | Installed; available in environment. Actual use in this workflow is not established. |
| pdfplumber | 0.11.10 | Installed; actual use in this workflow is not established. |
| OpenCV (`opencv-python`) | 4.11.0.86 | Installed; actual use in this workflow is not established. |
| Git | 2.47.3 | Local repository/history/staging/commits. |

The environment also had approximately 1.9 GiB RAM and 2 CPUs according to the earlier workspace record; that resource figure was not remeasured at handoff creation and should be treated as historical only.

### 6.2 Analysis and page inventory

The analysis script `.nodia_work/scripts/analyze_source.py`:

- verifies the downloaded source MD5 before analysis;
- opens the complete document with PyMuPDF;
- checks SHA-256, page count, metadata, encryption/permission state, and qpdf check notes;
- iterates all 599 pages;
- extracts per-page text and saves it separately;
- inspects text spans, bounding boxes, fonts, font sizes, colors, images, drawing/vector-path counts, links, annotations, and page dimensions;
- writes per-page summaries and a heading inventory.

Full page text is stored as `.nodia_work/analysis/pages/0001.txt` through `0599.txt`; page summaries are in `.nodia_work/analysis/page_summaries.json`; heading output is `.nodia_work/analysis/headings.txt`.

### 6.3 OCR

OCR was an aid for low-text/sparse/image-heavy source pages, not a way of rebuilding the paper PDFs. The recorded configuration:

- Tesseract 5.5.0;
- languages `eng+hin`;
- rendering at 200 dpi;
- page segmentation mode 3 (`--psm 3`);
- 90-second timeout per page.

The 26 OCR pages were source pages 1, 2, 37, 73, 99, 125, 151, 177, 203, 229, 230, 256, 282, 308, 334, 360, 386, 412, 438, 464, 490, 516, 542, 568, 594, and 599. Recorded OCR errors: 0. Sparse pages were mostly advertisements/front/back matter. OCR outputs are in `.nodia_work/analysis/ocr/` and `.nodia_work/second_audit/ocr/`.

### 6.4 Paper boundary and answer/question classification

The extraction was not a simple whole-page split. Questions and worked solutions share pages and columns. The script `.nodia_work/scripts/classify_extract.py` uses a per-column question/answer state model:

- Uses text span positions/font/color and page/block geometry to identify question anchors, section/instruction anchors, and `Sol :` markers.
- `Sol :` is gray (`color == 8421504`) and bold in the source; color alone was insufficient, so labels and contexts were reviewed.
- Question numbers were detected as bold, black spans at the column margins; block-top position was used as the anchor because equations/numerators can rise above the number glyph.
- Columns are treated separately so the answer state on one side does not spill into the other.
- Per-page extraction state includes source page, output page, column events, initial state, and redaction rectangles in `.nodia_work/analysis/extraction_plan.json`.
- The final extraction script has `MANUAL=[]`; a prior manual override mistakenly included solution text at source p31 right column and was removed. Do not reinstate it.
- Answer-only source page 32 is excluded rather than emitted as a blank/solution page.
- Advertisements inside paper ranges are omitted by selecting individual source pages.

**Final recorded parameters:**

- `QUESTION_GAP = 8.0` points above next question anchors, added after rendering revealed clipping of ascenders/equation limits at smaller gaps.
- Partial `Sol :` label redaction starts at `Sol.y0 + 0.6` to retain the last portion of the preceding question line while removing the label and solution.
- Source page clipping/answer masks use top around y=62 pt, bottom y=752 pt, two-column regions, with left/right coordinates recorded in the script and plan. The Nodia gutter is approximately x=282.4–309.9 pt.
- Paper_01 left/right mask boundaries use x≤282.34 and right x=314.5–544.0; Paper_02 left starts at x=35.0 (right start x=314.5). Exact rects vary per page and are persisted in the plan.

### 6.5 Redaction and PDF generation

- PyMuPDF `insert_pdf` copies original source pages into a new output document; text is not reflowed and digital pages are not rasterized wholesale.
- Targeted redaction rectangles remove the answer text/graphics while retaining original page geometry and page appearance as far as possible.
- Redactions are applied with `apply_redactions(images=2, graphics=1, text=0)` as recorded in the extraction script. Question text and relevant images outside answer masks are retained. Solution-only images within answer masks are removed.
- Whitespace remains where answers were removed intentionally; pages are not reformatted to close gaps.
- Output save uses PyMuPDF compression/cleanup settings (`garbage=4`, `deflate=True`) as shown in `classify_extract.py`.
- Pages 7–9 and 20–31 are copied for 2026. Pages 33–36 and 38–50 are copied for 2025. This preserves page geometry, fonts, image resources, vector lines, equations, and paper pagination.

### 6.6 Relevant scripts

Scripts were created under `.nodia_work/scripts/` (excluded from Git). This directory is local processing evidence; it is not part of the committed user deliverables.

| Script | Purpose |
|---|---|
| `analyze_source.py` | Full 599-page inventory: text, layout, font/color spans, images, drawings, page geometry, headings, metadata and hashes. |
| `ocr_sparse_pages.py` | OCR pages whose extracted text is sparse, using `eng+hin`. |
| `render_overview.py` | Source contact sheets and selected higher-resolution page renders. |
| `classify_extract.py` | Paper page selection, question/answer state classification, targeted redactions, PDF generation. |
| `validate_final.py` | First extraction QA: qpdf, page counts, question/option checks, missing source spans, answer markers, geometry and pixel diffs. |
| `second_audit_inventory.py` | Independent source-page text/layout inventory and scan outputs. |
| `second_audit_ocr.py` | Independent sparse-page OCR pass. |
| `second_audit_renders.py` | 20 source-page overview sheets and individual 150-dpi renders/contact sheets for the 32 outputs. |
| `second_audit_verify.py` | Independent output verifier: questions/options/choices, answer markers, geometry, images, masks, missing text, residual pixels, pixel differences. |

Typical historical invocations recorded include:

```bash
python .nodia_work/scripts/analyze_source.py
python .nodia_work/scripts/ocr_sparse_pages.py
python .nodia_work/scripts/render_overview.py
python .nodia_work/scripts/classify_extract.py
python .nodia_work/scripts/validate_final.py
python .nodia_work/scripts/second_audit_inventory.py
python .nodia_work/scripts/second_audit_ocr.py
python .nodia_work/scripts/second_audit_renders.py
python .nodia_work/scripts/second_audit_verify.py
qpdf --check extracted_papers/Paper_01.pdf
qpdf --check extracted_papers/Paper_02.pdf
```

**Do not rerun the extraction scripts in a new repository merely because the scripts are not tracked.** The output files already exist and have been validated. A re-run should occur only if there is a concrete, verified issue, after inspecting the current repository and preserving all existing files.

### 6.7 Visual review and ambiguous cases

- First QA rendered all 32 outputs and reviewed them in contact sheets, with ambiguous/mixed pages and equation-limit edges inspected at higher resolution against the source.
- Independent audit built 20 source contact sheets (30 pages per sheet; final sheet 29 pages), visually reviewed all pages 1–599, and rendered all 32 outputs individually at 150 dpi for page-by-page review.
- OCR and keyword matches were checked contextually; isolated words such as `answer`, `sample`, `practice`, `previous year`, and bold `or` were not used as automatic classification decisions.
- Page 31 right-column solution text, source p32 solution-only continuation, and source p37 advertisement were explicitly investigated as boundary cases.

---

## 7. Quality assurance and validation history

### 7.1 First extraction validation (recorded in `extraction_report.md`)

Checks reported as passing:

- Source download size/MD5 matched Drive metadata.
- Source opened in PyMuPDF and all 599 pages were accounted for; qpdf found no syntax/stream encoding errors.
- Sparse source pages were OCR-reviewed with `eng+hin`; 26 pages, zero errors.
- Both outputs opened as PDFs and passed `qpdf --check`.
- Page counts: 15 and 17; page size/orientation match kept source pages.
- Q1–Q38 are present in each paper; no missing question spans were reported by the extraction validator.
- All 20 MCQ/assertion items in each paper have four option labels.
- Internal-choice markers were retained: 10 in Paper_01 and 9 in Paper_02.
- Question diagrams and images were checked; equations, tables, passages, headers, footers, and page geometry were visually compared.
- Answer indicators (`Sol :`, `correct option`, `answer key`) and residual solution spans: zero reported.
- All 32 output pages received visual review.
- Pixel changes outside nominal answer masks were investigated; no question loss was found.

First report's summary: 2 complete paper instances identified and extracted; 32 output pages; 0 duplicate instances found; unresolved boundary issues: none.

### 7.2 Second independent audit — reason and scope

The user requested a second independent review specifically to make sure the initial classification had not missed other sample/model/practice/previous-year/complete papers and that no answers or solution fragments remained. It was also to verify missing/truncated questions, options, diagrams, equations, passages, and paper boundaries. The second agent did not restart extraction and did not overwrite the already-validated PDFs.

Second audit recorded results:

- All 599 source pages re-examined by fresh text inventory, keyword/heading checks, 20 visual contact sheets, contextual review, and an independent 26-page OCR pass.
- All 32 output pages individually rendered and reviewed.
- No additional complete paper found.
- Q1–Q38 present in both PDFs; zero missing questions or duplicate question anchors.
- 20/20 MCQs in each PDF have A–D/a–d options.
- Internal choices retained (Paper_01 10; Paper_02 9).
- Zero residual `Sol :`, correct-option, answer-key, or `Ans` markers; no hidden white text, annotations, or embedded files.
- No missing source question spans outside answer masks.
- No residual non-white pixels inside strict answer masks.
- All question images outside answer masks preserved; six images inside answer masks were verified as solution-only graphics and legitimately removed.
- All page dimensions and orientations match source kept pages.
- No verified defect or correction required; PDFs remain unchanged.

### 7.3 Flags investigated and resolved as benign

The first run of the independent verifier reported two overly strict checks. Both were investigated and the verifier criteria corrected; they were not PDF defects:

1. **Unequal source/output image counts:** the six absent images were inside answer masks and visually identified as solution-only graphs/diagrams. All question images outside masks were preserved. Requiring exact image-count equality was inappropriate.
2. **One gray residual pixel on Paper_02 output p10/source p43:** it was only in the 1-pixel padding tolerance around the answer mask and was part of the preserved Q27(b) integral. The strict unpadded answer-mask check found zero residual pixels.

Other benign image/pixel observations:

- Paper_02 source page 36 / output p4 had 35 changed pixels, max channel difference 65, a minor anti-aliasing edge difference on preserved question material.
- Paper_02 source page 39 / output p6 had 16 pixels outside the nominal mask corresponding to removed answer text descenders from “Thus (a) is correct option.” Context review showed no question content lost.
- Paper_01 had zero pixel differences outside masks.

Removed solution-only images:

| Paper | Source page | Image content |
|---|---:|---|
| Paper_01 | 9 | Worked-solution graph for Q10 area problem. |
| Paper_01 | 26 | Worked-solution graph for Q30 linear programming. |
| Paper_02 | 39 | Solution duplicate graph for Q18; the question's shaded-region graph remains. |
| Paper_02 | 44 | Solution graph for Q29 absolute-value area. |
| Paper_02 | 48 | Solution diagram for Q35. |
| Paper_02 | 50 | Solution diagram for Q38. |

### 7.4 Source-inherent oddities preserved

These were noted as source content, not extraction defects, and were not silently corrected:

- split options across pages (Paper_01 Q15/Q17 and Paper_02 Q18);
- garbled probability notation in Paper_02 Q7;
- wording “angel” (Q23), “fined” (Q29), “radio” (Q30), repeated “are 180” (Q32);
- Paper_02 Q37 number printed alone.

### 7.5 Detailed audit report is authoritative

Read `extracted_papers/second_audit_report.md` directly for the complete page-by-page result table, source exclusion rationale, question/option/internal-choice data, checks, and limitations. It has 356 lines in the inspected local checkout. The extraction report is the corresponding source for the original pipeline and first QA.

There is a local `.nodia_work/second_audit/progress.json` whose `pending` array was not refreshed after the independent verification/report/commit finished. It still lists audit items as pending. **That file is stale.** For final second-audit status, use the committed `second_audit_report.md`, the final independent-verifier JSON, and Git history—not the stale progress array. The transient verifier artifacts are excluded from Git.

---

## 8. Git history and current repository state

### 8.1 Verified local state at handoff creation

The following commands were run in `/home/user` immediately before writing this handoff:

```text
pwd                         /home/user
git rev-parse --show-toplevel /home/user
git branch --show-current   main
git status --short --branch  ## main
git remote -v               (no output)
```

Local history:

```text
51cde6e (HEAD -> main) docs: add independent second audit report
ff7bf1b feat: extract all Nodia sample question papers into separate PDFs
```

Full commit IDs:

| Commit | Message | Files included |
|---|---|---|
| `ff7bf1bed7eb11a7ff200d9039d09866411346ce` | `feat: extract all Nodia sample question papers into separate PDFs` | `Paper_01.pdf`, `Paper_02.pdf`, `extraction_report.md` only. |
| `51cde6e13e1d8007e560e39a679938845d7c4773` | `docs: add independent second audit report` | `second_audit_report.md` only. |

Commit dates in this local environment are 2026-10-31. Author configured as `Arena Agent <arena-agent@localhost>`; this is a local Git identity, not a GitHub account assertion.

**Remote state:** none configured in this workspace; no push was attempted. These commits are known local commits only and are not necessarily present in the user's actual GitHub repository.

### 8.2 Working-tree status with this handoff file

At inspection time, before creation of `PROJECT_HANDOFF_NODIA_EXTRACTION.md`, the working tree was clean (`## main`). This handoff is specifically not to be committed now. Therefore, after creation, the expected status is:

```text
## main
?? PROJECT_HANDOFF_NODIA_EXTRACTION.md
```

If the status differs, inspect why. Do not stage or commit automatically.

### 8.3 GitHub synchronization caveat

No GitHub repository URL, remote, branch relationship, or actual remote contents is established by this local workspace. The user intends to connect a new agent to the actual repository. The new agent must determine whether the two local commit histories and four tracked deliverables are present in that connected repository. It must report exactly what it observes and carefully recover missing files/commits without discarding unrelated history.

---

## 9. Current file and directory inventory

The table distinguishes tracked deliverables from local/excluded analysis evidence. File sizes and hashes below were checked in the inspected local workspace on 2026-10-31; re-check in a new session.

### 9.1 Deliverables tracked in local `main`

| File | Purpose | Expected / verified status |
|---|---|---|
| `extracted_papers/Paper_01.pdf` | 2026 question-only paper | Present, 15 pages, validated, tracked, unchanged during second audit. |
| `extracted_papers/Paper_02.pdf` | 2025 question-only paper | Present, 17 pages, validated, tracked, unchanged during second audit. |
| `extracted_papers/extraction_report.md` | Initial source, extraction-method, and QA report | Present, tracked, 113 lines, unchanged during second audit. |
| `extracted_papers/second_audit_report.md` | Independent source/output audit report | Present, tracked, 356 lines, committed in `51cde6e`. |
| `PROJECT_HANDOFF_NODIA_EXTRACTION.md` | New-session handoff (this document) | Created at repository root; intentionally not committed by the current task. Expected untracked. |

### 9.2 Local-only processing/QA evidence (excluded from Git)

`.nodia_work/` is listed in `.git/info/exclude`; its contents do not appear in `git ls-files` and may not travel with a GitHub clone. It contains:

| Path | Contents / relevance |
|---|---|
| `.nodia_work/source/CBSE 12th Mathematics.pdf` | Local downloaded source copy; 47,655,270 bytes; exact SHA-256 above. Do not add to Git or modify. |
| `.nodia_work/analysis/source_info.json` | Source metadata, counts, hash, PDF integrity/encryption notes. |
| `.nodia_work/analysis/page_summaries.json` | Per-page text/layout/font/image/drawing/geometry summaries for all 599 pages. |
| `.nodia_work/analysis/pages/0001.txt`–`0599.txt` | Full extracted source-page text inventory. |
| `.nodia_work/analysis/headings.txt`, `analysis.log` | Heading scan and execution log. |
| `.nodia_work/analysis/extraction_plan.json` | Per-paper page records, event/state classification, mask rectangles, source/output page map. |
| `.nodia_work/analysis/validation.json` | First validator output for both PDFs. |
| `.nodia_work/analysis/ocr/` | First sparse-page OCR JSON/text and summary. |
| `.nodia_work/qa/draft/`, `draft_renders/` | Draft PDFs and renders from iteration; not deliverables. |
| `.nodia_work/qa/final/` | Final 130-dpi renders/contact sheets and validation render evidence. |
| `.nodia_work/qa/diff/` | Difference maps/crops for boundary/pixel review. |
| `.nodia_work/qa/source_overview/` | Source overview sheets and selected renders. |
| `.nodia_work/scripts/` | Nine local analysis/extraction/validation scripts listed above. |
| `.nodia_work/second_audit/inventory.json`, `inventory/0001.txt`–`0599.txt` | Independent source inventory and individual page text files. |
| `.nodia_work/second_audit/keyword_hits.md` | Context list of relevant keyword hits. |
| `.nodia_work/second_audit/ocr/`, `ocr_summary.json` | Independent 26-page OCR pass; 0 errors. |
| `.nodia_work/second_audit/renders/` | 20 source sheets, 32 output PNGs, and 4 output contact sheets. |
| `.nodia_work/second_audit/context/` | Focus crops used to resolve benign pixel/image flags. |
| `.nodia_work/second_audit/verification.json` | Final independent verifier results; both papers PASS. |
| `.nodia_work/second_audit/progress.json` | Progress log, but its pending list is stale after completion; do not treat as current final status. |

Git excludes also include `.cache/` and `.sudo_as_admin_successful` in `.git/info/exclude`; these are environment artifacts and not deliverables.

---

## 10. Instructions for the next AI agent

### Step 1 — Read this document completely

Do not skip the requirements, Drive restrictions, repository-state caveats, or synchronization instructions. Read both committed reports if present. This handoff is a historical map, not a license to ignore current Git state.

### Step 2 — Connect to the actual repository

The user will connect the new agent to the actual GitHub repository. Do not assume the new agent shares `/home/user`, `.nodia_work/`, Drive permissions, or local Git objects from this session.

Do not invent a repository URL or remote. Use the connected repository context provided by the platform/user and verify it directly.

### Step 3 — Inspect before changing anything

Run non-destructive inspection first. At minimum:

```bash
pwd
git rev-parse --show-toplevel
git branch --show-current
git status --short --branch
git log --oneline --decorate --all -20
git remote -v
git ls-files
find . -maxdepth 3 -type f -print | sort
```

Check whether `extracted_papers/` exists and inspect each PDF/report. Check file sizes and hashes if possible. Use `pdfinfo`/PyMuPDF and `qpdf --check` only if available; report exact availability/errors. Do not reset or clean the working tree to make it match this handoff.

### Step 4 — Recover existing work; do not repeat extraction unnecessarily

- Do not rerun the extraction just because the source or temporary scripts are absent from the new clone.
- Do not overwrite or recreate validated output PDFs without a concrete, verified defect.
- Preserve commits, branches, uncommitted changes, and unrelated repository content.
- Keep the original file names and papers' contents intact.
- Read `extraction_report.md` and `second_audit_report.md` directly; those contain primary project evidence.

### Step 5 — Determine whether the local deliverables/commits are synchronized

The previous local repository had two commits but **no remote**. In the connected actual repository, establish:

- whether the four tracked deliverables are already present;
- whether the two commit IDs or equivalent content/history are present;
- whether the current branch has newer work, diverged history, or unrelated changes;
- whether the handoff file itself has been uploaded/committed by the user.

If anything is missing, recover it through the safest repository-supported path, respecting existing branch protection/history. Do not force-push, overwrite the remote branch, invent an origin, or assume that matching filenames imply matching validated contents. Compare hashes/content where appropriate. If synchronization needs a user-selected remote/branch or cannot be safely performed, report the exact blocker and ask only for information truly necessary.

### Step 6 — Check the original source only if needed

The source copy was local under `.nodia_work/` in the previous workspace, but it is untracked/excluded. Use read-only Drive access in the new session only if reinspection is required and only if the user has provided authorized access there. Do not assume the permissions persist. Never make Drive changes or access unrelated files.

### Step 7 — Continue only unfinished work

Extraction and the independent audit were reported complete. No PDF correction is pending. Continue only tasks that are actually unfinished in the current repository (for example, synchronizing deliverables to the user's GitHub repository if requested/authorized, or checking a genuinely missing file). If a new defect is discovered, preserve originals and obtain/verbalize concrete evidence before changing a PDF.

### Step 8 — Retain all original requirements

Question-only output, formatting preservation, multilingual/math/diagram/table fidelity, full-document coverage, duplicate retention, and strict Drive read-only rules remain binding for any future correction or extension.

### Step 9 — Report actual state, not assumptions

The next agent's final response must state:

1. Whether the actual repository was connected successfully (and what was actually inspectable).
2. Whether `Paper_01.pdf` and `Paper_02.pdf` exist in that repository and their current validation/hash status.
3. Whether `extraction_report.md` and `second_audit_report.md` exist.
4. Whether the two commits were found, recovered, or synchronized; provide hashes and branch details.
5. Whether the working tree is clean (including any handoff-file change).
6. Whether GitHub synchronization/push truly succeeded, or if it remains local/blocked; never claim a push without evidence.
7. Any missing deliverable, error, or unresolved question, with exact command/error and next required action.

---

## 11. Lessons learned and warnings

1. **Do not assume whole-page splitting is sufficient.** Questions and solutions share pages and even text blocks/lines; classify per column and at span/line level where needed.
2. **Do not rely only on keywords to detect or remove answers.** A question can contain “answer,” “hence,” or a source citation; classify context and visually inspect.
3. **Preserve original PDF geometry and appearance.** Page-level copying plus targeted redaction retained typography and diagrams better than reflow or rasterization. Whitespace where solutions were deleted is intentional.
4. **Inspect every page, not just representative pages.** The source had 599 pages; the outputs had 32. Audits used full page inventory, source contact sheets, and individual output review.
5. **Retain duplicates.** The source had no duplicate complete papers, but future duplicate instances must not be discarded.
6. **Do not mistake a solved question bank for a complete sample paper.** Chapter-organized questions and interleaved solutions are not full examination papers without complete paper structure/context.
7. **Never claim local commits are pushed to GitHub.** This workspace has no remote. The new agent must verify the actual connected repository and push status.
8. **Never overwrite validated deliverables unnecessarily.** No second-audit correction was verified; the PDFs were left unchanged.
9. **Inspect Git status before staging or committing.** Stage only intended files and review staged names/diff before commit.
10. **Never modify the original Google Drive PDF.** Drive is read-only, solely for source access; no uploads, edits, moves, renames, deletions, or Drive organization.
11. A strict source/output image-count equality check is invalid when solution-only images are deliberately removed. Compare image location/context to answer masks.
12. A one-pixel padding zone around a mask can capture preserved question glyphs. Inspect strict masks and pixel crops before calling a residual-answer defect.
13. A bold `or` is not automatically a question boundary; internal choices and alternative solution methods must be disambiguated using column/page state and visual context.
14. PDF block boundaries can combine the end of a question with a `Sol :` label; inspect spans and their coordinates, not only blocks.
15. Do not “fix” source typos or layout oddities while extracting unless the user explicitly requests content correction; retain original content faithfully.

---

## 12. Known limitations, unknowns, and pending items

### Confirmed complete in the inspected local project

- Source downloaded and validated in original session.
- All 599 source pages analyzed and, during the second audit, visually reviewed as source contact sheets.
- Two complete papers extracted into two question-only PDFs.
- All 32 outputs visually reviewed; Q1–Q38, options, choices, diagrams/passages/tables checked.
- First validation and independent second audit completed.
- Both reports present and committed.
- No PDF corrections identified.

### Unknown or not transferable by assumption

- Actual GitHub repository URL and current remote branch contents.
- Whether local commits `ff7bf1b...` and `51cde6e...` already exist in the user's actual GitHub repository.
- Whether a new agent session retains any Google Drive connector permissions.
- Whether the local-only `.nodia_work/` artifacts or source PDF will exist in the new clone.
- Any repository changes made after this handoff was created.

### Pending task for the next session

The only expected next-session work is repository reconciliation/reporting: inspect the user-connected repository and determine whether the validated PDFs and reports, and the two local commits, are present/synchronized. Do not redo extraction or audit unless the current repository reveals a verified problem.

---

## 13. Final verification of this handoff file

After creation, verify with commands such as:

```bash
ls -l PROJECT_HANDOFF_NODIA_EXTRACTION.md
wc -l -c PROJECT_HANDOFF_NODIA_EXTRACTION.md
sed -n '1,40p' PROJECT_HANDOFF_NODIA_EXTRACTION.md
grep -n '^## ' PROJECT_HANDOFF_NODIA_EXTRACTION.md
git status --short --branch
sha256sum extracted_papers/Paper_01.pdf extracted_papers/Paper_02.pdf
```

Expected critical headings include:

- `## 2. Original objective and project scope`
- `## 3. Source document and verified identity`
- `## 4. Full-document analysis and paper classification`
- `## 6. Technical implementation`
- `## 7. Quality assurance and validation history`
- `## 8. Git history and current repository state`
- `## 10. Instructions for the next AI agent`
- `## 11. Lessons learned and warnings`
- `## 12. Known limitations, unknowns, and pending items`

This handoff is intentionally left uncommitted so the user can download it and decide how to add it to their actual GitHub repository. Do not upload it to Google Drive.
