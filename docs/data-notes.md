# Data notes

> This content was generated with AI support (Claude, Anthropic) and subsequently checked and, where necessary, revised by a human. Examine it before use.

This file tells you how each version changes the data in the project database of a Mini Code artifact. The jelk package manager will show this file before an update that changes the data model. `jelk.json` refers to it as `dataNotes`.

## Data model version

The record `meta/schema` holds the data model version: `{version, app, at}`.

- `version`: a positive integer. The data model that the data uses. The page also reads a string of digits, for example `"2"`.
- `app`: the Mini Code version that wrote the record.
- `at`: the time in ISO 8601, UTC.

If the record is missing, the data model is version 1.

The page knows one data model version (the constant `DATA_SCHEMA` in `index.html`). When the page opens:

- Until the page has read `meta/schema`, it does not write to the database. For a person who can write, the status bar shows "Connecting…". After 10 seconds without a result, the page shows a message and keeps trying.
- If `meta/schema` is missing and the person can write, the page writes `{version: 1, …}` one time.
- If `version` is higher than the version that the page knows, the page becomes read-only. The status bar shows "Project (read only: newer data model)". The page writes nothing to the database, and it keeps the change markers in the browser. Update the page to a newer Mini Code version.
- If `version` cannot be read, or the page cannot read `meta/schema`, the page also becomes read-only. The status bar shows "Project (read only: unknown data model)". The page keeps trying. When it reads version 1 again, writes are possible again.
- The read-only state also stops operations that started before it, for example an import. A write that is already in progress can still finish. An operation with several steps (for example a move or a changeset) can stop after some of its steps.
- The page never deletes `meta/schema`. It changes `version` only after a confirmed migration (rule 4 in the rules below).

## Versions

| Mini Code | Data model | Change to the data |
|---|---|---|
| 0.4.2 and older | 1 (no record) | `files/`, `meta/dirs`, `comments/` |
| 0.5.0, 0.6.0 | 1 (no record) | Adds `history/`, `changesets/`, `meta/paths`, `data/users/<uid>/seen` and new optional fields. No old record changes. |
| 0.7.0 | 1 | Adds the record `meta/schema`. No other record changes. |

### 0.7.0

- The page adds `meta/schema` with `version: 1`. It changes no other record.
- Downgrade: possible. Version 0.6.0 and older ignore `meta/schema`.
- After a change to data model 2, do not downgrade below 0.7.0. Older pages do not read `meta/schema` and can write to the data.

## Rules for a new data model version

1. A migration only adds records or fields. It keeps the old records and fields.
2. The migration runs in the page when the page opens. It does not run in a Claude chat.
3. The page asks the person to confirm that the new version works. Before that confirmation, the old data stays complete, so a downgrade stays possible.
4. The page sets `version` in `meta/schema` to the new number only after the person confirms. This is the only change to an existing `meta/schema` record.
5. Increase `DATA_SCHEMA` in `index.html` and add a row to the table in this file.
6. Update `docs/claude-integration.md`, because Claude reads it before it writes data.
7. A page with a newer data model reads `meta/schema` each time it opens and on each change. If it finds a lower `version` after the confirmation, it writes its own `version` again. Reason: the page database has no "create only" write. An older page that writes the missing record at the same time as a newer page can overwrite it. The rewrite repairs this, and the older page then becomes read-only.
