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
2. **Always** update `index.md` and `log.md` when creating or modifying wiki pages. Consult `tracker.md` at session start for orientation.
3. Note contradictions explicitly — do not silently resolve conflicting information

## Work Tracker
- `tracker.md` tracks work items, session history, and lint findings
- Format: `- [ ] \`status\` \`priority\` Description — output: [[page]]`
- Statuses: `todo`, `in-progress`, `blocked`, `done`
- Priorities: `high`, `medium`, `low`
- **Session log**: append a brief note at session start (what you're picking up) and end (what was done, what's next)
- **Always** consult `tracker.md` at the start of a conversation for orientation
<!-- END second-brain wiki conventions -->
