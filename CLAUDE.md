# CLAUDE.md – Mini Code

Read this file before you start a task. It contains the rules for agents in this repository.

## Overview
Mini Code is a code editor in one HTML file. It runs in a browser, or as a claude.ai artifact with a project database.

## Structure
- `index.html`: the full application (HTML, CSS and JavaScript).
- `docs/claude-integration.md`: data model and procedures for artifact mode.
- `skills/mini-code/SKILL.md`: the Claude skill that creates, opens and lists Mini Code artifacts. jelk installs and updates the page and the skill as one package. The skill never updates an artifact or itself. `docs/skill.md` describes it.
- `jelk.json`: the manifest for the jelk package manager. It refers to `index.html`, `docs/claude-integration.md`, `docs/data-notes.md` and `skills/mini-code/SKILL.md`. Keep their paths.
- `docs/data-notes.md`: the data model version and the data changes of each version.

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
- Branch model: `main` holds the releases. `dev` holds the development version. Use feature branches from `dev` for large changes.
- Version scheme: Semantic Versioning (MAJOR.MINOR.PATCH).

## Project rules
- Keep the application in one file. Do not add external code, fonts or images.
- Treat all data from the database and from imported files as text. Escape it before you put it into HTML.
- Do not put artifact IDs, links or personal data into the repository.
- Data model changes: obey the rules in `docs/data-notes.md`. Migrations only add records or fields. The only exception is `version` in `meta/schema` (refer to `docs/data-notes.md`). Change `DATA_SCHEMA` in `index.html`, `docs/data-notes.md` and `docs/claude-integration.md` together.

## Release
The version number is in these locations. Change all of them for each release.

| File | Location | Example |
|------|----------|---------|
| `index.html` | `<meta name="mini-code-version" content="…">` in `<head>` (line 7) | `content="0.4.2"` |
| `index.html` | `<meta name="jelk-package" content="mini-code@…">` in `<head>` (line 8). It must stay in the first 15 lines. | `content="mini-code@0.7.0"` |
| `jelk.json` | `"version"` | `"version": "0.7.0"` |
| `docs/quick-start-prompt.md` | Prompt 1: `git -C mini-code-editor checkout v…`. Prompt 3: first line `…to version v…` and `checkout v…` | `checkout v0.4.2` |
| `skills/mini-code/SKILL.md` | Line `Skill version: …`. Change it for each release, also if the skill did not change. | `Skill version: 0.6.0` |
| `skills/mini-code/SKILL.md` | Line `Jelk-package: mini-code@…` | `Jelk-package: mini-code@0.7.0` |
| `CHANGELOG.md` | New heading at the top | `## 0.4.2 – 2026-11-25` |

The README has no version number: its prompt installs the skill, and the skill finds the newest release tag.

On the branch `dev`, the meta tags, `jelk.json` and the `Jelk-package` line have the suffix `-dev` (for example `0.7.0-dev`). The line `Skill version` keeps the version of the last release, without a suffix: the skill compares only `X.Y.Z` release versions. Change it only for a release. The prompts in `docs/quick-start-prompt.md` then select the branch: `checkout dev`, and the update prompt starts with "…to the development version (branch dev):". For a release from `dev`, set the meta tags, `jelk.json`, the `Jelk-package` line and the skill version to the release version and set the prompts to the tag (`checkout v0.6.0`, "…to version v0.6.0:") before you merge into `main`. The skill uses only release tags, so it never installs the branch `dev`.

Do not change the text "older than 0.4.2" in the update prompt. Version 0.4.2 is the first version with the meta tag `mini-code-version`.

The welcome screen reads the version from the meta tag `mini-code-version`. No other code holds the version. The page code does not read the tag `jelk-package`.

Procedure:

1. Change the version in all locations in the table.
2. Make sure that the commands in `skills/mini-code/SKILL.md`, the command reference in `README.md` and `docs/skill.md` agree.
3. To find old version numbers, run `grep -rn "v0\.4\.1\|0\.4\.1" README.md docs skills index.html jelk.json` (use the old version). Do not change the version numbers in the history table of `docs/data-notes.md`, in `CHANGELOG.md` or in the text "older than 0.6.0" in `skills/mini-code/SKILL.md`.
4. Commit. Get approval, then push.
5. The owner creates the release and the tag on GitHub, with the target `main`. The tag must point to the commit that contains the new version numbers. The git proxy of Claude sessions blocks tag pushes.

## Deviations
- This repository has no GLOBAL_AGENTS.md and no separate AGENTS.md. The owner decided on 2026-11-25 to keep all agent rules in this file.
- The code uses short names for some UI variables (for example `fs`, `cm`, `S`) to keep the single file compact.
