# Work Routing

How to decide who handles what.

## Routing Table

| Work Type | Route To | Examples |
|-----------|----------|----------|
| Inbox processing | Curator | Process _inbox/ notes, add frontmatter, move to wiki/ |
| Deduplication | Curator | Find overlapping notes, merge them, fix links |
| Link maintenance | Curator | Fix broken wikilinks, normalize tags, archive stale notes |
| Source processing | Archivist | Read raw/ articles, extract concepts, create wiki pages |
| Research | Archivist | Research a topic, synthesize findings, save to wiki |
| Knowledge extraction | Archivist | Turn session logs or dumps into permanent wiki notes |
| Index maintenance | Librarian | Update index.md, check vault health, find orphan pages |
| Weekly review | Librarian | Summarize the week, surface patterns, prune stale notes |
| New project setup | Librarian | Scaffold a project memory bank in wiki/projects/ |
| Session logging | Scribe | Automatic. Never needs routing. |
| Watch & triage | Ralph | Poll for work, auto-dispatch agents |

## Issue Routing

| Label | Action | Who |
|-------|--------|-----|
| `squad` | Triage: analyze issue, assign `squad:{member}` label | Lead |
| `squad:{name}` | Pick up issue and complete the work | Named member |

### How Issue Assignment Works

1. When a GitHub issue gets the `squad` label, the **Lead** triages it — analyzing content, assigning the right `squad:{member}` label, and commenting with triage notes.
2. When a `squad:{member}` label is applied, that member picks up the issue in their next session.
3. Members can reassign by removing their label and adding another member's label.
4. The `squad` label is the "inbox" — untriaged issues waiting for Lead review.

## Rules

1. **Eager by default** — spawn all agents who could usefully start work, including anticipatory downstream work.
2. **Scribe always runs** after substantial work, always as `mode: "background"`. Never blocks.
3. **Quick facts → coordinator answers directly.** Don't spawn an agent for "what port does the server run on?"
4. **When two agents could handle it**, pick the one whose domain is the primary concern.
5. **"Team, ..." → fan-out.** Spawn all relevant agents in parallel as `mode: "background"`.
6. **Anticipate downstream work.** If a feature is being built, spawn the tester to write test cases from requirements simultaneously.
7. **Issue-labeled work** — when a `squad:{member}` label is applied to an issue, route to that member. The Lead handles all `squad` (base label) triage.
