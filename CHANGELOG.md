# Changelog

All dates are in ISO 8601 (UTC).

## Unreleased

### Added
- Claude skill `mini-code` in `skills/mini-code/SKILL.md` with the commands `/mini-code new`, `update`, `open`, `list` and `update-skill`. The skill finds the newest release, detects all Mini Code artifacts of the user and lets the user select the artifacts to update. It checks its own version and offers an update of itself.
- `docs/skill.md`: command reference, version check, detection and limits of the skill.

### Changed
- The quick start in `README.md` installs the skill with one prompt and has a command reference. The prompts for chats without skills are only in `docs/quick-start-prompt.md`.
- On the branch `dev`, the prompts in `docs/quick-start-prompt.md` install the branch `dev`.
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
