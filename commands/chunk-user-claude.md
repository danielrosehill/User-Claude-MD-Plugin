---
description: Prune the user-level ~/.claude/CLAUDE.md and offload supplementary sections into ~/.claude/context/ files.
---

Review the user's global CLAUDE.md at `~/.claude/CLAUDE.md`.

The goal is to keep that file lean — containing only the essentials an AI agent needs to establish foundational context about the user — and to move supplementary material into the existing `~/.claude/context/` directory, which is already the canonical location for split-out context files.

## Prune

Reduce `~/.claude/CLAUDE.md` to the minimum length needed for an agent to understand:

- Who the user is (name, role, location, core identity)
- The machine and environment context (one or two lines)
- Working-style preferences that apply to every session (autonomy level, communication style, input-method quirks)
- A pointer table to `~/.claude/context/` for everything else

Remove anything that is topic-specific, reference-style, or only relevant occasionally. That content belongs in `~/.claude/context/`, not inline.

## Nest

For each section removed, find the appropriate existing file in `~/.claude/context/` (e.g. `system-environment.md`, `development-environment.md`, `mcp-usage.md`, `preferences.md`, `git-rules.md`, `tools.md`, `troubleshooting.md`, `auth-and-security.md`, `contacts.md`, `file-organization.md`, `media-tools.md`).

- If a suitable file exists, append the removed content there.
- If no suitable file exists, create a new one with a descriptive kebab-case filename.
- Do **not** duplicate content that is already in a context file — prefer deletion from CLAUDE.md over duplication.

## Update CLAUDE.md

Ensure the pruned CLAUDE.md ends with the context directory pointer table (the existing `| File | Contents |` table) so agents know where to look. Regenerate the table if new context files were added.

## Report

Summarise: lines removed, files touched in `~/.claude/context/`, and the new total length of CLAUDE.md. Do not commit — the user's global `~/.claude/` is not a git repo by default.
