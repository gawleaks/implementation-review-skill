# Implementation Review Skill

Probe changes against codebase ground truth — finds gaps, pattern violations, and missing pieces in implemented features. Works with VS Code Copilot, Claude Code, and any agent that loads `.agents/skills/`.

## What it does

Instead of nitpicking style, this skill examines changes through five structural lenses:

- **Pattern conformance** — does the change follow the codebase's established conventions?
- **Domain fidelity** — does it use the domain vocabulary correctly?
- **Completeness** — what's missing? (tests, types, error paths, migrations)
- **Contract integrity** — does it honour contracts with adjacent code?
- **Regression surface** — could it break existing behaviour?

Findings are reported as **Gap** (missing), **Violation** (contradicts), or **Risk** (fragile).

## Install

### Skill (required — powers everything)

**User-level** (all projects):

```sh
mkdir -p ~/.agents/skills/implementation-review
cp implementation-review/SKILL.md ~/.agents/skills/implementation-review/
```

**User-level for Claude Code:**

```sh
mkdir -p ~/.claude/skills/implementation-review
cp implementation-review/SKILL.md ~/.claude/skills/implementation-review/
```

**Project-level** (team-shared, commit to repo):

```sh
mkdir -p .agents/skills/implementation-review
cp implementation-review/SKILL.md .agents/skills/implementation-review/
```

**Project-level for Claude Code:**

```sh
mkdir -p .claude/skills/implementation-review
cp implementation-review/SKILL.md .claude/skills/implementation-review/
```

### VS Code Copilot prompts (optional)

```sh
# macOS
cp prompts/*.prompt.md ~/Library/Application\ Support/Code/User/prompts/

# Linux
cp prompts/*.prompt.md ~/.config/Code/User/prompts/

# Project-level
cp prompts/*.prompt.md .github/prompts/
```

### Claude Code commands (optional)

```sh
# User-level
cp commands/*.md ~/.claude/commands/

# Project-level
cp commands/*.md .claude/commands/
```

## Usage

### Slash commands

| Command | What it does |
|---------|-------------|
| `/review-changes` | Review uncommitted diff |
| `/review-commit` | Review last commit (accepts range like `HEAD~3..HEAD`) |
| `/review-design` | Architectural review of a module |
| `/review-completeness` | Completeness audit — what's missing |

### Natural language (auto-triggers)

The skill fires automatically when you say things like:

- "review my changes"
- "check this implementation"
- "what's missing from this feature"
- "validate this is complete"

## How it works

1. **Build ground truth** — reads the unchanged codebase to understand its conventions, patterns, and contracts
2. **Scope the change** — enumerates what changed and articulates intent in domain language
3. **Probe** — examines every changed file through every applicable lens
4. **Report** — delivers findings grouped by severity with traceable ground truth references

## Compatibility

| Agent | How it loads |
|-------|-------------|
| VS Code Copilot | Skill auto-detected from `.agents/skills/`; prompts via `/` menu |
| Claude Code | Skill from `.agents/skills/` or `.claude/skills/`; commands via `/review-*` |
| Cursor | Skill from `.agents/skills/` |
| Codex | Skill from `.agents/skills/` |
| Any SKILL.md-compatible agent | Copy `skill/SKILL.md` to the expected skills path |

## License

MIT
