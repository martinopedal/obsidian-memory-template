---
name: weekly-review
description: End-of-week review. Summarize the week, surface patterns, prune stale notes.
---

# Weekly Review Workflow

1. Read all session logs from `logs/` for the current week.
2. Read `wiki/decisions/` for any decisions made this week.
3. Synthesize:
   - What got done
   - Decisions made with reasoning
   - Patterns discovered
   - What did not get done and why
   - Recurring themes
   - Next week priorities
4. Save weekly summary to `logs/YYYY-WNN-weekly-review.md`.
5. Run a light curation pass:
   - Check for stale notes (not updated in 60+ days, not referenced)
   - Flag candidates for archival
   - Verify every note has at least 2 backlinks
6. Update `index.md`.
7. Ask: "Any wins or lessons to add before I save?"
