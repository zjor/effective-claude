---
name: index-file
description: Indexes a file by optionally moving it from an Inbox folder to a destination, reading its content, generating a summary in .index/<filename>.md, and appending a short snippet to CLAUDE.md in the same folder. Use for organizing and enabling semantic search over documents, PDFs, invoices, notes, and other files.
argument-hint: [filepath] [destination]
allowed-tools: Bash, Read, Write, Glob, Edit
---

Index a file: read its content, generate a summary, and create index artifacts in the file's folder.

## Arguments

`$ARGUMENTS` may contain:
- nothing — ask the user which file to index
- `<filepath>` — index the specified file in place (unless it's in an Inbox folder)
- `<filepath> <destination>` — move the file to destination, then index it there

---

## Step 1: Resolve the target file

If no filepath was provided in `$ARGUMENTS`, ask the user:
> Which file would you like to index?

---

## Step 2: Check for Inbox

Check whether any component of the file's current path is a folder named `inbox` (case-insensitive).

- **If yes (Inbox file):** ask the user for the destination folder (unless already provided as the second argument).
  - Move the file to the destination folder before proceeding.
  - All further steps operate on the file at its new location.
- **If no:** proceed with the file in its current location. No moving needed.

---

## Step 3: Read and understand the file

Read the file content. Identify:
- What kind of document it is (report, article, code, notes, invoice, etc.)
- Its main topic and key points
- Any important metadata (date, author, subject, etc.)

---

## Step 4: Create `.index/` directory if needed

In the folder where the file now lives, check for a `.index/` subdirectory.
If it does not exist, create it.

---

## Step 5: Write the summary to `.index/<filename>.md`

Create (or overwrite) `.index/<original-filename>.md` with a structured summary:

```
# <Original Filename>

**Type:** <document type>
**Date indexed:** <today's date>

## Summary

<3–6 sentence summary capturing the main content, purpose, and key points>

## Key Points

- <bullet 1>
- <bullet 2>
- ...
```

Keep it informative but concise — this is a reference document.

---

## Step 6: Update `CLAUDE.md` in the file's folder

Check if `CLAUDE.md` exists in the file's folder.
- If not, create it with a header:

```markdown
# Folder Index
```

Append the following entry to `CLAUDE.md` (do not duplicate if the file was already indexed):

```markdown
## <original-filename>

<One to two sentence description — shorter than the summary. Captures what the file is and why it matters.>
```

If an entry for this filename already exists in `CLAUDE.md`, replace it with the updated snippet.

---

## Step 7: Confirm to the user

Report what was done:
- File location (original → new, if moved)
- Path to the summary file created in `.index/`
- Whether `CLAUDE.md` was created or updated
