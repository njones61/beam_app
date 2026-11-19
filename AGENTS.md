# Project Structure

This is a single-file web app. The index.html and top-level documentation (spec.md, AGENTS.md, prompts.md) live at the root for GitHub Pages compatibility.

## Folder Organization

- **00_planning/** — Project notes, sketches, diagrams, and brainstorming
- **01_data/** — Data files, JSON, CSV, and reference datasets
- **02_validation/** — Hand calculations, test cases, and verification results
- **03_output/** — Screenshots, exported results, and deliverables

Each folder contains a README.md describing its purpose.

## Filing Rule

When creating new files:
1. If it's part of the app logic → `index.html` (single-file)
2. If it's a note or sketch → `00_planning/`
3. If it's input data → `01_data/`
4. If it's validation, calculation, or test case → `02_validation/`
5. If it's a screenshot or export → `03_output/`

## Logging

- After each request, add an entry to prompts.md: what I asked, what you changed, and whether it worked.

## Version control

- Auto-commit my changes: after finishing each request (and its prompts.md entry), commit everything changed in a single commit with a short, descriptive message. Don't push.
- If I undo or revert an edit, don't redo it unless I ask.