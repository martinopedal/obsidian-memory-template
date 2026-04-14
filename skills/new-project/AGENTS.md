---
name: new-project
description: Add a new project to the memory vault. Creates a project memory bank.
---

# New Project Workflow

1. Ask for the project name (git repo name or org name).
2. Create folder `wiki/projects/<project-name>/`.
3. Copy `_templates/project-index.md` to `wiki/projects/<project-name>/index.md`.
4. Fill in project details: overview, tech stack, architecture.
5. Add `[[wikilinks]]` to `coding-standards` and `tools-and-setup`.
6. Add backlinks from related existing projects.
7. Update the main `index.md` to list the new project.
8. Ask: "Tell me about this project so I can populate the initial notes."
