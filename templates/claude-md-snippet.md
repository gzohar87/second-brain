<!-- BEGIN second-brain wiki conventions -->
# Wiki Conventions

Wiki location: `{{WIKI_PATH}}`

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
<!-- END second-brain wiki conventions -->
