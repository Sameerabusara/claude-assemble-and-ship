# qa-kit

A small Claude Code plugin with two helpers for everyday review work:

- **Summarise changes** — a slash command that lists every file touched on the current branch with a one-line description of each change, short enough to paste into a pull-request description.
- **Code reviewer** — a subagent that reads recent changes and reports bugs, missing error handling and unclear names, grouped by severity (high, medium, low).

## Components

| Component | Type | File | What it does |
| --- | --- | --- | --- |
| `summarize-changes` | Slash command | `commands/summarize-changes.md` | Summarises the branch's changes for a PR description |
| `code-reviewer` | Subagent | `agents/code-reviewer.md` | Reviews recently changed code (read-only tools: Read, Grep, Glob) |

## Installation

Load the plugin from a local checkout:

```bash
claude --plugin-dir /path/to/claude-assemble-and-ship
```

Use `/reload-plugins` inside Claude Code after editing any component.

## Usage

**Summarise a branch** — run the command with its namespaced name:

```
/qa-kit:summarize-changes
```

Paste the output straight into your pull-request description.

**Review recent changes** — ask Claude in plain language, for example:

```
Review my recent changes for bugs.
```

Claude hands the review to the `code-reviewer` subagent, which returns a short, severity-grouped list with the file and a one-sentence fix for each item.

## Plugin layout

```
.
├── .claude-plugin/
│   └── plugin.json            # manifest: name, version, description
├── commands/
│   └── summarize-changes.md   # /qa-kit:summarize-changes
├── agents/
│   └── code-reviewer.md       # code-reviewer subagent
└── README.md
```

Only `plugin.json` lives in `.claude-plugin/`; the component folders sit at the root.
