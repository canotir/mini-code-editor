# Changelog

All dates are in ISO 8601 (UTC).

## 0.4.2 – 2026-11-25

### Added
- Screenshots in `README.md` and `docs/images/`.

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
