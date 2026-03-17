---
name: translate-docs
description: Update outdated translation files (*_XX.md). Compares commit hashes to skip up-to-date translations. Supports any target language.
argument-hint: "[language-code] (e.g., KO, ZH, JA, ES)"
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Translate Docs

Update translations for all translatable documents.

## Steps

1. **Determine target language:**
   - If `$ARGUMENTS` is provided, use it as the language code (e.g., KO, ZH, JA)
   - If not, check project's CLAUDE.md or docs for the configured translation language
   - If still unknown, ask the user

2. **Find translatable files:**
   - Search for documentation about translation rules (e.g., multilingual docs guide)
   - If no guide exists, default to translating: README.md, docs/planning/*.md, docs/guides/*.md
   - Skip: `.claude/rules/`, `docs/references/`, generated files

3. **Check which translations are outdated:**
   ```bash
   # Get current commit hash of the original
   git log --format="%h" -1 -- <original_file>

   # Read first line of the translation file to get tracked hash
   head -1 <translated_file>
   ```
   - If hashes match → skip (up to date)
   - If hashes differ or translation doesn't exist → needs translation

4. **Translate outdated files:**
   - Read the English original
   - Create/update the `_XX.md` file (e.g., `README_KO.md`) with:
     - `<!-- translated from: <filename> @ commit <hash> (<date>) -->` as first line
     - Full translation of the content
   - **Preserve in English:** code blocks, file paths, command examples, technical terms

5. **Report summary:**
   - Files checked / skipped (up to date) / translated

## Important

- Never modify the English originals
- Preserve markdown formatting exactly
- Code blocks, file paths, CLI commands stay in English
- Technical terms (Repository, ViewModel, etc.) stay in English
