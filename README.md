# CCSE Conference Platform — Frontend

Frontend / UX: Jonathan Cruz

## Milestone 2 review workbench

Open `m2/index.html` after extracting the ZIP. Load the fictional sample or import candidate JSON, review evidence and conflicts, edit fields/deadlines/prices, and export a review or rejection request.

**Backend connection is pending. Exporting a packet does not approve or reject a record in the official database.** No live extraction/API/authentication/save integration is included. Gavin's API/schema files and Joshua's backend were absent from the supplied repository ZIP.

Read `M2_HANDOFF.md` for completed work, limitations, required teammate files, testing steps, and the end-to-end acceptance gate. Read `M2_VALIDATION.md` for checks actually run.

## Milestone 1 prototype

The root `index.html` is the unchanged fictional-data prototype. Its approve/reject actions are stored only in the browser. Existing PDF and screenshots document that earlier UI.

## Publishing

These files have not been committed, pushed, or deployed. After a repository update, the existing GitHub Pages workflow can serve both the root M1 prototype and `/m2/` review workbench. GitHub Pages alone cannot run the Django approval workflow; authenticated integration must use the team's agreed deployment and CSRF policy.
