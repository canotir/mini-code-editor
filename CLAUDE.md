# CLAUDE.md – Mini Code

Read this file before you start a task. It contains the rules for agents in this repository.

## Overview
Mini Code is a code editor in one HTML file. It runs in a browser, or as a claude.ai artifact with a project database.

## Structure
- `index.html`: the full application (HTML, CSS and JavaScript).
- `docs/claude-integration.md`: data model and procedures for artifact mode.
- `skills/mini-code/SKILL.md`: the Claude skill that creates, updates, opens and lists Mini Code artifacts. `docs/skill.md` describes it.

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
| `docs/quick-start-prompt.md` | Prompt 1: `git -C mini-code-editor checkout v…`. Prompt 3: first line `…to version v…` and `checkout v…` | `checkout v0.4.2` |
| `skills/mini-code/SKILL.md` | Line `Skill version: …`. Change it for each release, also if the skill did not change. | `Skill version: 0.6.0` |
| `CHANGELOG.md` | New heading at the top | `## 0.4.2 – 2026-11-25` |

The README has no version number: its prompt installs the skill, and the skill finds the newest release tag.

On the branch `dev`, the meta tag has the suffix `-dev` (for example `0.6.0-dev`). The prompts in `docs/quick-start-prompt.md` then select the branch: `checkout dev`, and the update prompt starts with "…to the development version (branch dev):". For a release from `dev`, set the meta tag and the skill version to the release version and set the prompts to the tag (`checkout v0.6.0`, "…to version v0.6.0:") before you merge into `main`. The skill uses only release tags, so it never installs the branch `dev`.

Do not change the text "older than 0.4.2" in the update prompt. Version 0.4.2 is the first version with the meta tag.

The welcome screen reads the version from the meta tag. No other code holds the version.

Procedure:

1. Change the version in all locations in the table.
2. Make sure that the commands in `skills/mini-code/SKILL.md`, the command reference in `README.md` and `docs/skill.md` agree.
3. To find old version numbers, run `grep -rn "v0\.4\.1\|0\.4\.1" README.md docs skills index.html` (use the old version).
4. Commit. Get approval, then push.
5. The owner creates the release and the tag on GitHub, with the target `main`. The tag must point to the commit that contains the new version numbers. The git proxy of Claude sessions blocks tag pushes.

## Deviations
- This repository has no GLOBAL_AGENTS.md and no separate AGENTS.md. The owner decided on 2026-11-25 to keep all agent rules in this file.
- The code uses short names for some UI variables (for example `fs`, `cm`, `S`) to keep the single file compact.
