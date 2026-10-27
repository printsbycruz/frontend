# Milestone 2 frontend validation

## Passed

- JavaScript syntax: `node --check m2/review.js`.
- Automated DOM interaction checks using Node 24.22.1 and jsdom 30.1.3.
- Reviewed-value export retains the original record, applies edits, and keeps unknown pricing as an empty array.
- Unresolved conflicts and unconfirmed source review block export.
- Event date ordering, real calendar dates, edition-year matching, malformed arrays, and negative prices are checked.
- Rejection requires a reason and exports no approved values.
- Imported HTML is displayed as text; javascript: source links are not made clickable.
- Wrapper status controls decision availability, even when raw_payload contains a different status; missing status disables decisions.
- Draft edits survive candidate switching; clearing removes the session.
- Malformed candidate structures are rejected.

Reproduce the DOM checks with Node 24+, `npm install`, then `npm test`. Runtime operation of the page does not require Node or dependencies. The test harness stubs file-download browser APIs and calls the importer directly; it does not exercise the OS file chooser or actual download handling.

## Not verified

- Visual rendering, mobile overflow, native file import/download, and full browser behavior. Playwright was available, but Chromium was absent and its installation download failed. These require manual browser checks.
- Live extraction, authenticated API loading, schema conformance, CSRF, authorization, backend error handling, persisted approval/rejection, or integrated database behavior. The necessary teammate source and API documentation were not included.

These checks establish local frontend behavior only, not readiness of the integrated platform.
