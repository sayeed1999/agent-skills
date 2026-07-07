# Battle Tested Engineer

**Instructions for your AI coding agent** — not a library you import or an app you run.

This repo teaches your AI agent how to write and review code: ask before guessing, change only what was asked, prefer simple fixes over big refactors, and ship a working minimal version first.

Supported by Claude, Cursor, Codex, Gemini and 15+ AI agents.

This work was shaped by knowledge from two earlier skill repositories: [andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) and [caveman](https://github.com/JuliusBrussee/caveman/blob/main/skills/caveman/SKILL.md).

## Quick Start Guide

1. Clone this repo:
  ```bash
    git clone https://github.com/sayeed1999/agent-skills.git
    cd agent-skills
  ```

2. Copy the skill into your agent skills dir:

  **User-wide:**
  ```bash
  mkdir -p ~/.agents/skills
  cp -r skills/battle-tested-engineer ~/.agents/skills/
  ```

  **Project-scoped:**
  ```bash
    mkdir -p .agents/skills
    cp -r skills/battle-tested-engineer .agents/skills/
  ```

3. In your AI agent, try a real prompt — e.g., 
  ```bash
  /battle-tested-engineer explain the codebase
  ```

That's it!

## What it does

Nine principles for writing, reviewing, and refactoring code — plus an ultra-terse "caveman" communication style during code work (code, commits, and PR descriptions stay normal prose).


| Principle                   | Addresses                                       |
| --------------------------- | ----------------------------------------------- |
| **Think before code**       | Wrong assumptions, hidden confusion             |
| **Simplicity**              | Over-engineering, speculative abstractions      |
| **Surgical change**         | Drive-by refactors, orthogonal edits            |
| **Data vs UI**              | Components owning data, scattered loading state |
| **Goal-driven execution**   | Vague tasks without verifiable success criteria |
| **Tests**                   | Bloated test suites, testing internals          |
| **Propose spec when need**  | Ambiguous requirements, wide blast radius       |
| **Ship then improve**       | Premature optimization, big-bang refactors      |
| **Gut-check before output** | Silent over-build, under-delivered quality      |




## Install


| Tool            | Method                                                                            | Recommended?         |
| --------------- | --------------------------------------------------------------------------------- | -------------------- |
| **Any agent**   | Copy `skills/battle-tested-engineer/` to `~/.agents/skills/` or `.agents/skills/` | Yes (on-demand)      |
| **Cursor**      | Copy `skills/battle-tested-engineer/` to `~/.cursor/skills/`                      | Yes (on-demand)      |
| **Cursor**      | Copy `.cursor/rules/battle-tested-engineer.mdc` to project `.cursor/rules/`       | Optional (always-on) |
| **Claude Code** | Plugin marketplace (see below)                                                    | Yes (global)         |
| **Claude Code** | `curl` `CLAUDE.md` into project root                                              | Per-project          |
| **Codex**       | Copy skill to `~/.codex/skills/` or `.agents/skills/`                             | Yes (on-demand)      |
| **Codex**       | `curl` `AGENTS.md` into project root                                              | Per-project          |




### Generic — `.agents` (any agent)

User-wide:

```bash
mkdir -p ~/.agents/skills
cp -r skills/battle-tested-engineer ~/.agents/skills/
```

Project-scoped:

```bash
mkdir -p .agents/skills
cp -r skills/battle-tested-engineer .agents/skills/
```



### Claude Code — Plugin (recommended)

From within Claude Code, add the marketplace:

```
/plugin marketplace add sayeed1999/agent-skills
```

Then install:

```
/plugin install agent-skills@agent-skills
```



### Claude Code — Per-project [CLAUDE.md](http://CLAUDE.md)

New project:

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/sayeed1999/agent-skills/main/CLAUDE.md
```

Existing project (append):

```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/sayeed1999/agent-skills/main/CLAUDE.md >> CLAUDE.md
```



### Cursor — On-demand skill (recommended)

```bash
cp -r skills/battle-tested-engineer ~/.cursor/skills/
```

See [CURSOR.md](CURSOR.md) for always-apply rule setup and tradeoffs.

### Codex — On-demand skill (recommended)

Global:

```bash
cp -r skills/battle-tested-engineer ~/.codex/skills/
```

Repo-scoped:

```bash
mkdir -p .agents/skills
cp -r skills/battle-tested-engineer .agents/skills/
```

See [CODEX.md](CODEX.md) for `AGENTS.md` per-project install.

## How to use it

After install, you do not invoke the skill manually. Just open a project and talk to your agent as usual.

1. **Install** using one of the methods in [Install](#install) above (pick your tool; on-demand skill is recommended).
2. **Open a codebase** in Cursor, Claude Code, or Codex.
3. **Ask for work** the way you already would — e.g. "fix the login 500", "review this diff", "add tests for checkout", "refactor this component".
4. **Let the agent apply the guidelines** — it should clarify ambiguous asks, keep diffs small, and write minimal code. See [EXAMPLE.md](EXAMPLE.md) for good vs bad behavior.

**On-demand skill:** loaded when the task fits (refactor, review, tests, UI). General questions may not trigger it.

**Always-on rule or** `CLAUDE.md` **/** `AGENTS.md`**:** guidelines apply every message in that project, including ultra-terse style during code work.

**Optional:** merge project-specific rules into the same files (see [Customization](#customization)).

## How to know it's working

- Fewer unnecessary changes in diffs — only requested changes appear
- Clarifying questions come before implementation, not after mistakes
- Characterization tests before risky behavior changes
- Terse responses during code work; normal prose for commits and PRs
- Clean, minimal PRs — no drive-by refactoring



## Customization

These guidelines merge with project-specific instructions. Add sections like:

```markdown
## Project-Specific Guidelines

- Use TypeScript strict mode
- All API endpoints must have tests
- Follow error handling in `src/utils/errors.ts`
```



## Tradeoff note

These guidelines bias toward **caution over speed**. Ultra-terse output style is opt-in via the on-demand skill; it is not forced unless you install the always-apply Cursor rule or per-project `CLAUDE.md` / `AGENTS.md`.

For trivial tasks (typo fixes, obvious one-liners), use judgment — not every change needs full rigor.

## Repository structure

```text
agent-skills/
├── .claude-plugin/          # Claude Code plugin manifests
├── .cursor/rules/           # Optional always-apply Cursor rule
├── skills/                  # Canonical skill definitions
│   └── battle-tested-engineer/
│       └── SKILL.md
├── CLAUDE.md                # Claude Code per-project install
├── AGENTS.md                # Codex per-project install
├── CURSOR.md                # Cursor setup guide
├── CODEX.md                 # Codex setup guide
└── EXAMPLE.md               # Good vs bad agent behavior
```



## License

MIT