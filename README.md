# Obsidian Memory System for GitHub Copilot

Persistent memory for GitHub Copilot using an Obsidian vault, Git, and Squad.

Based on Andrej Karpathy's knowledge base pattern: a structured markdown wiki that your AI reads from and writes to across sessions. Each session adds knowledge. Next session starts smarter.

## What this gives you

- Persistent memory across Copilot sessions and projects
- Portable: works with any AI tool, plain markdown files
- Offline access via Obsidian on any device
- Version controlled with full git history
- Curated by a Squad agent team that keeps the vault tidy

## Prerequisites

- Git
- GitHub CLI (`gh`) authenticated
- Node.js 18+
- Obsidian (https://obsidian.md, free)
- GitHub Copilot Pro/Pro+ or Enterprise subscription

### Windows

```powershell
winget install Git.Git
winget install GitHub.cli
winget install OpenJS.NodeJS
winget install Obsidian.Obsidian
npm install -g @bradygaster/squad-cli
```

### macOS

```bash
brew install git gh node
brew install --cask obsidian
npm install -g @bradygaster/squad-cli
```

## Setup

### 1. Create your vault

```powershell
mkdir ~/memory-vault && cd ~/memory-vault
git init && git checkout -b main
```

### 2. Clone this template

Copy the contents of this repo into your vault, or use it as a GitHub template:

```powershell
gh repo create my-memory-vault --private --template martinopedal/obsidian-memory-template
cd my-memory-vault
```

### 3. Initialize Squad

```powershell
squad init
```

Squad creates its agent team in `.squad/`. Three custom agents are pre-configured in this template:

| Agent | Role | What it does |
|-------|------|-------------|
| Curator | Vault hygiene | Processes inbox, merges duplicates, fixes broken links, normalizes tags |
| Archivist | Knowledge extraction | Reads raw sources, extracts concepts, creates wiki pages |
| Librarian | Index and review | Maintains index, weekly reviews, vault health checks |
| Scribe | Session memory | Built-in. Logs decisions and session history. |
| Ralph | Watch and triage | Built-in. Autonomous polling and dispatch. |

After `squad init`, copy the agent charters from this template:

```powershell
Copy-Item -Recurse .squad-agents/* .squad/agents/ -Force
```

### 4. Open in Obsidian

Open Obsidian, select "Open folder as vault", point it at your vault directory.

Install two community plugins:
- **Obsidian Git** (auto-commit and push)
- **Dataview** (query notes like a database)

Settings > Community plugins > Turn on community plugins > Browse > Install each one.

### 5. Set GitHub personal instructions

Go to https://github.com/copilot > click your profile picture (bottom left) > Personal instructions. Paste:

```
## Memory Vault (local only)
If you have access to the local filesystem, read my memory vault at <YOUR_VAULT_PATH> before answering project or coding questions.

Start with: AGENTS.md, then index.md, then global/current-focus.md.
For project-specific work, also read wiki/projects/<project-name>/index.md.

This only applies to software engineering, architecture, and project tasks.
Do not load the vault for general conversation, math, or non-technical questions.
```

Replace `<YOUR_VAULT_PATH>` with your actual vault path.

### 6. Enable Copilot Memory

GitHub.com > Settings > Copilot > Memory > Enable. This runs in parallel as a complementary cloud layer (per-repo, 28-day TTL, auto-generated).

### 7. Start using it

```powershell
cd ~/memory-vault
copilot --agent squad
```

Or from any project repo, Copilot reads the vault via your personal instructions.

## Vault structure

```
memory-vault/
├── AGENTS.md                    # Master instructions (Copilot reads this first)
├── index.md                     # What exists in the vault
├── README.md
├── .github/
│   └── copilot-instructions.md  # Vault-level Copilot instructions
│
├── raw/                         # Unprocessed sources (articles, dumps, transcripts)
├── wiki/
│   ├── patterns/                # Reusable code patterns and anti-patterns
│   ├── decisions/               # Architectural Decision Records
│   └── projects/                # Per-project memory banks
│       └── _template/           # Copy this for new projects
├── global/
│   ├── index.md
│   ├── coding-standards.md      # Your coding conventions
│   ├── tools-and-setup.md       # Your environment and tools
│   └── current-focus.md         # What you are working on right now
├── curation/
│   ├── index.md
│   └── curation-rules.md        # Rules for keeping the vault tidy
├── logs/                        # Session summaries
├── _inbox/                      # Quick capture, process later
├── _templates/                  # Note templates
│   ├── decision.md
│   ├── pattern.md
│   ├── session-log.md
│   └── project-index.md
├── skills/                      # Named workflows
│   ├── session-close/AGENTS.md
│   ├── curate/AGENTS.md
│   ├── new-project/AGENTS.md
│   └── weekly-review/AGENTS.md
├── .squad/                      # Squad agent team (created by squad init)
└── .squad-agents/               # Pre-configured agent charters (copy to .squad/agents/)
    ├── curator/
    ├── archivist/
    └── librarian/
```

## How it works

### The Karpathy pattern

Three-layer knowledge flow:
1. **raw/** - dump unprocessed sources here (articles, notes, transcripts)
2. **wiki/** - processed, linked knowledge. The brain. Copilot searches here first.
3. **logs/** - session summaries. Historical evidence, not default reading.

### Session lifecycle

**Start**: Copilot reads AGENTS.md, index.md, current-focus.md, then the relevant project index.

**During**: Copilot writes reusable knowledge proactively. Patterns go to wiki/patterns/, decisions to wiki/decisions/, project context to wiki/projects/<name>/.

**End**: Run the session-close skill to summarize what happened, update wiki pages, write a log entry.

### Linking rules

Every note must have a `## Related` section with at least 2 `[[wikilinks]]`. When creating a new note, add backlinks from related existing notes. An unlinked note is invisible in the Obsidian graph.

### Redaction rules

Before writing any note, strip:
- Customer names (replace with "Customer A")
- Financial instruments (remove entirely)
- Credentials, API keys, tokens (never write)
- PII: emails, phone numbers, employee IDs
- Internal codenames (use public product names)

The agent is the filter. There is no automated pre-commit hook.

## Skills

| Skill | Trigger | What it does |
|-------|---------|-------------|
| session-close | End of session | Summarize, update wiki, write log |
| curate | On demand | Process inbox, fix links, deduplicate |
| new-project | On demand | Scaffold a project memory bank |
| weekly-review | End of week | Review week, surface patterns, plan ahead |

## Adding a project

Run the new-project skill, or manually:

```powershell
mkdir wiki/projects/my-repo
cp _templates/project-index.md wiki/projects/my-repo/index.md
```

Edit the index with your project details. Add a reference in your project repo's `.github/copilot-instructions.md`:

```markdown
## Memory Vault
Read context from: <YOUR_VAULT_PATH>
Initialize from: AGENTS.md, then index.md, then global/index.md, then wiki/projects/<this-repo>/index.md
```

## Why not Claude Code hooks?

This system was designed for GitHub Copilot, which does not have lifecycle hooks like Claude Code's Stop/PreToolUse. Instead:
- AGENTS.md instructs Copilot to write knowledge proactively during sessions
- The session-close skill replaces the Stop hook as a manual trigger
- Squad agents handle curation that hooks would automate

If you use Claude Code, you can add hooks on top of this structure. The vault format is tool-agnostic.

## Credits

- Andrej Karpathy's knowledge base pattern (https://x.com/karpathy/status/2039805659525644595)
- Squad by Brady Gaster (https://github.com/bradygaster/squad)
- Obsidian (https://obsidian.md)
