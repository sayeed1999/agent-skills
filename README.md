# Agent Skills

Three reusable skills for AI coding agents:

| Skill | What it helps with |
|---|---|
| `battle-tested-engineer` | General code changes, reviews, tests, and frontend work |
| `go-http-server-reliability` | Building, changing, or reviewing Go HTTP servers |
| `go-tcp-server-reliability` | Building, changing, or reviewing Go TCP servers |

## Install without cloning

The easiest way to install these skills is with the `skills` command-line tool. You do **not** need to clone or download this repository.

### 1. Install Node.js

Install **Node.js 22.20 or newer** from [nodejs.org](https://nodejs.org/). This includes `npx`, which runs the installer.

### 2. Open a terminal

Open Terminal on macOS or Linux, or PowerShell on Windows. To install globally for Claude Code, OpenCode, and Cursor, run:

```bash
npx skills add sayeed1999/agent-skills --global --agent claude-code opencode cursor
```

The installer downloads the skills from GitHub and puts them in each agent's user-level skills folder. To install for just one agent, pass only its name after `--agent`, such as `--agent claude-code`.

To install into the current project only, open a terminal in that project folder and run the same command **without** `--global`:

```bash
npx skills add sayeed1999/agent-skills
```

### Install just one skill

Add `--skill` with the skill name. For example, to install only the general engineering skill globally:

```bash
npx skills add sayeed1999/agent-skills --skill battle-tested-engineer --global --agent claude-code opencode cursor
```

Replace `battle-tested-engineer` with `go-http-server-reliability` or `go-tcp-server-reliability` to install a Go skill instead.

### Check or update installed skills

```bash
npx skills list
npx skills check
npx skills update
```

See the [`skills` CLI guide](https://skills.sh/docs/cli) for more options and supported agents.

## Install directly with curl (no Node.js)

You can download the skill files straight from GitHub without cloning this repository or installing Node.js. These are global skill folders for the main supported agents:

| Agent | Global skills folder |
|---|---|
| Claude Code | `~/.claude/skills/` |
| OpenCode | `~/.config/opencode/skills/` or `~/.agents/skills/` |
| Cursor | `~/.cursor/skills/` |
| Codex and other supported agents | Check the [`skills` CLI agent list](https://github.com/vercel-labs/skills/blob/main/docs/agents.md) |

### macOS, Linux, or Git Bash

To install one skill for Claude Code, run this one-line command:

```bash
mkdir -p "$HOME/.claude/skills/battle-tested-engineer" && curl -fsSL "https://raw.githubusercontent.com/sayeed1999/agent-skills/main/skills/battle-tested-engineer/SKILL.md" -o "$HOME/.claude/skills/battle-tested-engineer/SKILL.md"
```

To install only the Go HTTP skill in Claude Code:

```bash
mkdir -p "$HOME/.claude/skills/go-http-server-reliability" && curl -fsSL "https://raw.githubusercontent.com/sayeed1999/agent-skills/main/skills/go-http-server-reliability/SKILL.md" -o "$HOME/.claude/skills/go-http-server-reliability/SKILL.md"
```

To install for OpenCode or Cursor instead, replace `~/.claude/skills` in the command with `~/.config/opencode/skills` or `~/.cursor/skills`. OpenCode also supports `~/.agents/skills`. To install the Go TCP skill, replace `go-http-server-reliability` in both paths with `go-tcp-server-reliability`.

To install all three skills for Claude Code:

```bash
skills_dir="$HOME/.claude/skills"

for skill in battle-tested-engineer go-http-server-reliability go-tcp-server-reliability; do
  mkdir -p "$skills_dir/$skill"
  curl -fsSL "https://raw.githubusercontent.com/sayeed1999/agent-skills/main/skills/$skill/SKILL.md" \
    -o "$skills_dir/$skill/SKILL.md"
done
```

To update a direct install later, run the matching commands again.

## Skills

- [Battle Tested Engineer](skills/battle-tested-engineer/SKILL.md)
- [Go HTTP Server Reliability](skills/go-http-server-reliability/SKILL.md)
- [Go TCP Server Reliability](skills/go-tcp-server-reliability/SKILL.md)

## License

MIT
