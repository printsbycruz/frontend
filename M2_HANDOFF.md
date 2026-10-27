# Milestone 2 — Jonathan Cruz frontend handoff

## Actual completion status

The original `index.html` is the Milestone 1 fictional-data prototype. Its local approve/reject actions do not update a database. It remains unchanged.

The new `m2/index.html` and `m2/review.js` implement a local candidate review workbench:

- Import a JSON candidate, or an array of up to 100 candidates (2 MB file limit).
- Accept fields directly on a record or inside its `raw_payload`, using `fields.<name>.value` as described in Gavin's handoff.
- Display extracted scalar/structured fields, field evidence, warnings, source records, summary, changes, and conflict alternatives using text rendering.
- Edit all supplied fields plus deadline and registration-price arrays. These array editors currently require valid JSON, not a row-based form.
- Treat absent price rows as unknown; never infer that registration is free.
- Require documented conflict decisions, confirmation that they were applied to the reviewed values, and source-review confirmation before exporting reviewed values.
- Validate core event dates/year, JSON array structure, and numeric nonnegative price amounts for recognized amount/price/value properties.
- Export a review request or a rejection request, retaining the complete original record. No local decision changes the official candidate status.
- Preserve edits while switching between imported candidates in the current tab. Reloading or clearing discards the session.

This is preparatory frontend work, NOT a live integrated workflow. `review_packet_version: frontend-draft-1` is a proposed handoff shape, not Gavin's or Joshua's verified API contract. It deliberately exports `backend_contract_verified: false`.

## Run

Extract the ZIP and open `m2/index.html` in a browser. No installation is needed for this workbench. For GitHub Pages, the M2 path is `/frontend/m2/` after these changes are actually committed/published. This package has not been pushed or published.

1. Load the fictional sample.
2. Expand warnings and evidence.
3. Review the location conflict. Enter `Atlanta` in Location.
4. Enter a conflict decision identifying the selected value, destination, and demo-a evidence; check that the edit was applied.
5. Confirm source review and export reviewed values.
6. Inspect the JSON: the reviewed location is Atlanta; the original value remains null. Empty registration_prices means unknown.
7. To test rejection, enter a reason and export a rejection request.

The fictional sample is not a live AI result or an exact reproduction of the official JSON schema.

## Files needed from Gavin

- `docs/AI_API.md`
- `examples/frontend-integration.mjs`
- `docs/ai-candidate.schema.json`
- A real pending candidate API response, with secrets removed.
- Current shared repository/branch and local setup instructions.

Without these files, endpoint paths, wrapper shapes, field metadata, supported conflict structures, and response errors cannot be verified. The importer currently recognizes direct records or records with raw_payload; list wrappers and other payload wrappers need an adapter based on the actual documentation. Existing status strings other than exactly `pending` intentionally disable decision export. Pending status is not authorization.

## Coordination with Joshua

Confirm the approval/rejection endpoint paths, HTTP methods, exact editable payload structure, authorization roles, CSRF bootstrap flow, and response shape. Confirm handling of candidate IDs, stale or already-reviewed records, edition selection, conflict decisions, and server validation errors.

Once confirmed, replace packet download with the documented authenticated workflow, load pending candidates using Gavin's integration module, and refresh status from server responses. Keep UI controls pending during requests and show failures without claiming success. Do not put Gemini keys in browser code.

Per Gavin's handoff, Joshua also needs to address approval transactionality, updating existing values, removing superseded deadlines, copying source URLs into child records, and separating completeness from verification. These backend responsibilities were not changed in this frontend package.

## What Ayo can test now

The local import/review/export interface and validation. Use the steps above plus malformed JSON, unknown prices, malicious text/URLs, multiple candidates, unresolved conflicts, invalid event dates, and mobile layouts.

Conflict resolution is a manual reviewer attestation in this workbench. It does not semantically prove that the chosen value was applied correctly. Price/deadline schema validation, required-field policies, role checks, and all authoritative approval rules still belong to the backend. The importer is a compatibility aid, not an implementation of the missing official schema.

## End-to-end acceptance gate (not completed)

1. Authenticate as an authorized reviewer on the team's Django app.
2. Extract one official conference URL using Gavin's service.
3. Load its pending candidate without hand-copying JSON.
4. Review and correct fields, deadlines, prices, and conflicts.
5. Submit through Joshua's authorized approval endpoint.
6. Verify the correct ConferenceEdition and child records in the database.
7. Reload and confirm persisted values and server status.
8. Verify rejection creates no official edition, unauthorized requests are denied, CSRF is enforced, and duplicate/stale approvals fail safely.

The team's Wednesday end-to-end target and Friday integrated demo depend on obtaining the missing files and completing this gate. This workbench alone does not establish that those targets are met.
