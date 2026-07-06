# Battle Tested Engineer

Reusable agent skills for battle-tested engineering judgment — least code, fix the problem, don't break what works. Works with Claude Code, Cursor, and Codex.

## What it does

Nine principles for writing, reviewing, and refactoring code — plus an ultra-terse "caveman" communication style during code work (code, commits, and PR descriptions stay normal prose).

| Principle | Addresses |
|-----------|-----------|
| **Think before code** | Wrong assumptions, hidden confusion |
| **Simplicity** | Over-engineering, speculative abstractions |
| **Surgical change** | Drive-by refactors, orthogonal edits |
| **Data vs UI** | Components owning data, scattered loading state |
| **Goal-driven execution** | Vague tasks without verifiable success criteria |
| **Tests** | Bloated test suites, testing internals |
| **Propose spec when need** | Ambiguous requirements, wide blast radius |
| **Ship then improve** | Premature optimization, big-bang refactors |
| **Gut-check before output** | Silent over-build, under-delivered quality |

## Install

| Tool | Method | Recommended? |
|------|--------|--------------|
| **Cursor** | Copy `skills/battle-tested-engineer/` to `~/.cursor/skills/` | Yes (on-demand) |
| **Cursor** | Copy `.cursor/rules/battle-tested-engineer.mdc` to project `.cursor/rules/` | Optional (always-on) |
| **Claude Code** | Plugin marketplace (see below) | Yes (global) |
| **Claude Code** | `curl` `CLAUDE.md` into project root | Per-project |
| **Codex** | Copy skill to `~/.codex/skills/` or `.agents/skills/` | Yes (on-demand) |
| **Codex** | `curl` `AGENTS.md` into project root | Per-project |

### Claude Code — Plugin (recommended)

From within Claude Code, add the marketplace:

```
/plugin marketplace add sayeed1999/agent-skills
```

Then install:

```
/plugin install agent-skills@agent-skills
```

### Claude Code — Per-project CLAUDE.md

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
└── CODEX.md                 # Codex setup guide
```

## License

MIT
