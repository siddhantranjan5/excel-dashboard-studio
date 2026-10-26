# Contributing

Thanks for considering a contribution to Excel to Dashboard Studio.

## Before you start

- Open an issue describing a bug, use case, or proposed improvement.
- For larger changes, discuss the approach before investing in implementation.
- Do not commit real customer workbooks, credentials, personal data, or confidential business data.

## Development workflow

1. Fork the repository and create a focused branch.
2. Keep the app usable as a static page unless a change explicitly proposes a different architecture.
3. Follow the existing HTML/CSS/vanilla JavaScript style where practical.
4. Escape user-provided values before inserting them into HTML.
5. Consider malformed workbooks, empty sheets, duplicate column names, missing values, and large inputs.
6. Run the manual smoke-test checklist in `README.md`.
7. Describe the change, test steps, known limitations, and any dependency changes in your pull request.

## Pull requests

- Keep changes focused and explain the user benefit.
- Include reproduction steps for bug fixes.
- Update documentation when behavior changes.
- Do not claim a feature is tested unless you have actually tested it.
