---
name: session-close
description: End-of-session workflow. Summarize the session, update wiki, write log.
---

# Session Close Workflow

1. Review the current session. Identify key decisions, patterns learned, and action items.
2. For each reusable insight:
   - Check if a wiki page already exists. Update it.
   - If not, create a new page in the appropriate `wiki/` subfolder.
   - Use proper YAML frontmatter and `[[wikilinks]]`.
   - Add backlinks from related existing notes.
3. Write a session summary to `logs/YYYY-MM-DD-<topic>.md` using the session-log template.
4. Update `index.md` if new wiki pages were created.
5. Ask: "Anything else to capture before we close?"
