---
description: Edit or create a file in ~/.claude/context/, keeping the CLAUDE.md pointer table in sync.
argument-hint: <context-file-name> [instruction]
---

Edit or create `~/.claude/context/$1`.

Treat the user's instruction in `$2` (and any additional args) as the change to apply.

## Workflow

1. If the target file exists, read it first. Apply the requested change as a focused edit — do not rewrite unrelated sections.
2. If the file does not exist, create it. Use a descriptive header and prose that matches the style of neighbouring files in `~/.claude/context/`.
3. After the edit, check the `| File | Contents |` pointer table at the top of `~/.claude/CLAUDE.md`:
   - If the file is new, add a row for it.
   - If the file's contents meaningfully changed scope, update the description column.
   - If neither applies, leave the table alone.
4. Report what changed in the context file and whether the pointer table was updated.

Do not commit — `~/.claude/` is not a git repo by default on the user's machine.
