# Agent Skills

Three standalone skills for AI coding agents: one generic engineering skill and two Go-specific reliability skills.

### Generic

| Skill | Use it for |
|---|---|
| [Battle Tested Engineer](skills/battle-tested-engineer/SKILL.md) | General code changes, reviews, tests, and frontend work across languages |

### Golang

| Skill | Use it for |
|---|---|
| [Go HTTP Server Reliability](skills/go-http-server-reliability/SKILL.md) | Building, changing, or reviewing Go HTTP servers |
| [Go TCP Server Reliability](skills/go-tcp-server-reliability/SKILL.md) | Building, changing, or reviewing Go TCP servers |

Run the commands from the repository root. Copy all three skills, or replace `skills/*` with a single skill folder.

## Setup

### Global setup

Skills are available across your projects when installed in your user-level skills directory.

| Agent | Install location |
|---|---|
| Claude Code | `~/.claude/skills/` |
| Codex | `~/.agents/skills/` |
| OpenCode | `~/.config/opencode/skills/` or `~/.agents/skills/` |
| Cursor | `~/.cursor/skills/` or `~/.agents/skills/` |

For example, to install all skills for Claude Code:

```bash
mkdir -p ~/.claude/skills
cp -R skills/* ~/.claude/skills/
```

Alternatively, Claude Code users can install the plugin globally:

```text
/plugin marketplace add sayeed1999/agent-skills
/plugin install agent-skills@agent-skills
```

### Project-specific setup

Install skills in your project when they should only be available there.

| Agent | Project install location |
|---|---|
| Claude Code | `.claude/skills/` |
| Codex | `.agents/skills/` |
| OpenCode | `.opencode/skills/` or `.agents/skills/` |
| Cursor | `.cursor/skills/` or `.agents/skills/` |

For example, to install all skills for Cursor in the current project:

```bash
mkdir -p .cursor/skills
cp -R skills/* .cursor/skills/
```

To install one skill only, replace `skills/*` in either example with its folder, such as `skills/go-http-server-reliability`.

## License

MIT
