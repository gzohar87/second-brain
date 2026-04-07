<!-- BEGIN sb -->
## second-brain (LLM Wiki framework)
Location: `{{FRAMEWORK_DIR}}`
Alias: `sb` (in ~/.bashrc)

Framework for building LLM-maintained personal wikis. The LLM ingests raw material (documents, notes, transcripts) into `raw/`, distills it into interlinked wiki pages in `wiki/`, and keeps everything organized via `index.md`, `log.md`, and `tracker.md`.

Wikis are standalone private directories. Registered vaults are listed below and visible in every Claude Code session.

Commands:
- `sb init <path>` — Create a new wiki vault (dirs + templates)
- `sb register <vault>` — Register a vault (adds to `~/.claude/CLAUDE.md`)
- `sb unregister <name>` — Remove a vault from the registry
- `sb install` — Install/update global skills and this section
- `sb update` — Refresh everything (global + all registered vaults)
- `sb config [vault]` — Show vault automation config

Skills (`/wiki-init`, `/wiki-ingest`, `/wiki-query`, `/wiki-lint`, `/wiki-distill`, `/wiki-automate`) are installed globally in `~/.claude/skills/`.

### Automation

Vaults can opt into scheduled automation via `config.yml`:
- **Distill** (`/wiki-distill`): Reviews recent Claude Code conversations, extracts wiki-worthy content into `raw/sessions/`, then ingests into wiki pages. Runs on a cron schedule (default: daily).
- **Lint** (`/wiki-lint`): Runs mechanical checks and auto-fixes on a cron schedule (default: every 30 min). Skips if no changes since last lint. Semantic findings go to `tracker.md` for human review.

Setup: run `/wiki-automate` in Claude Code to register schedules from `config.yml`.

### Wiki Conventions

#### Linking
- Internal links: `[[page-name]]` (Obsidian wikilinks)
- Code references: `src/auth/handler.ts:45` (file path with optional line number)

#### Page Format
- YAML frontmatter: `title`, `type`, `created`, `updated`, `sources`, `tags`
- Use `##` headers for sections
- Filenames: `kebab-case.md`

#### Golden Rules
1. **Never** modify anything in `raw/` — that directory is source-of-truth input
2. **Always** update `index.md` and `log.md` when creating or modifying wiki pages. Consult `tracker.md` at session start for orientation.
3. Note contradictions explicitly — do not silently resolve conflicting information
4. **Use wiki skills as the primary interface.** Use `/wiki-query` to read, search, or answer questions about wiki content — do not read wiki files directly with Read/Grep. Use `/wiki-ingest` to add new content. Direct file access is only for mechanical operations (editing frontmatter, fixing links).

#### Work Tracker
- `tracker.md` tracks work items and lint findings
- Format: `- [ ] \`status\` \`priority\` Description — output: [[page]]`
- Statuses: `todo`, `in-progress`, `blocked`, `done`
- Priorities: `high`, `medium`, `low`
- **Always** consult `tracker.md` at the start of a conversation for orientation
<!-- END sb -->
