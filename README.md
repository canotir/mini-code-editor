# Mini Code

A small code editor in one HTML file. It looks and works like a simple version of Visual Studio Code (VS Code): an explorer on the left, an editor with tabs in the middle, and search across all files.

![Mini Code with the comments panel: comments with kinds and priorities, a question from Claude that waits for an answer, and a comment that Claude resolved](docs/images/comments.png)

*Screenshot with sample content, made automatically with a headless browser.*

You can use Mini Code in two modes:

- **Browser-only mode.** Open `index.html` in a browser, or publish it with GitHub Pages. The files stay in the storage of your browser.
- **Claude artifact mode.** Publish `index.html` as an artifact on claude.ai with a project database. Then Claude can read and write the same files, and you can add comments to code for Claude. Refer to [docs/claude-integration.md](docs/claude-integration.md).

## Features

- Explorer: create, rename, delete and move files and folders. Move them with drag and drop. Import files or a full folder.
- Editor: tabs, line numbers, syntax colors for 15 languages ([list](#supported-languages)), indent and outdent, auto-indent, line comments, undo for each tab.
- Command palette with all commands (`Ctrl+Shift+P`, `⌘⇧P` or `F1`). Go to file and go to line.
- Find and replace in the current file (`Ctrl+F`).
- Search and replace in all files (`Ctrl+Shift+F`): match case, whole word, regular expressions, files to include and to exclude.
- Light and dark theme. Layout for phones.
- Claude artifact mode only: live updates, a conflict bar with a compare view, and comments on selected text (`Ctrl+K` then `C`; macOS: `⌘K` then `C`).
- Claude artifact mode only, from version 0.5.0:
  - File history: the last 5 revisions of each file. Compare a revision with the current text and restore it. Restore deleted files.
  - Activity: one changeset for each Claude turn, with the changed files, comments, test results, open points and items not tested. Review the diff of a changeset and undo it. Apply or reject a proposal.
  - Change markers: a dot marks files that changed since you opened them the last time. The markers are kept for each person and work across devices.
  - Path rules in the Explorer menu: read-only for Claude, focus files for Claude, and pinned files at the top.
  - Comment kinds (note, question, bug, to-do, idea), priorities, "Waiting for you" and "Waiting for Claude", a kind filter, and sorting.

## Supported languages

Mini Code shows syntax colors for these languages. It finds the language from the file extension or the file name.

| Language | File extensions and file names |
|----------|--------------------------------|
| C and C++ (also Arduino) | `.c` `.h` `.cpp` `.cc` `.hpp` `.ino` |
| Python | `.py` |
| JavaScript | `.js` `.mjs` `.cjs` `.jsx` |
| TypeScript | `.ts` `.tsx` |
| Java | `.java` |
| Go | `.go` |
| Rust | `.rs` |
| Shell | `.sh` `.bash` `.zsh`, `Makefile`, `Dockerfile`, `.gitignore`, `.bashrc` |
| HTML and XML | `.html` `.htm` `.xml` `.svg` `.vue` |
| CSS | `.css` `.scss` |
| JSON | `.json` |
| Markdown | `.md` `.markdown` |
| INI | `.ini` `.cfg` `.conf` |
| TOML | `.toml` |
| YAML | `.yml` `.yaml` |

Mini Code shows all other files as plain text. You can edit and search them.

The syntax colors are simple. They show comments, strings, numbers, keywords and function calls. For HTML they also show tags and attributes. For Markdown they also show headings, lists and code. Mini Code does not analyze the code. For `Makefile` and `Dockerfile`, it uses the shell colors as an approximation.

The user interface is in English only.

## Screenshots

All screenshots show sample content. They were made automatically with a headless browser.

| | |
|---|---|
| ![Comment box at a selection in main.cpp](docs/images/write-comment.png) | ![Search panel with a replace preview across files](docs/images/search-replace.png) |
| Comment on selected text. Each comment gets a number, such as #4. | Search and replace in all files, with a preview of each change. |
| ![Command palette with all commands and their shortcuts](docs/images/command-palette.png) | ![Comments panel with open and resolved comments](docs/images/comments.png) |
| The command palette shows all commands and their shortcuts. | Claude replies to comments and resolves them. |
| ![Activity panel with two changesets from Claude: changed files, comments, test result, open points and items not tested](docs/images/activity.png) | ![Review of a changeset: the diff of each changed file and the Undo button](docs/images/review.png) |
| Activity shows one changeset for each Claude turn (version 0.5.0). | Review the diff of a changeset and undo it. |
| ![Explorer with a pinned file, change markers, a lock icon and the menu with the path rules](docs/images/explorer-rules.png) | |
| Dots mark changed files. The Explorer menu sets the path rules. | |

## Quick start with Claude

Install the Claude skill `mini-code` one time. Copy this prompt into a chat with Claude. The chat must have a shell and artifact tools.

```text
Please install the Mini Code skill for me.

1. Find the newest release of Mini Code with the shell:
   git ls-remote --tags --refs https://github.com/canotir/mini-code-editor
   Use the highest tag of the form vMAJOR.MINOR.PATCH. Tell me which tag you use.
2. Download this release:
   git clone --depth 1 --branch <tag> https://github.com/canotir/mini-code-editor
   If you cannot run shell commands or reach GitHub, tell me and stop.
3. Read skills/mini-code/SKILL.md completely. Do not change it.
4. Propose it to me as a new skill with the name "mini-code", so that I can save it.
5. Tell me the commands of the skill.
```

Then type `/mini-code new` to create your first Mini Code artifact.

### Command reference

| Command | Action |
|---|---|
| `/mini-code new` | Create a new Mini Code artifact. Claude asks for its name, installs the newest release and gives you the link. Each artifact has its own files and comments. |
| `/mini-code update` | Find your Mini Code artifacts and show the ones with an older version. You select the artifacts to update, or all. Each artifact keeps its link, name, files and comments. |
| `/mini-code open` | Select one Mini Code artifact and continue to work with it in this chat. Claude reads the project rules and shows the open comments and the newest changeset. |
| `/mini-code list` | Show all your Mini Code artifacts with name, version and "update available". Changes nothing. |
| `/mini-code update-skill` | Update the skill to the version of the newest release. |
| `/mini-code` | Ask which of the commands above you want. |

Each command first finds the newest release and asks you to confirm it. If that release has a newer skill, Claude offers to update the skill first. A skill update always shows a card that you save with one click. The skill never changes without your approval.

For details and limits, refer to [docs/skill.md](docs/skill.md). For chats without skills, use the prompts in [docs/quick-start-prompt.md](docs/quick-start-prompt.md).

## Setup

Mini Code has no dependencies and no build step.

1. Download `index.html`.
2. Open it in a current browser (Chrome, Edge, Firefox or Safari).

To use GitHub Pages:

1. In the repository settings, open **Pages**.
2. Select the branch `main` and the folder `/ (root)`.
3. Open the URL that GitHub shows.

## Use

The shortcuts work with all keyboard layouts on Windows, Linux and macOS. Mini Code does not use Alt or Option shortcuts, because these keys type characters on many layouts (for example AltGr or Option+N).

To see all commands, press `Ctrl+Shift+P` (macOS: `⌘⇧P`) or `F1`. The command palette also shows the shortcuts.

| Action | Windows and Linux | macOS |
|--------|-------------------|-------|
| Show all commands | `Ctrl+Shift+P` or `F1` | `⌘⇧P` or `F1` |
| Go to file | `Ctrl+P` | `⌘P` |
| Go to line | `Ctrl+G` | `⌃G` |
| Save · save all | `Ctrl+S` · `Ctrl+Shift+S` | `⌘S` · `⌘⇧S` |
| Find in this file | `Ctrl+F` | `⌘F` |
| Search in files · replace in files | `Ctrl+Shift+F` · `Ctrl+Shift+H` | `⌘⇧F` · `⌘⇧H` |
| Toggle line comment | `Ctrl+/` or `Ctrl+#` | `⌘/` or `⌘#` |
| Toggle sidebar | `Ctrl+B` | `⌘B` |
| New file | `Ctrl+K` then `N` | `⌘K` then `N` |
| Close tab | `Ctrl+K` then `W` | `⌘K` then `W` |
| Previous tab · next tab | `Ctrl+K` then `←` · `→` | `⌘K` then `←` · `→` |
| Comment on the selection (artifact mode) | `Ctrl+K` then `C` | `⌘K` then `C` |
| Toggle comments panel (artifact mode) | `Ctrl+K` then `M` | `⌘K` then `M` |
| Rename · delete (in the explorer) | `F2` · `Del` | `F2` · `⌘⌫` |

Notes:

- On German keyboards, use `Ctrl+#` to toggle a line comment, as in VS Code.
- Shortcuts use the letter that is printed on the key. Thus they also work with AZERTY and QWERTZ layouts.
- Some browsers keep a shortcut for themselves (for example `Ctrl+W`, `⌘W`, `Ctrl+N`). For this reason, Mini Code uses `Ctrl+K` chords. All commands are also in the command palette.

## Limits

- Browser-only mode keeps the files in the local storage of one browser. The limit is approximately 5 MB. Other devices cannot see the files. Make backups.
- Mini Code has no terminal and no Git integration.
- The page cannot start downloads in the claude.ai artifact frame. Use the **Copy** button.

## Tests

The tests were done manually and with automated browser scripts (Playwright and headless Chrome) during development. The repository does not contain test scripts at this time.

## Disclaimer

Mini Code is an independent hobby project. It is not affiliated with, sponsored by or endorsed by Microsoft. Visual Studio Code and VS Code are trademarks of Microsoft Corporation. Mini Code does not contain code, icons or other assets from Visual Studio Code.

## License

MIT. Refer to [LICENSE](LICENSE). Mini Code uses no external code, fonts or images. Refer to [NOTICE.md](NOTICE.md).

## AI disclosure

This content was generated with AI support (Claude, Anthropic) and subsequently checked and, where necessary, revised by a human.

- Claude (Anthropic) wrote most of the code and the documentation.
- A human specified the requirements, tested the editor and examined the result.
- Claude made the screenshots automatically with a headless browser. They show sample content. They are not edited.
- Examine the code before you use it for important work.
