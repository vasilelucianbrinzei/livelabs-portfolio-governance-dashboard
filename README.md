# LiveLabs Analytics

LiveLabs Analytics is a static governance dashboard for reviewing the Oracle LiveLabs workshop portfolio. It helps portfolio owners identify high-performing content, workshops and sprints that need review, and content that may be ready for retirement after replacement validation.

The repository is designed for GitHub Pages. The checked-in HTML and JSON files are the publishable dashboard bundle; raw workbook and CSV source files stay local in `dataset/` and are intentionally ignored.

## What This Project Contains

- `index.html` is the published dashboard page.
- `dashboard_tables.json`, `dashboard_payload.json`, `wms_canonical.json`, `replacement_similarity.json`, and `workshop_updates.json` provide the main data payloads used by the dashboard.
- `data/` contains the split JSON tables that back the dashboard sections and row-level details.
- `assets/` and `content/` contain supporting static files used by the page.
- `.github/workflows/pages.yml` publishes the static site through GitHub Pages.
- `dataset/` is a local-only source-data folder for raw Excel, CSV, and QA material. It should not be committed.
- `QA_TEST_PLAN.md` is a local-only checklist for validating dashboard changes before publication.

## How To Read The Dashboard

Start at the summary cards at the top of the page. They highlight the leading top performer, highest-risk item, and retire-now candidate across workshops and sprints.

Use the Contents section to move between the main views:

- `Top Performers` shows workshops and sprints with the strongest demand and freshness signals.
- `At-Risk Content` shows stale or low-demand content that should be reviewed before it moves closer to retirement.
- `Retire-Now Content` shows items with stronger evidence for retirement, usually after replacement evidence is available.
- `Replacement Suggestions` lists candidate successors and similarity evidence.
- `Disabled Content` keeps already disabled workshops and sprints visible for audit context.
- `Portfolio Stats` summarizes source coverage, scoring inputs, governance signals, and data-quality notes.

Most tables support sorting, filtering, and expandable rows. Open a row to review identifiers, source evidence, ownership fields, update dates, replacement details, and the reason the item appears in that view.

## How To Use It Locally

Open `index.html` directly in a browser for a quick review, or serve the folder locally when checking browser behavior:

```powershell
cd path\to\LiveLabs_Portfolio_Governance_Dashboard
python -m http.server 8000
```

Then open `http://127.0.0.1:8000/`.

Before publishing changes, verify:

- the page title and main heading read `LiveLabs Analytics`;
- the dashboard loads with HTTP 200 when served locally;
- the key JSON payloads under the repository root and `data/` are present;
- raw Excel and CSV files remain under ignored `dataset/` paths;
- local planning files such as `QA_TEST_PLAN.md` are not staged.

## Publishing Notes

Commit only the static dashboard assets that GitHub Pages needs: the HTML page, checked-in JSON payloads, content assets, workflow files, and documentation. Keep raw source exports, local QA notes, temporary debug output, and generated scratch bundles out of Git.

Use `git status --short --ignored` to confirm ignored local files before staging. Use `git diff --check` before committing to catch whitespace problems in tracked files.
