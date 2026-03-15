---
name: init-project
description: Bootstrap a new project with documentation structure, tracking files, and development rules. Use at the start of any new project.
argument-hint: "[project-name]"
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebSearch, WebFetch
---

# Project Initialization

Set up standard project documentation structure and development workflow.

## Steps

### 1. Gather project info

Ask the user (skip if already provided via `$ARGUMENTS` or conversation context):

- **Project name**
- **Tech stack** (language, framework, database)
- **Platform** (web, mobile, desktop, API)
- **Team size** (solo / small team / large team)

### 2. Create project management files

```
CLAUDE.md          — Agent instructions (session startup, documentation rules, workflow)
AGENTS.md          — Cross-agent entry point referencing CLAUDE.md
PLAN.md            — Task checklist by phase (empty phases)
PROGRESS.md        — Completion log and agent handoff notes (empty template)
README.md          — Minimal project description with links to docs/
```

**CLAUDE.md must include:**
- Session startup rule: read PLAN.md → PROGRESS.md before starting work
- Documentation language rules
- Commit workflow (update PROGRESS.md on every commit, mark PLAN.md tasks)
- Link to docs/INDEX.md and .claude/rules/

### 3. Create documentation structure

```
docs/
├── INDEX.md                    — Central document map
├── planning/
│   └── CHANGELOG_PLANNING.md   — Planning decision history
├── adr/                        — Architecture Decision Records (empty)
├── issues/
│   └── TEMPLATE.md             — Issue template (FEAT/BUG)
├── references/                 — Research materials (empty)
├── guides/
│   └── ONBOARDING.md           — Reading order for newcomers
├── tips/                       — Practical knowledge (empty)
└── conversations/
    └── LOG.md                  — User request log (written on request only)
```

### 4. Create development rules

Based on tech stack answers, generate:

```
.claude/rules/
├── commit-rules.md       — Conventional Commits (extend user-level with project scopes)
├── code-style.md         — Language-specific lint, naming, formatting
├── architecture.md       — Architecture pattern, folder structure, layer rules
├── testing.md            — Test strategy, conventions, what to test
└── pitfalls.md           — Empty template for mistake prevention
```

**For code-style.md, ask or infer:**
- Linter (e.g., very_good_analysis for Dart, eslint for JS/TS)
- Formatter and line length
- Naming conventions for the language

**For architecture.md, ask or infer:**
- Architecture pattern (MVVM, MVC, Clean Architecture, etc.)
- Folder structure (feature-first vs layer-first)
- State management (if applicable)

### 5. Create issue template

Generate `docs/issues/TEMPLATE.md` with:
- Type, Priority, Severity, Status, Created, Resolved, Related
- Context, Steps to Reproduce, Expected vs Actual
- Technical Analysis (affected layer, feature, root cause)
- Security Consideration
- Solution, Test, Takeaway

### 6. Record initial ADR

Create `docs/adr/0001-initial-architecture.md` documenting the chosen architecture and tech stack.

### 7. Report

Show the user:
- List of all created files
- Suggested next steps (e.g., "run flutter create", "npm init", etc.)
- Any decisions that need user input
