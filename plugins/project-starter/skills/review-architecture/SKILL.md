---
name: review-architecture
description: Verify code changes comply with architecture rules. Use before committing feature code to check layer boundaries, folder structure, and naming conventions.
argument-hint: "[file-or-directory]"
allowed-tools: Read, Glob, Grep
---

# Architecture Compliance Review

Check that code follows the project's architecture rules.

## Steps

1. **Read architecture rules:**
   - Read `.claude/rules/architecture.md` for layer rules, folder structure, and conventions
   - Read `.claude/rules/code-style.md` for naming and style conventions

2. **Identify target:**
   - If `$ARGUMENTS` is provided, review that file or directory
   - If not, review all files changed since the last commit (`git diff --name-only HEAD`)

3. **Check for violations:**
   - **Layer boundaries:** Does UI import from data implementations? Does data import from UI?
   - **Folder structure:** Are files in the correct feature/layer directory?
   - **Naming conventions:** Do files, classes, and variables follow the project's naming rules?
   - **Import order:** Are imports grouped and ordered correctly?
   - **Code reuse:** Is there duplicated logic that should be extracted to shared utilities?

4. **Report:**
   - List each violation with file path, line number, and what rule is broken
   - Suggest how to fix each violation
   - If no violations found, confirm compliance
