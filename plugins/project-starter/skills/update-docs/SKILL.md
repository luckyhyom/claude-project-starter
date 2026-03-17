---
name: update-docs
description: Update PROGRESS.md and PLAN.md after completing work. Use after finishing a task or before committing.
allowed-tools: Read, Edit
---

# Update Project Tracking Documents

Synchronize PLAN.md and PROGRESS.md with completed work.

## Steps

1. **Read current state:**
   - Read `PLAN.md` to see task checklist
   - Read `PROGRESS.md` to see current status and last entries

2. **Update PLAN.md:**
   - Mark completed tasks as `[x]`
   - Add any new tasks discovered during work as `[ ]`

3. **Update PROGRESS.md:**
   - Update `Last Updated` date
   - Update `Active Phase` if changed
   - Update `Blocker` if any
   - Add new entry under `## Recent Work` with today's date
   - **Trim old entries:** keep only the most recent 2-3 sessions. Remove older entries — they are preserved in git history.
   - Update `## Notes for Next Agent` section:
     - **Immediate Next Task:** what should be done next and in what order
     - **Environment:** any relevant environment state
     - **Key Context:** important state information for the next agent

4. **Report:**
   - Summarize what was marked complete
   - Show the current active phase and next task
