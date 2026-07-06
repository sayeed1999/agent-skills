# Using this repo with Codex

Codex reads project instructions from `AGENTS.md` and discovers skills from skill directories. This repo supports both.

## Recommended: on-demand skill

Copy the skill folder for global use across all repos:

```bash
cp -r skills/battle-tested-engineer ~/.codex/skills/
```

Or install repo-scoped for a single project:

```bash
mkdir -p /path/to/your-project/.agents/skills
cp -r skills/battle-tested-engineer /path/to/your-project/.agents/skills/
```

Codex detects newly installed skills automatically; restart Codex if one does not appear.

The agent loads [`skills/battle-tested-engineer/SKILL.md`](skills/battle-tested-engineer/SKILL.md) when the task matches its description (code review, refactors, tests, UI work).

## Per-project: AGENTS.md

For project-wide behavioral guidelines without a skill install:

**New project:**

```bash
curl -o AGENTS.md https://raw.githubusercontent.com/sayeed1999/agent-skills/main/AGENTS.md
```

**Existing project (append):**

```bash
echo "" >> AGENTS.md
curl https://raw.githubusercontent.com/sayeed1999/agent-skills/main/AGENTS.md >> AGENTS.md
```

Codex concatenates `AGENTS.md` files from the repo root down to your current directory. Merge with project-specific sections as needed.

## Global instructions

You can also place guidelines in `~/.codex/AGENTS.md` for all Codex sessions.

## Codex vs Claude Code vs Cursor

| Tool | Per-project file | Skill location |
|------|------------------|----------------|
| Codex | `AGENTS.md` | `~/.codex/skills/` or `.agents/skills/` |
| Claude Code | `CLAUDE.md` | Plugin or `skills/` via marketplace |
| Cursor | N/A (use rules) | `~/.cursor/skills/` |

See [`README.md`](README.md) for full install options.

## For contributors

When you change the principles, keep these files in sync:

- [`skills/battle-tested-engineer/SKILL.md`](skills/battle-tested-engineer/SKILL.md) (canonical)
- [`AGENTS.md`](AGENTS.md)
- [`CLAUDE.md`](CLAUDE.md)
- [`.cursor/rules/battle-tested-engineer.mdc`](.cursor/rules/battle-tested-engineer.mdc)
