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

## Deviations
- This repository has no GLOBAL_AGENTS.md and no separate AGENTS.md. The owner decided on 2026-11-25 to keep all agent rules in this file.
- The code uses short names for some UI variables (for example `fs`, `cm`, `S`) to keep the single file compact.
