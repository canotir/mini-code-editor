# Quick-start prompt for Claude

> This content was generated with AI support (Claude, Anthropic) and subsequently checked and, where necessary, revised by a human. Examine it before use.

Use these prompts to set up Mini Code as a claude.ai artifact. Copy a prompt and paste it into a new chat with Claude.

## Requirements

- The chat must have a shell and artifact tools.
- Claude must be able to reach GitHub from the shell.
- A web fetch alone is not sufficient. It returns a summary, not the exact file.

## Prompt 1: set up Mini Code

Use this prompt one time for each project.

```text
Please set up "Mini Code" for me as an artifact.

1. Download the editor into your workspace with the shell:
   git clone https://github.com/canotir/mini-code-editor
   git -C mini-code-editor checkout v0.4.1
   If you cannot run shell commands or reach GitHub, tell me and stop.
2. Read index.html and docs/claude-integration.md completely before you publish anything.
3. Publish index.html without changes as a new artifact with the title "Mini Code".
4. Declare these capabilities for the artifact:
   {"db": {"rules": [{"path": "", "read": "view", "write": "owner"}]}, "user": {}}
5. Give me the link. Do not write files into the project unless I ask.

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

## Why the prompt uses a release tag

The `checkout` line selects one released version. Without it, `git clone` gets the newest version, which can contain changes that nobody examined.

Only the owner of the repository can create or move a tag. When you release a new version, do these steps:

1. Change the tag in the prompts to the new version, for example `v0.4.2`.
2. Commit the change.
3. Create the release with this tag on the new commit.
