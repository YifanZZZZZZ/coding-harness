# Coding Agent Harness

This is a lightweight local coding agent for code repositories. It runs directly in your terminal: it first inspects the current workspace, then uses a constrained set of tools to read files, edit files, and run commands, keeping session state in a local `.pico/` directory.

It behaves more like a command-line assistant that can keep working inside a repository than a plain chat window. Use it to investigate code, fix tests, analyze a repository, or run one-off engineering tasks in your current project.

## What It's Good For

- Investigating failing tests in a local repository
- Reading the current code structure and proposing changes
- Iterating in small steps on existing files instead of guessing without repository context
- Preserving context across a session so you can pick up where you left off

## Screenshots

CLI help:

![pico help](assets/screenshots/pico-help.png)

Startup screen:

![pico start](assets/screenshots/pico-start.png)

Built-in REPL commands and session path:

![pico repl](assets/screenshots/pico-repl.png)

## Installation

Requires Python 3.10+.

If you use `uv`, install the dependencies directly:

```bash
uv sync
```

If you are already working inside your own Python environment, you can install it in editable mode instead:

```bash
pip install -e .
```

## Common REPL Commands

- `/help`: list the built-in commands
- `/memory`: view the distilled working memory
- `/session`: show the current session file path
- `/reset`: clear the current session state
- `/exit` or `/quit`: leave the REPL

## Safety and Persistence

`pico` does not enable every action by default. High-risk operations such as shell execution and file writes are governed by the approval mode:

- `--approval ask`
- `--approval auto`
- `--approval never`

After each run, the following files are written to `.pico/runs/<run_id>/`:

- `task_state.json`
- `trace.jsonl`
- `report.json`

By default these stay on your local machine.
