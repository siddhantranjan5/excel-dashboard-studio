# Security Policy

## Supported version

Security reports should identify the latest version on the repository's default branch. This is a small static web application and does not currently publish formal release tags or a supported-version matrix.

## Reporting a vulnerability

Please do not publish sensitive exploit details in a public issue. Contact the repository owner privately through the contact method listed on their GitHub profile, and include:

- A short description and potential impact
- Steps to reproduce
- Browser and operating-system details
- A suggested mitigation, if known

Do not include real or confidential spreadsheet data in a report.

## Data-handling notes

The app processes selected spreadsheet contents in the browser and has no application backend. It loads third-party JavaScript libraries from CDNs, which are part of the runtime trust boundary. Before using this tool with sensitive information or in a production environment, review the source code, vendor and audit dependencies, and apply your organization's security requirements.
