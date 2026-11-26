# Quick-start prompt for Claude

> This content was generated with AI support (Claude, Anthropic) and subsequently checked and, where necessary, revised by a human. Examine it before use.

Use these prompts to set up Mini Code as a claude.ai artifact in a chat without skills. If the chat can use skills, install the skill `mini-code` instead. Refer to the section "Quick start with Claude" in the README and to [skill.md](skill.md).

Copy a prompt and paste it into a new chat with Claude.

## Requirements

- The chat must have a shell and artifact tools.
- Claude must be able to reach GitHub from the shell.
- A web fetch alone is not sufficient. It returns a summary, not the exact file.

## Prompt 1: set up Mini Code

Use this prompt one time for each project. Each run creates a separate Mini Code artifact with its own files and comments. Claude asks you for its name first.

```text
Please set up "Mini Code" for me as an artifact.

1. Ask me for the name of the new artifact, for example "Mini Code – Weather station".
   Each Mini Code artifact has its own files and comments, so I can have several.
   Wait for my answer.
2. Download the editor into your workspace with the shell:
   git clone https://github.com/canotir/mini-code-editor
   git -C mini-code-editor checkout v0.6.0
   If you cannot run shell commands or reach GitHub, tell me and stop.
3. Read index.html and docs/claude-integration.md completely before you publish anything.
4. Publish index.html without changes as a new artifact. Use the name from step 1 as the title.
5. Declare these capabilities for the artifact:
   {"db": {"rules": [{"path": "", "read": "view", "write": "owner"}]}, "user": {}}
6. Give me the name and the link. Do not write files into the project unless I ask.

When I later ask you to read or change files or comments in Mini Code,
follow docs/claude-integration.md.
```

## Prompt 2: continue in a new chat

Use this prompt when Mini Code is already set up. Replace `<link>` with the link to your artifact.

```text
Open my Mini Code artifact: <link>
First download https://github.com/canotir/mini-code-editor with git and read
docs/claude-integration.md. Then look at my open comments.
```

## Prompt 3: update Mini Code

Use this prompt to update an existing Mini Code artifact to a newer version. Replace `<link>` with the link to your artifact. Your files and comments stay in the project database.

```text
Please update my Mini Code artifact to version v0.6.0: <link>

1. Read my artifact and find its version in the tag
   <meta name="mini-code-version">. If the tag is missing, the version is older than 0.4.2.
2. Download the new version into your workspace with the shell:
   git clone https://github.com/canotir/mini-code-editor
   git -C mini-code-editor checkout v0.6.0
   If you cannot run shell commands or reach GitHub, tell me and stop.
3. Read CHANGELOG.md for all versions newer than mine, and docs/claude-integration.md.
   If the data model or the capabilities changed, tell me and wait for my approval.
4. Read index.html completely. In a copy, set the text of the <title> element to the
   name of my artifact. Change nothing else. Publish the copy to my existing artifact
   (same link). Keep its title. Do not create a new artifact.
5. Keep the declared capabilities. Do not change or delete data in the project database.
6. Tell me the old and the new version.
```

## Why the prompt uses a release tag

The `checkout` line selects one released version. Without it, `git clone` gets the newest version, which can contain changes that nobody examined.

Only the owner of the repository can create or move a tag. When you release a new version, do these steps:

1. Change the tag in all prompts to the new version, for example `v0.4.3`. Also change `content` in the tag `<meta name="mini-code-version">` in `index.html`.
2. Commit the change.
3. Create the release with this tag on the new commit.
