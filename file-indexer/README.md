# file-indexer

A Claude Code plugin that indexes files by generating AI summaries and keeping a lightweight catalog alongside your files.

## What it does

When you run `/index-file`, Claude will:

1. Read and understand the file
2. Create a `.index/<filename>.md` with a structured summary
3. Append a short snippet to `CLAUDE.md` in the same folder

If the file lives in an **Inbox** folder (case-insensitive), Claude will ask where to move it before indexing.

## Installation

Copy `.claude/commands/index-file.md` into your project's `.claude/commands/` folder, or place it in `~/.claude/commands/` to make it available globally.

## Usage

```
/index-file                              # Claude asks which file to index
/index-file path/to/file.pdf            # Index a specific file in place
/index-file Inbox/report.pdf ~/Docs/    # Move from Inbox to destination, then index
```

## Artifacts created

Given a file at `~/Docs/report.pdf`:

```
~/Docs/
  report.pdf
  CLAUDE.md              ← short snippet appended here
  .index/
    report.pdf.md        ← full summary
```

### `.index/report.pdf.md` (summary)

```markdown
# report.pdf

**Type:** Research report
**Date indexed:** 2026-02-20

## Summary

...

## Key Points

- ...
```

### `CLAUDE.md` entry

```markdown
## report.pdf

A Q4 2025 market research report covering competitor analysis and pricing trends.
```
