---
name: research
description: Search existing references first, then web search if needed. Use when investigating a technology, pattern, or best practice.
argument-hint: "<topic>"
allowed-tools: Read, Glob, Grep, WebSearch, WebFetch, Write, Edit
---

# Research with Reference Check

Look up existing project references before performing new web searches.

## Steps

1. **Check existing references:**
   - Use `Grep` to search `docs/references/` for `$ARGUMENTS` and related keywords
   - If found, read the relevant reference file and present the information

2. **If not found or insufficient:**
   - Use `WebSearch` to find up-to-date information on the topic
   - Use Context7 plugin for library API and documentation lookups
   - Summarize findings for the user

3. **Verify before presenting:**
   - Never present unverified information as fact — this applies to all web research results, not just numbers or versions
   - When citing external info, include the source URL
   - If a claim cannot be verified via primary sources, mark it with the reason:
     - `(unverified — site blocked access)` — primary source exists but could not be fetched; likely accurate, recommend manual check
     - `(unverified — no primary source found)` — no authoritative source located; treat as uncertain
   - Trusted primary sources: official docs, GitHub repos, pub.dev, arxiv, HuggingFace model cards

4. **Save results:**
   - If the research produced useful new information, ask the user whether to save it
   - If yes, save to `docs/references/{topic-name}.md` with a consistent format:
     ```markdown
     # {Topic Title}

     > Researched: {date}

     ## Summary
     (Key findings)

     ## Details
     (Detailed information, comparisons, pros/cons)

     ## Sources
     (URLs or references)
     ```
   - Update `docs/INDEX.md` if a new reference file was created
