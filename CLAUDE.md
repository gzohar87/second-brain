# second-brain

Framework for building LLM-maintained personal wikis. The LLM ingests raw material, distills it into interlinked wiki pages, and keeps everything organized and up to date.

## Wiki Conventions

Wiki location: `meta/`

The `meta/` directory uses the wiki pattern to document the framework's own development (dogfooding).

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

## Repo Structure

- `raw/` — Source material (read-only input)
- `meta/` — Wiki pages documenting this project's own development
- `templates/` — Starter templates for new vaults
- `tools/` — Scripts and utilities for wiki operations
- `docs/` — User-facing documentation
