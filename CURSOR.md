# Using this repo with Cursor

This project includes a **Cursor project rule** and a **reusable Agent Skill** so battle-tested engineering guidelines work in Cursor.

## Recommended: on-demand Agent Skill

Copy the skill into your personal skills directory so Cursor loads it when relevant (code review, refactors, tests, UI work):

```bash
cp -r skills/battle-tested-engineer ~/.cursor/skills/
```

The agent discovers skills from `description` in [`skills/battle-tested-engineer/SKILL.md`](skills/battle-tested-engineer/SKILL.md). Ultra-terse caveman style applies during code work, not every conversation.

## Optional: always-apply project rule

If you want these guidelines in **every** session (including caveman output style), copy the rule into a project:

```bash
mkdir -p /path/to/your-project/.cursor/rules
cp .cursor/rules/battle-tested-engineer.mdc /path/to/your-project/.cursor/rules/
```

Confirm under **Settings → Rules** that `battle-tested-engineer` appears.

**Tradeoff:** always-apply changes communication style globally. Most users should prefer the on-demand skill above.

## In this repository

1. Open the folder in Cursor.
2. The committed rule [`.cursor/rules/battle-tested-engineer.mdc`](.cursor/rules/battle-tested-engineer.mdc) has `alwaysApply: true`, so guidelines apply automatically when you work here.
3. You can disable or remove that rule locally if you only want on-demand behavior.

## Other tools

If a stack only supports a root instruction file, copy [`CLAUDE.md`](CLAUDE.md) or [`AGENTS.md`](AGENTS.md) into that project instead (or merge with existing instructions).

## Claude Code vs Cursor

- **Claude Code:** Install via the plugin marketplace and [`README.md`](README.md) instructions; the plugin exposes the skill from this repo. Per-project use can also rely on `CLAUDE.md`.
- **Cursor:** Use the on-demand skill (recommended) or the committed `.cursor/rules/` file. Cursor does not read `.claude-plugin/` or `CLAUDE.md` by default.

## For contributors

When you change the principles, keep these files in sync:

- [`skills/battle-tested-engineer/SKILL.md`](skills/battle-tested-engineer/SKILL.md) (canonical)
- [`CLAUDE.md`](CLAUDE.md)
- [`AGENTS.md`](AGENTS.md)
- [`.cursor/rules/battle-tested-engineer.mdc`](.cursor/rules/battle-tested-engineer.mdc)
