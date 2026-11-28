# Changelog

All dates are in ISO 8601 (UTC).

## 0.7.0 – 2026-11-28

### Added
- `jelk.json`: manifest for the jelk package manager, with the parts page and skill. The manifest refers to the current paths, so the old prompts continue to work, and the skill 0.6.0 can still update itself to this version.
- Meta tag `jelk-package` in `index.html` and the line `Jelk-package:` in `skills/mini-code/SKILL.md`.
- Data model version in the record `meta/schema`. The page writes `version: 1` if the record is missing. If the data has a newer data model, the page becomes read-only and the status bar shows "Project (read only: newer data model)". If the version cannot be read, the page also becomes read-only ("unknown data model") until it can read version 1 again.
- One write guard for all database writes of the page. It also stops operations that started before the page became read-only, and it blocks writes until the page has read the data model version.
- `docs/data-notes.md`: the data model version, the data changes of each version and the rules for migrations.

### Changed
- `docs/claude-integration.md`: Claude checks `meta/schema` before it writes data (section 2.3).
- `CLAUDE.md`: the branch model with `main` and `dev`, the new version locations and the rule for data model changes.
- The skill `mini-code` is a part of the jelk package. jelk installs and updates the page and the skill. The skill keeps `new`, `open` and `list`.
- `/mini-code new` publishes the page of the skill's own version (the line `Jelk-package`), not the newest release. It sets the version label `jelk:mini-code@X.Y.Z`, so that jelk can update the artifact.
- `/mini-code list` does not need GitHub. Its column "update available" now compares each artifact with the skill (older, same or newer).
- README: the new section "Installation" has the ways "With jelk (recommended)" and "Manual installation", like mini-spice. The section "Skill for Claude" has the command reference. `docs/skill.md`: installation with `/jelk install mini-code`. `docs/quick-start-prompt.md`: do not use the update prompt for artifacts that jelk manages.
- The update prompt reads `docs/data-notes.md`.

### Removed
- `/mini-code update` and `/mini-code update-skill` no longer update. They only tell the user to use `/jelk update mini-code`.

### Fixed
- A re-render of the Explorer, for example after a change by Claude, no longer creates the file whose name the person is typing. The typed name and the caret stay in the input. If the file of an open rename is deleted, the rename ends.

### Known limits
- The page has no confirmation "the new version works". It is necessary only for the first migration to data model 2.
- The page database has no "create only" write. If an older page and a newer page open a project without `meta/schema` at the same time, the older page can overwrite the record. A newer page writes its version again (rule 7 in `docs/data-notes.md`).
- If you have the skill 0.6.0: it has no `Jelk-package` line. Update it one time with its own command `/mini-code update-skill`. The new skill has the line, and jelk can then update it. Alternative: run `/jelk install mini-code`. jelk warns about the skill without the line: select "Replace". Artifacts that were made or updated without jelk have no jelk version label, so the first `/jelk update` asks about them.

## 0.6.0 – 2026-11-26

### Added
- Claude skill `mini-code` in `skills/mini-code/SKILL.md` with the commands `/mini-code new`, `update`, `open`, `list` and `update-skill`. The skill finds the newest release, detects all Mini Code artifacts of the user and lets the user select the artifacts to update. It checks its own version and offers an update of itself.
- `docs/skill.md`: command reference, version check, detection and limits of the skill.

### Changed
- The quick start in `README.md` installs the skill with one prompt and has a command reference. The prompts for chats without skills are only in `docs/quick-start-prompt.md`.
- The prompts in `docs/quick-start-prompt.md` install version 0.6.0. The manual update prompt sets the page title to the name of the artifact.
- `CLAUDE.md`: the skill version is a version location. The README has no version number.

## 0.5.0 – 2026-11-26

### Added
- Disclaimer in `README.md`: Mini Code is not affiliated with Microsoft.
- File history: the page keeps the last 5 revisions of each file in `history/`. The History button shows them, compares them and restores them into the editor.
- Changesets in `changesets/` and the Activity panel: review the diff of each changeset, undo an applied changeset, apply or reject a proposal.
- Change markers for files that changed since the person opened them. Kept privately for each person in `data/users/<uid>/seen`, or in the browser without a user ID.
- Path rules in `meta/paths`: read-only for Claude, focus files and pinned files. Explorer menu items and commands for them. Command "Open project rules (CLAUDE.md)".
- Comment fields `kind`, `priority` and `waitingFor`, with badges, a kind filter and sorting by position, priority or time.
- Status block on the welcome screen.
- New screenshots in `README.md`: Activity, review of a changeset, and the Explorer with path rules. The other screenshots show the new version.
- Command "Restore a deleted file": the page keeps the last text of deleted and moved files in the file history.

### Changed
- File records get the fields `changeset` and `byUser`. File IDs for new paths can have at most 188 bytes, so that history IDs stay in the segment limit.
- `docs/claude-integration.md`: new procedures for the file history, changesets, proposals, path rules and comment states.
- A file that is created again continues the revision numbers of its history.
- The delete dialog tells how to restore a file.
- The prompts in `README.md` and `docs/quick-start-prompt.md` install version 0.5.0.
- The setup prompt tells Claude to ask for the name of the new artifact, so that you can have several Mini Code artifacts. The update prompt keeps the title.

## 0.4.2 – 2026-11-25

### Added
- List of supported languages in `README.md`.
- Screenshots in `README.md` and `docs/images/`.
- Version number in the page (`<meta name="mini-code-version">`) and on the welcome screen.
- Prompt to update an existing Mini Code artifact, in `README.md` and in `docs/quick-start-prompt.md`.

### Fixed
- The status bar labels "Spaces", "UTF-8" and "LF" had too little contrast.

## 0.4.1 – 2026-11-25

### Changed
- The quick-start prompts select a release tag instead of a commit hash.

## 0.4.0 – 2026-11-25

### Added
- Quick-start prompt for Claude in `README.md` and in `docs/quick-start-prompt.md`.
- Command palette (`Ctrl+Shift+P`, `⌘⇧P` or `F1`) with all commands and their shortcuts.
- `Ctrl+K` and `⌘K` chords for new file, close tab, previous and next tab, comment, and comments panel.
- `Ctrl+#` toggles a line comment on German keyboards.
- Shortcut labels for the platform (`⌘` `⇧` `⌃` on macOS, `Ctrl` and `Shift` on Windows and Linux).

### Changed
- Shortcuts use the letter that is printed on the key, not the key position.
- Go to line on macOS is `⌃G`.

### Removed
- All Alt and Option shortcuts. They blocked characters on some layouts.

### Fixed
- AltGr characters (for example `@`, `{`, `ś`) no longer start shortcuts.
- Code no longer shows below the line numbers when you scroll horizontally.

## 0.3.0 – 2026-11-25

### Added
- Comments on selected text (`Alt+C`), with gutter markers, a comments panel, replies, and resolve and reopen. Artifact mode only.
- Move files and folders with drag and drop in the explorer.

### Removed
- Chat panel. Comments replace it.

## 0.2.0 – 2026-11-25

### Added
- Storage in the project database of a claude.ai artifact, with live updates.
- Conflict bar with a compare view when a file changes during unsaved edits.
- Search and replace in all files, with match case, whole word, regular expressions, and files to include and to exclude.
- Whole word and regular expressions in find and replace for the current file.
- Browser-only mode when no project database is available.

## 0.1.0 – 2026-11-25

### Added
- First version: explorer, editor with tabs, syntax colors, go to file, find and replace, storage in the browser.
