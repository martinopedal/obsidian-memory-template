---
name: curate
description: Tidy the vault. Process inbox, fix links, merge duplicates, update index.
---

# Curation Workflow

1. Read `curation/curation-rules.md` for the full ruleset.
2. Process all notes in `_inbox/`:
   - Add YAML frontmatter if missing
   - Determine correct destination folder
   - Add `[[wikilinks]]` to related notes
   - Move to destination
3. Scan `wiki/` for:
   - Duplicate or overlapping notes. Merge.
   - Broken `[[wikilinks]]`. Fix or create stubs.
   - Orphan pages (no incoming links). Connect or archive.
   - Notes with fewer than 2 links. Add connections.
   - Inconsistent tags. Normalize per curation rules.
4. Archive session logs in `logs/` older than 90 days to `logs/_archive/`.
5. Regenerate `index.md` to reflect current vault state.
6. Report summary of changes made.
7. Commit: `chore(vault): curate — <summary>`
