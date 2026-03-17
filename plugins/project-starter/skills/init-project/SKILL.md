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
PROGRESS.md        — Agent handoff notes, current status, recent 2-3 sessions only
README.md          — Minimal project description with links to docs/
blog/              — Deep-dive posts on specific topics (written on user request only)
daily/             — Human-readable daily work reports (TIL, decisions, file map)
```

**CLAUDE.md must include:**
- Session startup rule: read PLAN.md → PROGRESS.md before starting work
- Documentation language rules
- Commit workflow (update PROGRESS.md on every commit, mark PLAN.md tasks)
- Link to docs/INDEX.md and .claude/rules/
- **Code Reuse section:** instruct agents to search existing code before writing new helpers/utilities. List the project's key directories for shared code (e.g., utils, shared models, shared repositories).
- **PROGRESS.md guidance:** keep only recent 2-3 sessions; older history lives in git log

### 3. Create documentation structure

```
blog/                           — Deep-dive posts (user request only)
daily/                          — Daily work reports for human review
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

**daily/ report template:**

```markdown
# YYYY-MM-DD — Title

## One-line summary

## Work done
(Grouped by commit or logical unit)

## Key decisions
(Table: decision | reason)

## Changed files
(File map with annotations)

## TIL
(2-3 key learnings from today)

## Next
(What to do next)
```

**blog/ vs daily/ distinction:**
- `daily/` — every work session, holistic summary, human-readable review
- `blog/` — specific topic deep-dive, only when user explicitly requests

### 4. Create development rules

Based on tech stack answers, generate:

```
.claude/rules/
├── commit-rules.md       — Conventional Commits (extend user-level with project scopes)
├── code-style.md         — Language-specific lint, naming, formatting, comment guidelines
├── architecture.md       — Architecture pattern, folder structure, layer rules
├── testing.md            — Test strategy, conventions, what to test
└── pitfalls.md           — Mistake prevention log with starter entries
```

**For code-style.md, ask or infer:**
- Linter (e.g., very_good_analysis for Dart, eslint for JS/TS)
- Formatter and line length
- Naming conventions for the language
- **Comment guidelines must include:**
  - Comment language (match project's primary language)
  - Detail levels: **Why** (default — design decisions, trade-offs) > **What** (framework magic not readable from code) > **None** (self-explanatory code)
  - Doc comments (`///` or `/** */`) for public API (classes, methods, fields)
  - Inline comments for implementation details
  - Section dividers format (if applicable)
  - What NOT to comment (obvious code, simple getters, commented-out code)

**For architecture.md, ask or infer:**
- Architecture pattern (MVVM, MVC, Clean Architecture, etc.)
- Folder structure (feature-first vs layer-first)
- State management (if applicable)

**For pitfalls.md, include these starter entries:**

```markdown
# Pitfalls

> Known mistakes and rules to prevent them. Add new entries when mistakes are discovered.

## DON'T: Delete user-created files without asking
- **Rule:** Never delete files the user created, even if empty. Ask first.

## DON'T: Modify documents without explaining changes first
- **Rule:** Summarize all planned changes and get approval before writing.

## DO: Record progress before ending a session
- **Rule:** Update PROGRESS.md even without code commits when significant
  decisions are made or work context changes.
```

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
