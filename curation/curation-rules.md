---
type: rule
project: global
status: active
tags: [curation, maintenance]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Curation Rules

Rules for keeping the memory vault tidy and useful.

## Processing _inbox/

1. Read each note in `_inbox/`
2. Add proper YAML frontmatter if missing
3. Determine the correct destination folder
4. Add `[[wikilinks]]` to related existing notes
5. Move to destination folder
6. Update `index.md`

## Deduplication

- Search for existing pages before creating new ones
- If two pages cover the same concept, merge them (keep the better filename)
- Add a note about the merge in the updated page

## Archival

- Notes with `status: archived` should be moved to an `_archive/` subfolder
- Archive session logs older than 90 days
- Never delete. Always archive.

## Link Maintenance

- Fix broken `[[wikilinks]]`
- Every note must have at least 2 incoming or outgoing links
- Orphan pages should be connected or archived

## Tag Hygiene

- Lowercase, hyphenated tags: `#azure-functions` not `#AzureFunctions`
- Consolidate similar tags
- If a tag appears on 20+ notes, create a dedicated index page

## Git Commit Convention

- After curation: `chore(vault): curate — <summary>`

## Related

- [[curation/index]]
- [[AGENTS]]
