# The Claude skill `mini-code`

> This content was generated with AI support (Claude, Anthropic) and subsequently checked and, where necessary, revised by a human. Examine it before use.

The skill `mini-code` creates, updates, opens and lists Mini Code artifacts in claude.ai. The skill file is [`skills/mini-code/SKILL.md`](../skills/mini-code/SKILL.md).

## Requirements

- A chat with a shell that can reach GitHub, and artifact tools (list, read, publish, declare capabilities).
- A web fetch is not sufficient. It returns a summary, not the exact file.
- To install or update the skill, the chat must be able to propose a skill (a review card). Without this, Claude gives you the file, and you upload it in the settings.

## Installation

Use the prompt in the section "Quick start with Claude" of the [README](../README.md#quick-start-with-claude). Claude finds the newest release, reads the skill file and shows it on a card. Select **Save** on the card.

## Command reference

### `/mini-code new`

Creates a new Mini Code artifact.

1. Claude asks for the name of the artifact, for example "Mini Code – Weather station".
2. Claude finds the newest release and asks you to confirm it.
3. Claude publishes `index.html` of the release without changes, with your name as the title.
4. Claude declares the database and the user capability.
5. You get the name, the version and the link.

Each artifact has its own project database. Use one artifact for each project.

### `/mini-code update`

Updates selected Mini Code artifacts to a release.

1. Claude finds the newest release and asks you to confirm it.
2. Claude finds all your Mini Code artifacts (refer to "Detection").
3. Claude offers only the artifacts with an older version. You select them in a list, or you select "All". With more than 3 artifacts, you type the numbers, for example `1, 3, 4`.
4. Claude reads the changelog. If the data model or the capabilities changed, Claude tells you and waits for your approval.
5. Claude publishes the release to each selected artifact. The link, the name, the files and the comments stay. Claude tells you about shared artifacts before it publishes them.
6. You get a table: name, old version, new version, result.

### `/mini-code open`

Continues the work with one Mini Code artifact in the current chat.

1. You select the artifact.
2. If the artifact has an older version, Claude offers `/mini-code update`.
3. Claude reads the procedures of the artifact's version, the project rules (`CLAUDE.md` and the path rules) and the focus files.
4. Claude shows the open comments, sorted by priority, and the newest changeset.

### `/mini-code list`

Shows all your Mini Code artifacts with number, name, version, last change, link and "update available". This command changes nothing.

### `/mini-code update-skill`

Updates the skill.

1. Claude finds the newest release and reads its skill file.
2. If its skill version is newer, Claude shows the old and the new version and the changelog.
3. Claude shows the new skill on a card. Select **Save** to update.

### `/mini-code`

Without a subcommand, Claude asks which command you want.

## Version check and self-update

- Each command first finds the newest release tag (`vMAJOR.MINOR.PATCH`) on GitHub and asks you to confirm it. You can also name an older release. The skill never uses a branch.
- The skill file contains the line `Skill version: X.Y.Z`. Each command compares it with the skill file of the release.
- If the release has a newer skill, Claude tells you before it continues. Select "Update the skill now" to get the card, or "Not now" to continue with the installed skill.
- The skill cannot change itself without your approval. Each update needs your click on the card.

## Detection

Claude lists your own artifacts. It skips artifacts that are made from a type (Docs, Sheets, Slides, Design) and reads the first 15 lines of each other artifact.

- An artifact with `<meta name="mini-code-version" content="X.Y.Z">` is Mini Code version X.Y.Z (0.4.2 and newer).
- An artifact with a comment that starts with `Mini Code Editor` in its head is Mini Code older than 0.4.2.
- A version with a suffix, for example `0.5.0-dev`, is a development version. It is older than the release `0.5.0`.
- The title is not used. The platform replaces the HTML title with the name of the artifact.

## Limits

- The selection dialog has at most 4 options in each question. With more than 3 artifacts, you type the numbers.
- Detection finds only artifacts that you own. Artifacts that others shared with you are not updated.
- Detection reads each of your artifacts. With many artifacts, this takes some time.
- The skill does not change the data in the project databases.
