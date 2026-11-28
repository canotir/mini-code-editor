# The Claude skill `mini-code`

> This content was generated with AI support (Claude, Anthropic) and subsequently checked and, where necessary, revised by a human. Examine it before use.

The skill `mini-code` creates, opens and lists Mini Code artifacts in claude.ai. The skill file is [`skills/mini-code/SKILL.md`](../skills/mini-code/SKILL.md).

The skill is a part of the jelk package `mini-code`, together with the page. jelk installs and updates both parts. The skill never updates an artifact or itself.

## Requirements

- The commands `new` and `open` need a chat with a shell that can reach GitHub. All commands need the artifact tools (list, read, publish, declare capabilities).
- A web fetch is not sufficient. It returns a summary, not the exact file.

## Installation and updates

- Install: `/jelk install mini-code`. jelk shows each part of the package (the page and the skill) and asks for your approval.
- Update: `/jelk update mini-code`. jelk updates the skill and the selected Mini Code artifacts. Use only jelk for updates.
- The skill file contains the line `Jelk-package: mini-code@X.Y.Z`. jelk uses it to find the installed version of the skill.

If you have the skill 0.6.0: it has no `Jelk-package` line. Install the package with jelk one time. jelk then replaces the skill.

## Command reference

### `/mini-code new`

Creates a new Mini Code artifact.

1. Claude asks for the name of the artifact, for example "Mini Code – Weather station".
2. Claude gets the release of the installed skill version (the version in the line `Jelk-package`). It does not use a newer release. Only jelk changes the version.
3. Claude publishes `index.html` of that release without changes, with your name as the title and the version label `jelk:mini-code@X.Y.Z`. With this label, jelk can update the artifact later.
4. Claude declares the database and the user capability.
5. You get the name, the version and the link.

Each artifact has its own project database. Use one artifact for each project.

### `/mini-code open`

Continues the work with one Mini Code artifact in the current chat.

1. You select the artifact.
2. If the artifact has an older version than the skill, Claude tells you that `/jelk update mini-code` can update it.
3. Claude reads the procedures of the artifact's version, the project rules (`CLAUDE.md` and the path rules) and the focus files.
4. Claude shows the open comments, sorted by priority, and the newest changeset.

### `/mini-code list`

Shows all your Mini Code artifacts with number, name, version, last change, link and "older than this skill". This command changes nothing and does not need GitHub.

### `/mini-code update` and `/mini-code update-skill`

Removed in version 0.7.0. Claude tells you to use `/jelk update mini-code`.

### `/mini-code`

Without a subcommand, Claude asks which command you want.

## Versions

- The skill uses only the release tag of its own version (`vX.Y.Z`). It never uses a branch or a newer tag.
- If the tag does not exist, for example for a development version with the suffix `-dev`, the commands `new` and `open` stop.
- The skill checks that the page of the release has the tag `<meta name="jelk-package" content="mini-code@X.Y.Z">` with the same version.

## Detection

Claude lists your own artifacts. It skips artifacts that are made from a type (Docs, Sheets, Slides, Design) and reads the first 15 lines of each other artifact.

- An artifact with `<meta name="mini-code-version" content="X.Y.Z">` is Mini Code version X.Y.Z (0.4.2 and newer).
- An artifact with a comment that starts with `Mini Code Editor` in its head is Mini Code older than 0.4.2.
- A version with a suffix, for example `0.5.0-dev`, is a development version. It is older than the release `0.5.0`.
- The title is not used. The platform replaces the HTML title with the name of the artifact.

## Limits

- The selection dialog has at most 4 options in each question. With more than 3 artifacts, you type the number.
- Detection finds only artifacts that you own.
- Detection reads each of your artifacts. With many artifacts, this takes some time.
- The skill does not change the data in the project databases.
- Artifacts that were made or updated without jelk have no jelk version label. The first `/jelk update` asks you about them.
