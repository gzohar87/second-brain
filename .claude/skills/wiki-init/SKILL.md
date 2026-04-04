---
name: wiki-init
description: Initialize a new LLM Wiki vault — analyzes domain, proposes structure, creates files, installs skills
---

# Wiki Init

You are initializing a new LLM Wiki vault. Follow these steps carefully.

## Step 1: Gather Context

Ask the user:
1. **What is this wiki for?** (domain, intent, what kind of knowledge will it track)
2. **Deployment mode?**
   - **Standalone**: the wiki is its own git repo (for personal knowledge, research, book notes)
   - **Embedded**: the wiki lives in a named directory inside an existing code repo (default: `<repo-name>-wiki/`)

If embedded, explore the repo structure to understand the codebase — read the top-level directory listing, any existing README, CLAUDE.md, and key config files.

## Step 2: Propose Wiki Structure

Based on the domain and (if embedded) the repo structure, propose a set of subdirectories for `wiki/`. **Do not use generic defaults** — tailor the hierarchy to the specific domain.

Examples of domain-appropriate structures:
- Research project: `papers/`, `theories/`, `methods/`, `people/`, `datasets/`
- Code project: `architecture/`, `modules/`, `decisions/`, `guides/`, `apis/`
- Personal wiki: `goals/`, `health/`, `learning/`, `journal/`, `projects/`
- Book notes: `characters/`, `themes/`, `plot/`, `worldbuilding/`, `quotes/`

Present the proposal and **wait for user approval** before creating anything.

## Step 3: Create Vault Structure

### Standalone mode
1. Create the vault directory at the user-specified path
2. Run `git init` inside it
3. Create directories:
   - `raw/` and `raw/assets/`
   - `wiki/` with the approved subdirectories
4. Create `index.md` with this content:
   ```markdown
   ---
   title: Index
   type: index
   created: <TODAY>
   updated: <TODAY>
   ---

   # Index

   Master index of all wiki pages. Keep this up to date whenever pages are added, renamed, or removed.

   ## Pages

   <!-- Add entries: - [[page-name]] — Brief description -->
   ```
5. Create `log.md` with this content:
   ```markdown
   ---
   title: Log
   type: log
   created: <TODAY>
   updated: <TODAY>
   ---

   # Log

   Chronological record of wiki activity. **Append-only** — never edit or remove past entries.

   Actions: `created`, `updated`, `refactored`, `deprecated`, `deleted`

   ---

   ## [<TODAY>] created | Wiki initialized

   Vault created for: <domain description>
   Structure: <list approved subdirs>
   ```

### Embedded mode
Same as above, but:
- Create everything under the vault directory (e.g., `<repo-name>-wiki/`) in the repo root
- Do NOT run `git init` (the repo already has git)
- The wiki path is the vault directory name

## Step 4: Set Up CLAUDE.md

### Standalone mode
Create a new `CLAUDE.md` at the vault root with the wiki conventions. Replace `{{WIKI_PATH}}` with the appropriate path (root-level `wiki/`).

### Embedded mode
Append the wiki conventions block to the existing `CLAUDE.md` (or create one if it doesn't exist). Replace `{{WIKI_PATH}}` with the vault directory path. The conventions block:

```markdown
# Wiki Conventions

Wiki location: `<WIKI_PATH>`

## Linking
- Internal links: `[[page-name]]` (Obsidian wikilinks)
- Code references: `src/auth/handler.ts:45` (file path with optional line number)

## Page Format
- YAML frontmatter: `title`, `type`, `created`, `updated`, `sources`, `tags`
- Use `##` headers for sections
- Filenames: `kebab-case.md`

## Golden Rules
1. **Never** modify anything in `raw/` — that directory is source-of-truth input
2. **Always** update `index.md` and `log.md` when creating or modifying wiki pages
3. Note contradictions explicitly — do not silently resolve conflicting information
```

## Step 5: Configure Obsidian

Create `.obsidian/app.json` at the vault root:

```json
{
  "useMarkdownLinks": false,
  "newFileLocation": "folder",
  "newFileFolderPath": "wiki",
  "attachmentFolderPath": "raw/assets"
}
```

## Step 6: Install Wiki Skills

Copy the wiki skill directories (`wiki-ingest`, `wiki-query`, `wiki-lint`) into the target project's `.claude/skills/`. If the skills are already present (e.g., this is a re-init), skip this step.

## Step 7: Summary

Report to the user:
- What was created (directory tree)
- Where the wiki lives
- Next steps: drop source documents into `raw/`, then run `/wiki-ingest` to process them
