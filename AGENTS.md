# Memory Vault — Agent Instructions

> This is a persistent knowledge base for your development work.
> You are a wiki maintainer. When you learn something new, file it into the wiki.
> When answering questions, search the wiki first.

## Session Start (keep this minimal to save tokens)

1. Read this file (AGENTS.md)
2. Read `index.md` to see what exists
3. If working on a specific project, read `wiki/projects/<project>/index.md`
4. Read `global/current-focus.md` for what is actively being worked on

Do NOT read logs on startup. Only consult logs when you need historical context for a specific question.

## During Session

- When a reusable pattern emerges, create/update a note in `wiki/patterns/`
- When an architectural decision is made, create a note in `wiki/decisions/`
- When project-specific context is learned, create/update in `wiki/projects/<project>/`
- When a mistake is made and corrected, document in `wiki/patterns/` as an anti-pattern
- Always use `[[wikilinks]]` to connect related notes
- Always use descriptive kebab-case filenames (e.g. `use-cosmos-db-for-session-state.md`)
- Never create duplicate notes. Update existing ones with new information.
- Flag contradictions when you find them

### Linking Rules (mandatory)

Every note you create or update must follow these rules:
1. Add a `## Related` section at the bottom with at least 2 `[[wikilinks]]` to other notes
2. After creating a new note, add a backlink from at least 2 related existing notes pointing back
3. Use filename-only links for unique names: `[[coding-standards]]`
4. Use path links when ambiguous: `[[wiki/projects/my-project/index|my-project]]`
5. Cross-link related projects to each other
6. An unlinked note is invisible in the Obsidian graph. Every note must be reachable.

## Session End

1. Summarize key decisions, lessons learned, and action items
2. Save session summary to `logs/YYYY-MM-DD-<topic>.md`
3. Update any wiki pages affected by this session
4. Update `index.md` if new pages were created
5. If raw sources were processed, move insights to `wiki/` and note in index

## Note Format

Every note uses YAML frontmatter:

```yaml
---
type: pattern | decision | concept | log | rule | project | index
project: repo-name-or-global
status: active | draft | archived
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

Body text uses `[[wikilinks]]` for connections and `#tags` for topics.

## Folder Purposes

| Folder | Purpose |
|--------|---------|
| `raw/` | Unprocessed sources. Read, extract, file into `wiki/` |
| `wiki/` | Processed, linked knowledge. The brain. Search here first. |
| `wiki/patterns/` | Reusable code patterns and anti-patterns |
| `wiki/decisions/` | Architectural Decision Records (ADR-style) |
| `wiki/projects/` | Per-project memory banks (one subfolder per repo/org) |
| `global/` | Cross-project coding standards, tools, preferences |
| `global/current-focus.md` | What is actively being worked on right now. Read on session start. |
| `curation/` | Rules for keeping the vault tidy |
| `logs/` | Session summaries |
| `_inbox/` | Quick capture, unprocessed. Process during curation. |
| `_templates/` | Note templates (do not modify) |
| `skills/` | Named automation workflows |

## Redaction Rules (per-session, checked before writing ANY note)

Before writing or updating any note, check the content for:
- Customer names, company names, or project codenames that identify real customers
- Financial instruments: account numbers, invoice amounts, contract values, pricing
- Credentials: API keys, tokens, passwords, connection strings
- PII: email addresses, phone numbers, employee IDs
- Internal codenames or confidential project names

If any of these appear in content you want to capture:
- Replace customer names with generic labels: "Customer A", "a financial services customer"
- Remove financial figures entirely
- Never write credentials into any note, ever
- Strip PII before saving
- Replace codenames with public product names where possible

This filtering happens in your head during the session. There is no automated pre-commit hook. You are the filter.

## What NOT To Do

- Never delete notes. Set `status: archived` instead.
- Never rename a note's filename without updating all `[[wikilinks]]` that reference it
- Never modify `_templates/` files
- Never commit secrets, API keys, tokens, or PII
- Never commit customer names or financial instruments
- Don't create files in `.squad/` or `.obsidian/` directly
- Don't put everything in one mega-note. One concept per file.
- Don't read the entire vault on startup. Follow the minimal load path above.
