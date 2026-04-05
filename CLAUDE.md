# second-brain

Framework for building LLM-maintained personal wikis. The LLM ingests raw material, distills it into interlinked wiki pages, and keeps everything organized and up to date.

## Wiki as Project Knowledge Base

Wiki location: `meta/`

The `meta/` directory is the project's knowledge base — it documents architecture, design decisions, workflows, and concepts that aren't obvious from reading the code alone. Before exploring the repo to understand how something works, check `meta/index.md` for a map of available pages. The wiki is maintained alongside the code and should be your first stop for understanding the project's design and conventions.

The `meta/` directory also dogfoods the wiki pattern that this framework provides to other projects.

### Linking
- Internal links: `[[page-name]]` (Obsidian wikilinks)
- Code references: `tools/ingest.py:12` (file path with optional line number)

### Page Format
- YAML frontmatter: `title`, `type`, `created`, `updated`, `sources`, `tags`
- Use `##` headers for sections
- Filenames: `kebab-case.md`

### Golden Rules
1. **Never** modify anything in `raw/` — that directory is source-of-truth input
2. **Always** update `meta/index.md` and `meta/log.md` when creating or modifying wiki pages
3. Note contradictions explicitly — do not silently resolve conflicting information

## Skills

The canonical skill definitions live in `.claude/skills/` in this repo. The global copies in `~/.claude/skills/` are installed from here via `sb install`. **Always edit the repo copy first** — the global copy will be overwritten on next install.

## Repo Structure

- `raw/` — Source material (read-only input)
- `meta/` — Wiki pages documenting this project's own development
- `templates/` — Starter templates for new vaults
- `tools/` — Scripts and utilities for wiki operations
- `docs/` — User-facing documentation
