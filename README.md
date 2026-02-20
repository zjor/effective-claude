# effective-claude

A personal marketplace of Claude Code plugins — slash commands, skills, and agents for personal productivity.

Each plugin lives in its own directory and can be installed independently by copying its `.claude/commands/` contents into your project or global `~/.claude/commands/` folder.

## Plugins

### [file-indexer](./file-indexer/README.md)

Indexes files by generating AI summaries and maintaining a lightweight catalog alongside your files. Supports moving files out of an Inbox folder, creating `.index/<filename>.md` summaries, and keeping a `CLAUDE.md` snippet index in each folder.

```
/index-file path/to/file.pdf
/index-file Inbox/report.pdf ~/Docs/
```

## Installation via marketplace

This repository is a Claude Code plugin marketplace. Add it once and install individual plugins on demand.

**Step 1 — Add the marketplace** (requires Claude Code ≥ 1.0.33):

```
/plugin marketplace add zjor/effective-claude
```

**Step 2 — Install a plugin:**

```
/plugin install file-indexer@effective-claude
```

Plugin commands are namespaced by plugin name, so `file-indexer` provides `/file-indexer:index-file`.

### Manual installation (alternative)

If you prefer to install without the marketplace system, copy the commands folder directly:

```bash
# For a single project
cp -r file-indexer/.claude/commands/ .claude/commands/

# Globally (available in all projects)
cp -r file-indexer/.claude/commands/ ~/.claude/commands/
```

With manual installation, commands are available without namespacing (e.g. `/index-file` instead of `/file-indexer:index-file`).
