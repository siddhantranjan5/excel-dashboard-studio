# Excel to Dashboard Studio

A browser-based analytics tool that turns Excel workbooks and CSV files into interactive dashboards. Explore worksheets, profile and clean data, detect relationships between tables, create calculated columns and measures, and generate KPI cards and decision-oriented charts—all from a single HTML page.

> **Privacy note:** Workbook data is processed in your browser by the app; it is not intentionally uploaded to an application backend. The page does load third-party JavaScript libraries from CDNs, so an internet connection is required for those dependencies. Do not treat this as a security-audited environment for highly sensitive data.

## Features

- **Import data:** `.xlsx`, `.xls`, `.xlsm`, and `.csv` files.
- **Multi-worksheet exploration:** Preview rows, inspect columns, inferred data types, completeness, unique values, and basic column profiles.
- **Data cleaning:** Rename columns; convert values to numbers, dates, or text; normalize text; fill blanks; cap outliers using an IQR rule; remove blank rows, duplicates, and total/subtotal rows.
- **Relationship detection:** Suggest links between worksheets based on column names and value overlap, with controls to enable, remove, or add relationships.
- **Calculated columns:** Date parts, date differences, concatenation, numeric arithmetic, and low/medium/high bands.
- **Measure suggestions:** Common aggregations and counts, plus editable custom measures.
- **Power BI support:** Shows DAX-style formulas for calculated columns and measures that can be adapted for Power BI.
- **Interactive dashboard:** Four or five KPI cards, category ranking, time trends, category share, Pareto-style analysis, key insights, and detail rows.
- **Filters and drill-down:** Filter the dashboard from category controls and chart selections.
- **Presentation and export:** Switchable color themes, CSV export of the filtered model, and browser print / Save as PDF.

## Quick start

### Option 1 — Open locally

1. Download or clone this repository.
2. Open `index.html` in a modern browser.
3. Select **Try with sample data** to explore the app, or upload an Excel/CSV file.
4. Follow the workflow: **Upload → Explore → Relationships → Columns & Measures → Design → Dashboard**.

Because the application is a static HTML file, there is no build step or backend server.

### Option 2 — Run with a local static server

Some browser setups behave more consistently when the file is served over HTTP. From the repository folder, run:

```bash
python -m http.server 8000
```

Then visit [http://localhost:8000](http://localhost:8000).

### Option 3 — Publish with GitHub Pages

1. Create a new GitHub repository.
2. Upload the repository files, keeping `index.html` at the repository root.
3. Open **Settings → Pages**.
4. Under the build/deployment source, select **Deploy from a branch**.
5. Select your default branch (usually `main`) and the root (`/`) folder, then save.
6. Wait for GitHub Pages to publish the site. The public URL will be shown in the Pages settings.

GitHub changes its interface from time to time; follow the current labels shown in your repository settings.

## How to use

1. **Upload:** Choose an Excel workbook or CSV. You can also load the built-in sample dataset.
2. **Explore and clean:** Review each sheet and column profile. Apply cleaning operations carefully; changes affect the in-memory data used by the dashboard.
3. **Relationships:** Review automatically detected joins. Confirm that the key columns are correct, and manually add or remove links when necessary.
4. **Columns & measures:** Add suggested or custom calculations and measures. Review generated formulas before reusing them elsewhere.
5. **Design:** Choose a dashboard title, currency display, four or five KPIs, and a visual theme.
6. **Dashboard:** Use the filters and chart interactions to explore the data. Export the filtered model to CSV or print/save the dashboard as PDF.

## Technology

- HTML5
- CSS (responsive layout and theme variables)
- Vanilla JavaScript
- [SheetJS / xlsx](https://github.com/SheetJS/sheetjs) for spreadsheet parsing
- [Chart.js](https://www.chartjs.org/) for charts

The current HTML loads the libraries from CDN URLs. This keeps setup simple but means those URLs and the user's internet connection are runtime dependencies.

## Repository structure

```text
.
├── index.html          # Complete client-side application
├── README.md           # Project overview and usage instructions
├── LICENSE             # MIT license (update copyright holder if needed)
├── CONTRIBUTING.md     # Contribution workflow and coding guidance
├── SECURITY.md         # Responsible disclosure and data-handling notes
├── .gitignore          # Common local/editor files to exclude
└── CHANGELOG.md        # Initial project release notes
```

## Important behavior and limitations

Please review these before using the dashboard for business decisions:

- **Heuristic type detection:** Column types and key fields are inferred from observed values and column names. Review them before relying on results.
- **Relationship detection is heuristic:** Matching names and overlapping values do not prove that a relationship is correct. The join model can use the first row for duplicate lookup keys and reports join mismatches; verify keys and cardinality yourself.
- **Disconnected worksheets:** Only worksheets connected to the main table through enabled relationships are included in the merged model. Unlinked sheets may not contribute to dashboard visuals.
- **Join shape:** The app builds a flattened model around the largest worksheet. This is not a full relational query engine and may not represent every many-to-many or complex relationship correctly.
- **Cleaning is in-memory:** There is no persistent project save/load workflow. Reloading the page or uploading a new file should be treated as a fresh session.
- **Large workbooks:** All processing occurs in the browser. Large files can be slow or use substantial memory.
- **Date and number parsing:** Locale-specific date formats, ambiguous dates, currencies, percentages, and unusual spreadsheet layouts should be checked after import.
- **DAX output needs review:** Generated formulas are suggestions. Table names, relationship requirements, row context, aggregation behavior, and the target Power BI model can require changes.
- **Insight wording is heuristic:** Automated summaries describe patterns in the imported data; they do not establish causation or guarantee a business recommendation is appropriate.
- **External dependencies:** SheetJS and Chart.js are loaded from third-party CDNs. The app needs network access for these libraries, and upstream availability/version changes may affect operation.
- **No formal test suite is included:** Run through the manual checklist below after making changes or before a public release.

## Manual smoke-test checklist

- [ ] Open the app and confirm the upload screen renders.
- [ ] Load the built-in sample data and confirm three worksheets appear.
- [ ] Upload a small `.xlsx` workbook with multiple worksheets.
- [ ] Upload a `.csv` file.
- [ ] Change a detected header row and verify the preview changes.
- [ ] Rename a column and test at least one cleaning operation.
- [ ] Review a detected relationship; add or remove a relationship.
- [ ] Add a calculated column and a measure.
- [ ] Generate a dashboard with four and then five KPIs.
- [ ] Change a chart selector and apply/remove a filter.
- [ ] Export CSV and confirm it opens correctly in a spreadsheet editor.
- [ ] Use Print / PDF and check the resulting layout.
- [ ] Test a workbook with missing values, duplicate keys, and a date column.
- [ ] Test a larger file and note browser performance.

## Privacy and security

- The application is designed to read the selected file in the browser; this repository does not provide an application backend or server-side data store.
- Third-party CDN scripts are loaded when the page opens. For a stricter offline or enterprise deployment, vendor approved library files locally, pin and audit their versions, and review their licenses and security advisories.
- Avoid uploading confidential, regulated, or personal data unless your organization has approved the tool and deployment.
- CSV export includes a basic guard against formula-like cell values, but exports should still be treated as untrusted input and reviewed before being opened in downstream systems.
- See [SECURITY.md](SECURITY.md) for reporting guidance.

## Contributing

Bug reports, usability improvements, documentation fixes, and carefully scoped feature contributions are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) first.

## License

This project is distributed under the MIT License. See [LICENSE](LICENSE). If you are not the sole copyright owner of the source, confirm that you have the right to publish it under this license before making the repository public.
