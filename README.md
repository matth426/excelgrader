# Answer Key Grader

A strict, browser-based tool that checks a submitted `.xlsx` file against an answer key. Everything runs client-side — no server, no upload, no data ever leaves the browser.

Open `grade_xlsx.html` in any modern browser and drop in two files: an answer key and a submission.

## How scoring works

The tool checks every cell in the answer key against the matching cell in the submission and produces a strict score: **0, 25, 50, 75, or 100**.

| Score | Condition |
|------:|-----------|
| 100 | Every expected cell matches exactly |
| 75  | ≥ 90% of expected cells match |
| 50  | ≥ 70% of expected cells match |
| 25  | ≥ 40% of expected cells match |
| 0   | < 40% match, or the file fails to open |

If a required sheet is missing entirely, the score is capped (50 max, dropping further as the match ratio falls).

By default the comparison is exact: a stray space, a different case, or a rounded number counts as a mismatch. Three options loosen specific parts of that on request — everything else stays strict.

## Options

- **Numeric tolerance** — allow small floating-point differences (e.g. `0.01`) instead of requiring exact equality.
- **Count unexpected extra sheets against the score** — off by default, so extra sheets in the submission are ignored.
- **Ignore sheet names** — match sheets by their position in the workbook (1st vs. 1st, 2nd vs. 2nd) instead of requiring identical names.
- **Ignore row order** — a row counts as correct if it exists *anywhere* in the sheet, not just at the same position. Every cell in the row must still match exactly, and each submission row can only satisfy one expected row (so dropped duplicates still get caught).

## Reading the results

- A stamped score badge (0–100) with the overall match percentage.
- Flags for any missing or unexpected sheets.
- A per-sheet breakdown — click a row to expand the specific mismatches (which cell, or which whole row, didn't match).
- A **Download full report (.txt)** link with the complete, unabbreviated results for record-keeping.

## Tech

Single self-contained HTML file — no build step, no install.

- Vanilla HTML/CSS/JavaScript
- [SheetJS](https://sheetjs.com/) (loaded from a CDN) for parsing `.xlsx` files in the browser

## Limitations

- Reads `.xlsx` only.
- Grading logic runs on the visible grid of each sheet (values, not formulas or formatting).
- Intended for one submission at a time — for batch grading many submissions, a script-based version would be a better fit.

## License

Add a license of your choice (MIT is a common pick for a small utility like this).
