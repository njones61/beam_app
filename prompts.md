# Prompts Log

A record of requests and changes made to this project.

## Format

For each request, record:
- **What was asked**: Brief description of the user's request
- **What changed**: Files created, modified, or deleted
- **Status**: Whether it worked or needs follow-up

---

## Entry 1: Initial Project Structure Setup

**What was asked:** Set up the folders for this project, a single-file web app. AGENTS.md, spec.md, prompts.md, and index.html go at the top level, because GitHub Pages needs index.html there. Create numbered folders for everything else: 00_planning for notes and sketches, 01_data for data files, 02_validation for hand calculations and test cases, and 03_output for screenshots and exported results. Put a short README.md in each folder. Then describe this layout in AGENTS.md, with a rule to save new files in the right folder.

**What changed:**
- Created 4 numbered folders: `00_planning/`, `01_data/`, `02_validation/`, `03_output/`
- Created README.md in each folder describing its purpose
- Created `spec.md` (specification file)
- Created `prompts.md` (this log file)
- Created `index.html` (minimal single-file web app starter)
- Updated `AGENTS.md` with folder layout documentation and filing rules

**Status:** ✅ Completed successfully

## Entry 2: Review of spec.md

**What was asked:** Review spec.md (initial plan), give suggestions and recommendations, including real beam properties. Don't write code yet.

**What changed:** No project files changed except this log entry. Review delivered in chat: hand-checked the validation example (M = 50.0 kip-ft, deflection 0.609 in, both correct), and recommended additions for section property data, allowable stress rules, shear check, deflection limits, load definitions, validation cases, and scope.

**Status:** ✅ Completed (review only)

## Entry 3: Spec decisions folded into spec.md

**What was asked:** Answers to my open questions: steel grade selectable; recommend lumber species; partial uniform loads yes; deflection check on live load only; self-weight toggle OK.

**What changed:** Rewrote `spec.md` with a design basis section (ASD, braced/compact assumptions, units), dead/live tags on loads, partial uniform loads, selectable steel grade (A992/A36/custom Fy), shear check, live-only L/360 deflection (cantilever L = 2x length), self-weight toggle (default off), a Data section (AISC W-shapes, NDS lumber: DF-L, Southern Pine, Hem-Fir, SPF, all No. 2), expanded validation cases, and an explicit out-of-scope list. No code written.

**Status:** ✅ Completed (spec only)

## Entry 4: Section data (steel) and lumber deferred

**What was asked:** "ok" to start on the data; then, if lumber data can't be found, make up 20-30 samples; then "taking too long, skip lumber?" (confirmed: skip lumber for now, steel only, update spec).

**What changed:**
- Created `01_data/steel_w_shapes.csv`: 174 W8-W24 shapes (designation, weight, A, d, bf, tw, tf, Ix, Sx, Zx) generated from the AISC Shapes Database v15.0 CSV mirror (github.com/ambaker1/aisc-csv). AISC's own site blocks downloads. Spot-checked W12X26: Ix 204, Sx 33.4 (matches spec).
- Started a research agent for NDS lumber values; it was slow, so I asked it to wrap up. Its results were not used.
- Updated `spec.md`: removed lumber from inputs, calculations, data and validation; added a steel data source note; listed lumber and other shapes as deferred.

**Status:** ✅ Steel data done. Lumber deferred. Hand-calculation validation cases in `02_validation/` not yet written. No app code written.

## Entry 5: Build the app

**What was asked:** "no. let's see the app" (skip the validation hand calcs; build it).

**What changed:**
- Replaced the placeholder `index.html` with the full single-file app: inputs (support, span, W-shape dropdown from 174 embedded AISC shapes, A992/A36/custom Fy, point and partial-uniform loads tagged dead/live, self-weight toggle, deflection limit), exact singularity-function analysis for reactions/V/M/deflection, bending/shear/live-load-deflection checks with ratios and pass/fail, and an SVG beam sketch with shear, moment and deflection diagrams on a shared x-axis with a hover readout.
- Saved `03_output/example_beam_screenshot.png` (the opening example).
- Lumber is still deferred (a research agent did return sourced NDS values; not used, per your decision).

**Status:** ✅ Works. Core math checked in Node against closed-form cases (spec example M = 50.0 kip-ft, deflection 0.609 in; midspan and off-center point loads; cantilever tip and UDL; partial UDL; superposition; dead/live split; self-weight; 2L cantilever limit), all passing. Checked in the browser: example, cantilever with mixed loads, input errors, grade switch, hover, mobile width. The test cases are not yet saved in `02_validation/`.

## Entry 6: Cross-section under the beam selector

**What was asked:** Plot a cross section of the beam under the beam selector.

**What changed:**
- `index.html`: added a to-scale SVG W-shape cross-section (flanges and web from bf, tf, tw, d; fillets ignored) directly under the shape dropdown, with d, bf, tf, tw labels and a dashed x-x axis. It redraws whenever the shape changes and scales to the sidebar width.
- `spec.md`: noted the cross-section in the Section input.

**Status:** ✅ Works. Checked W12x26 in the browser with no JS errors, and the shape switch for W14x873, W24x55 and W8x10 ran without errors. The preview window was too narrow to judge the large and small shapes visually, so only W12x26 was checked by eye.

## Entry 7: Scaled deflected shape on the top plot

**What was asked:** For the plot at the top, add deflection (scaled).

**What changed:**
- `index.html`: the beam sketch now draws the deflected shape (total load, from the same exact deflection function as the lower diagram) as a purple curve below the beam, with the maximum drawn at 34 px. The max deflection is labelled in inches on the curve, and the legend shows the exaggeration factor ("Deflected shape (scaled ×N)", N = vertical scale / horizontal scale, so it changes with chart width). The sketch panel is 30 px taller to fit it. With no loads, no curve is drawn.
- `spec.md`: noted the deflected shape in Outputs.

**Status:** ✅ Works. Checked in the browser for the simply supported example and a cantilever with mixed loads, and with no loads. No JS errors. Seen only at a narrow preview width.


## Entry 8: Auto-commit going forward

**What was asked:** Auto-commit my changes from now on.

**What changed:**
- Created the first git commit (`0600286`) with the whole project as it stands.
- `AGENTS.md`: added a Version control section (commit after each request, no push, don't redo edits I undo).
- Correction to entries 6 and 7: you undid the cross-section and the scaled deflected-shape edits (and the matching `spec.md` notes). `index.html` and `spec.md` are currently without them, and I did not re-add them. Those two entries describe changes that are not in the files.

**Status:** ✅ Done.

## Entry 9: Make the repo public

**What was asked:** Change my repo to public.

**What changed:** Set `njones61/beam_app` on GitHub from private to public with `gh repo edit` (https://github.com/njones61/beam_app). No project files changed besides this log entry.

**Status:** ✅ Done. Verified with `gh repo view`: visibility is PUBLIC.

