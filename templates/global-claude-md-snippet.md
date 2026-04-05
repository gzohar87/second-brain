<!-- BEGIN sb -->
## second-brain (LLM Wiki framework)
Location: `{{FRAMEWORK_DIR}}`
Alias: `sb` (in ~/.bashrc)

Framework for building LLM-maintained personal wikis. The LLM ingests raw material (documents, notes, transcripts) into `raw/`, distills it into interlinked wiki pages in `wiki/`, and keeps everything organized via `index.md`, `log.md`, and `tracker.md`.

Wikis are standalone directories that can be linked to any repo. Skills are installed globally.

Commands:
- `sb init <path>` — Create a new wiki vault (dirs + templates)
- `sb link <wiki> [--repo R]` — Point a repo at a wiki (appends conventions to repo's CLAUDE.md)
- `sb unlink [--repo R]` — Remove wiki link from repo's CLAUDE.md
- `sb install` — Install/update global skills and this section
- `sb update` — Refresh everything (global + local if in linked repo)

Skills (`/wiki-init`, `/wiki-ingest`, `/wiki-query`, `/wiki-lint`) are installed globally in `~/.claude/skills/`.
<!-- END sb -->
