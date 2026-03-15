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

### Hooks

| Event | Action |
|-------|--------|
| `PostToolUse` (Edit/Write) | Auto-format code files after modification |

### Documentation Structure Created by `/init-project`

```
project/
├── CLAUDE.md                    # Agent instructions
├── AGENTS.md                    # Cross-agent entry point
├── PLAN.md                      # Task checklist by phase
├── PROGRESS.md                  # Completion log, status, agent handoff
├── README.md                    # Minimal project description
├── .claude/rules/               # Development rules
│   ├── commit-rules.md
│   ├── code-style.md
│   ├── architecture.md
│   ├── testing.md
│   └── pitfalls.md
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

### Workflow

1. **Session start:** Agent reads PLAN.md → PROGRESS.md
2. **During work:** Use `/new-feature` or `/bug-report` to track work
3. **Research:** Use `/research` to check existing references first
4. **After work:** Use `/update-docs` to sync tracking files
5. **Commit:** Follow Conventional Commits format

## Installation

```bash
# From local directory
claude plugin install /path/to/claude-project-starter

# From GitHub (after publishing)
# claude plugin install project-starter@your-marketplace
```

## Usage

After installing, start a new project:

```
/init-project my-app
```

The skill will ask about your tech stack, architecture, and generate all project files accordingly.
