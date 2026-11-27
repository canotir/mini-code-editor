# Data notes

> This content was generated with AI support (Claude, Anthropic) and subsequently checked and, where necessary, revised by a human. Examine it before use.

This file tells you how each version changes the data in the project database of a Mini Code artifact. The jelk package manager shows this file before an update. `jelk.json` refers to it as `dataNotes`.

## Data model version

The record `meta/schema` holds the data model version: `{version, app, at}`.

- `version`: an integer. The data model that the data uses.
- `app`: the Mini Code version that wrote the record.
- `at`: the time in ISO 8601, UTC.

If the record is missing, the data model is version 1.

The page knows one data model version (the constant `DATA_SCHEMA` in `index.html`). When the page opens:

- If `meta/schema` is missing and the person can write, the page writes `{version: 1, …}` one time.
- If `version` is higher than the version that the page knows, the page becomes read-only. The status bar shows "Project (read only: newer data model)". The page writes nothing to the database, and it keeps the change markers in the browser. Update the page to a newer Mini Code version.
- The page never changes or deletes an existing `meta/schema` record.

## Versions

| Mini Code | Data model | Change to the data |
|---|---|---|
| 0.4.2 and older | 1 (no record) | `files/`, `meta/dirs`, `comments/` |
| 0.5.0, 0.6.0 | 1 (no record) | Adds `history/`, `changesets/`, `meta/paths`, `data/users/<uid>/seen` and new optional fields. No old record changes. |
| 0.7.0 | 1 | Adds the record `meta/schema`. No other record changes. |

### 0.7.0

- The page adds `meta/schema` with `version: 1`. It changes no other record.
- Downgrade: possible. Version 0.6.0 and older ignore `meta/schema`.

## Rules for a new data model version

1. A migration only adds records or fields. It keeps the old records and fields.
2. The migration runs in the page when the page opens. It does not run in a Claude chat.
3. The page asks the person to confirm that the new version works. Before that confirmation, the old data stays complete, so a downgrade stays possible.
4. Increase `DATA_SCHEMA` in `index.html` and add a row to the table in this file.
5. Update `docs/claude-integration.md`, because Claude reads it before it writes data.
