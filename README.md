# User-Claude-MD

Claude Code plugin for managing the **user-level** `~/.claude/CLAUDE.md` and its chunked context directory (`~/.claude/context/`).

Part of the [danielrosehill Claude Code marketplace](https://github.com/danielrosehill/Claude-Code-Plugins).

## The pattern

`~/.claude/CLAUDE.md` is loaded into every Claude Code session — so it needs to stay lean. This plugin supports a split where:

- `~/.claude/CLAUDE.md` is a short index: identity, working-style preferences, and a pointer table.
- `~/.claude/context/*.md` holds topic-specific reference material, loaded on demand.

That keeps the always-on context small (token-efficient) while preserving deep reference material for when it's actually needed.

## Commands (`/user-claude-md:<name>`)

- `chunk-user-claude` — prune `~/.claude/CLAUDE.md` and push supplementary sections into the right file under `~/.claude/context/`.
- `user-claude-health` — audit the layout: CLAUDE.md size, pointer-table drift, context-file inventory, duplication, MEMORY.md size.
- `list-user-context` — list every file in `~/.claude/context/` with line counts and summaries.
- `edit-user-context <file> <instruction>` — targeted edit (or create) a context file, keeping the CLAUDE.md pointer table in sync.

## Skills

- `user-claude-md-reference` — auto-loaded reference for the split structure; invoked when an agent needs to reason about where a piece of global user context belongs.

## Installation

```bash
claude plugins install user-context-file@danielrosehill
```

## Lineage

Adapts the chunking/health patterns from [Claude-Meta-Tools-Plugin](https://github.com/danielrosehill/Claude-Meta-Tools-Plugin), redirecting them from repo-level `CLAUDE.md` to the user-level install.

## License

MIT
