---
description: Audit the user-level ~/.claude/CLAUDE.md and ~/.claude/context/ for bloat, duplication, staleness, and broken pointers.
---

Run a health check on the user's global Claude Code context layer.

## Checks

1. **CLAUDE.md length** — report line count and character count of `~/.claude/CLAUDE.md`. Flag if it exceeds ~200 lines or contains topic-specific reference material that belongs in `~/.claude/context/`.

2. **Context directory inventory** — list every file in `~/.claude/context/` with line counts. Flag files under 5 lines (probable stubs) and files over 300 lines (candidates to split further).

3. **Pointer table sync** — compare the `| File | Contents |` table at the top of `~/.claude/CLAUDE.md` against the actual files in `~/.claude/context/`. Report:
   - Files listed in the table but missing on disk
   - Files on disk but missing from the table
   - Descriptions that look stale relative to file contents

4. **Duplication scan** — look for content in `~/.claude/CLAUDE.md` that is already covered by a file in `~/.claude/context/`. Flag obvious duplication.

5. **Memory index** — check `~/.claude/projects/-home-daniel/memory/MEMORY.md` line count. Flag if over 150 lines (the system truncates after 200).

## Report format

Give a concise punch list:

```
CLAUDE.md:        <lines> lines — <verdict>
context/:         <N> files, <total> lines
Pointer table:    <in sync | drift detected>
Duplication:      <none | issues>
MEMORY.md:        <lines> lines — <verdict>

Recommendations:
- <specific actionable item>
```

Do not modify anything — this is read-only. If action is warranted, suggest running `/user-context-file:chunk-user-claude` or point at the specific file to edit.
