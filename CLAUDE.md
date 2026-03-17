# Claude Project Starter — Claude Code Rules

## Project Overview

Claude Code plugin that provides project scaffolding, documentation workflow, and development automation skills.

- **Type:** Claude Code Plugin (marketplace)
- **Repo:** https://github.com/luckyhyom/claude-project-starter
- **Users:** All projects that install this plugin

## Plugin Structure

```
plugins/project-starter/
├── .claude-plugin/plugin.json   — Plugin metadata and version
├── settings.json                — Default permissions
├── hooks/hooks.json             — Auto-format hook (multi-language)
├── rules/
│   └── commit-rules.md          — Conventional Commits (applied to all projects)
└── skills/
    ├── init-project/            — Bootstrap new project
    ├── new-feature/             — Create FEAT issue
    ├── bug-report/              — Create BUG issue
    ├── research/                — Reference-first research
    ├── update-docs/             — Sync PLAN.md + PROGRESS.md
    ├── review-architecture/     — Architecture compliance check
    └── translate-docs/          — Translation management with commit hash tracking
```

## Plugin Update Process

When a project (e.g., Taptime) discovers improvements to rules, skills, or workflows,
sync them back to this plugin so all future projects benefit.

### Step 1: Identify what to sync

Compare project-level rules with plugin contents:
- `.claude/rules/` (project) vs `plugins/project-starter/rules/` (plugin)
- `.claude/skills/` (project) vs `plugins/project-starter/skills/` (plugin)
- `CLAUDE.md` (project) vs what `/init-project` generates

### Step 2: Classify each improvement

| Category | Action | Example |
|----------|--------|---------|
| **Generic** — useful for any project | Sync to plugin | Comment guidelines (Why/What/None), pitfalls template, code reuse rules |
| **Parameterizable** — generic with project-specific values | Sync as template with placeholders | Architecture review (layer names vary), commit scopes |
| **Project-specific** — only relevant to one project | Do NOT sync | Flutter 2-layer MVVM, Korean comment language, Dart testing patterns |

### Step 3: Update plugin files

1. Modify the relevant skill/rule files in `plugins/project-starter/`
2. Bump version in `plugins/project-starter/.claude-plugin/plugin.json`
3. Update changelog in `README.md`
4. Commit and push

### Step 4: Update marketplace metadata (if needed)

If adding new skills or changing the plugin description, also update:
- `.claude-plugin/marketplace.json` — version and description

## Rules for This Repo

- Keep skills **language-agnostic** — use "ask or infer" instead of hardcoding (e.g., "Dart" or "Python")
- Keep rules **project-independent** — no project names, no specific folder paths
- Version follows semver: patch for fixes, minor for new skills/rules, major for breaking changes
