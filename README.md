# Claude Project Starter Plugin

A Claude Code plugin that provides standard project documentation structure, tracking workflow, and development automation.

## What's Included

### Skills

| Skill | Description |
|-------|-------------|
| `/init-project` | Bootstrap a new project with docs structure, rules, and tracking files |
| `/new-feature` | Create FEAT issue file and update PLAN.md |
| `/bug-report` | Create BUG issue file |
| `/research` | Check existing references before web searching |
| `/update-docs` | Sync PLAN.md and PROGRESS.md after work |
| `/review-architecture` | Verify code compliance with architecture rules |

### Rules

| Rule | Description |
|------|-------------|
| `commit-rules.md` | Conventional Commits format, atomic commit guidelines |

### Hooks

| Event | Action |
|-------|--------|
| `PostToolUse` (Edit/Write) | Auto-format code files after modification |

Supported languages: Dart, JS/TS, Python, Go, Rust

### Documentation Structure Created by `/init-project`

```
project/
├── CLAUDE.md                    # Agent instructions
├── AGENTS.md                    # Cross-agent entry point
├── PLAN.md                      # Task checklist by phase
├── PROGRESS.md                  # Current status and agent handoff (slim)
├── README.md                    # Minimal project description
├── .claude/rules/               # Development rules
│   ├── commit-rules.md          #   Conventional Commits + project scopes
│   ├── code-style.md            #   Lint, naming, formatting, comment guidelines
│   ├── architecture.md          #   Architecture pattern, folder structure, layer rules
│   ├── testing.md               #   Test strategy and conventions
│   └── pitfalls.md              #   Mistake prevention log
└── docs/
    ├── INDEX.md                 # Central document map
    ├── planning/
    │   └── CHANGELOG_PLANNING.md
    ├── adr/                     # Architecture Decision Records
    ├── issues/
    │   └── TEMPLATE.md          # FEAT/BUG issue template
    ├── references/              # Research materials
    ├── guides/
    │   └── ONBOARDING.md
    ├── tips/                    # Practical knowledge
    └── conversations/
        └── LOG.md               # User request log
```

### Key Conventions

- **PROGRESS.md:** Keep only recent 2-3 sessions. Older history lives in git log.
- **Code Reuse:** CLAUDE.md includes instructions for agents to search existing code before writing new utilities.
- **Comments:** code-style.md includes comment guidelines with detail levels (Why > What > None).
- **Pitfalls:** pitfalls.md starts with common agent mistakes and grows with project experience.

### Workflow

1. **Session start:** Agent reads PLAN.md → PROGRESS.md
2. **During work:** Use `/new-feature` or `/bug-report` to track work
3. **Research:** Use `/research` to check existing references first
4. **Before commit:** Use `/review-architecture` to verify compliance
5. **After work:** Use `/update-docs` to sync tracking files
6. **Commit:** Follow Conventional Commits format

## Installation

```bash
# 1. Add marketplace
/plugin marketplace add luckyhyom/claude-project-starter

# 2. Install plugin
/plugin install project-starter@luckyhyom-claude-project-starter
```

## Usage

After installing, start a new project:

```
/init-project my-app
```

The skill will ask about your tech stack, architecture, and generate all project files accordingly.

## Changelog

### v1.1.0 (2026-03-17)

- **New skill:** `/review-architecture` — verify code compliance with architecture rules
- **New rule:** `commit-rules.md` — Conventional Commits included in plugin
- **Enhanced:** `/init-project` — code-style.md now includes comment guidelines (Why/What/None levels), pitfalls.md starts with common entries, CLAUDE.md includes code reuse section
- **Enhanced:** `/update-docs` — PROGRESS.md slim structure (keep 2-3 recent sessions only)
- **Enhanced:** README — added key conventions section and workflow update
