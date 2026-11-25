# CLAUDE.md – Mini Code

Read this file before you start a task. It contains the rules for agents in this repository.

## Overview
Mini Code is a code editor in one HTML file. It runs in a browser, or as a claude.ai artifact with a project database.

## Structure
- `index.html`: the full application (HTML, CSS and JavaScript).
- `docs/claude-integration.md`: data model and procedures for artifact mode.

## Hardware
None.

## Commands
- Run: open `index.html` in a browser.
- Syntax check: extract the script and run `node --check`.
- Build: none.

## Tools
- Languages: HTML, CSS, JavaScript (ES2020, no framework).
- Formatter and linter: none at this time.
- Tests: manual tests and Playwright scripts (not in the repository).
- Branch model: `main` only. Use feature branches for large changes.
- Version scheme: Semantic Versioning (MAJOR.MINOR.PATCH).

## Project rules
- Keep the application in one file. Do not add external code, fonts or images.
- Treat all data from the database and from imported files as text. Escape it before you put it into HTML.
- Do not put artifact IDs, links or personal data into the repository.

## Release
The version number is in these locations. Change all of them for each release.

| File | Location | Example |
|------|----------|---------|
| `index.html` | `<meta name="mini-code-version" content="…">` in `<head>` (line 7) | `content="0.4.2"` |
| `README.md` | Quick-start prompt: `git -C mini-code-editor checkout v…` | `checkout v0.4.2` |
| `README.md` | Update prompt: first line `…to version v…` and `checkout v…` | `version v0.4.2` |
| `docs/quick-start-prompt.md` | Prompt 1 and prompt 3: the same lines as in `README.md` | `checkout v0.4.2` |
| `CHANGELOG.md` | New heading at the top | `## 0.4.2 – 2026-11-25` |

Do not change the text "older than 0.4.2" in the update prompt. Version 0.4.2 is the first version with the meta tag.

The welcome screen reads the version from the meta tag. No other code holds the version.

Procedure:

1. Change the version in all locations in the table.
2. Make sure that the prompts in `README.md` and in `docs/quick-start-prompt.md` are identical.
3. To find old version numbers, run `grep -rn "v0\.4\.1\|0\.4\.1" README.md docs index.html` (use the old version).
4. Commit. Get approval, then push.
5. The owner creates the release and the tag on GitHub, with the target `main`. The tag must point to the commit that contains the new version numbers. The git proxy of Claude sessions blocks tag pushes.

## Deviations
- This repository has no GLOBAL_AGENTS.md and no separate AGENTS.md. The owner decided on 2026-11-25 to keep all agent rules in this file.
- The code uses short names for some UI variables (for example `fs`, `cm`, `S`) to keep the single file compact.
