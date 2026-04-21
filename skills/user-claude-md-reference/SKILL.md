---
name: user-claude-md-reference
description: Reference for the split structure of the user-level Claude Code context — ~/.claude/CLAUDE.md acts as an index that points at topic files in ~/.claude/context/. Use when editing, auditing, or reasoning about global Claude Code user configuration, or when the user asks where a particular piece of global context lives.
---

# User-level CLAUDE.md layout

The user keeps their global Claude Code context split across two locations:

- `~/.claude/CLAUDE.md` — short index. Identity, working-style preferences, input-method notes, and a pointer table. Should stay lean (ideally under ~200 lines).
- `~/.claude/context/*.md` — one file per topic. Authoritative home for reference-style content.

## Canonical file split

The pointer table in `~/.claude/CLAUDE.md` names each context file and its scope. Typical files:

| File | Purpose |
|------|---------|
| `system-environment.md` | OS, hardware, storage, network, LAN map |
| `development-environment.md` | Languages, tools, containers, git |
| `mcp-usage.md` | Guidance for calling specific MCP servers |
| `mcp-provisioning.md` | Rules for adding new MCP connections |
| `file-organization.md` | Repo layout, scripts, backups, conventions |
| `media-tools.md` | Audio/video/image tooling |
| `troubleshooting.md` | Known-issue playbooks |
| `contacts.md` | Family and joint email addresses |
| `auth-and-security.md` | SSH, GPG, API keys, sudo policy |
| `tools.md` | Preferred CLI tools and utilities |
| `preferences.md` | Locale, naming, formatting conventions |
| `git-rules.md` | Commit/push policy |

Names and exact set may drift — always check the live pointer table.

## When to edit which

- **Working-style feedback that should fire in every session** → inline in `~/.claude/CLAUDE.md`.
- **Topic-specific facts or references** → the matching file in `~/.claude/context/`. Create a new file if none fits.
- **Per-project context** → not here at all; use the project's own CLAUDE.md.
- **Memory-type learnings** → `~/.claude/projects/-home-daniel/memory/` via the auto-memory system, not this layer.

## Keeping the pointer table in sync

Any time a file is added, removed, or meaningfully re-scoped in `~/.claude/context/`, the pointer table at the top of `~/.claude/CLAUDE.md` needs to match. Drift here is the most common bug in this layout.

## Commands provided by this plugin

- `/user-claude-md:chunk-user-claude` — prune CLAUDE.md, push overflow into `context/`.
- `/user-claude-md:user-claude-health` — audit the layout for bloat, drift, and duplication.
- `/user-claude-md:list-user-context` — list context files with summaries.
- `/user-claude-md:edit-user-context <file> <instruction>` — targeted edit, with pointer-table sync.

## Safety

`~/.claude/` is typically not a git repo. These commands do not commit. Before destructive rewrites (e.g. `chunk-user-claude`), consider a manual backup: `cp -r ~/.claude/CLAUDE.md ~/.claude/context ~/.claude/.backup-$(date +%Y%m%d)/`.
