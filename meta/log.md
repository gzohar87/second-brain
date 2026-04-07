---
title: "Meta-Wiki Log"
type: log
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [meta, log]
---

# Meta-Wiki Log

## [2026-04-05] created | Wiki initialized

Initial scaffold of the second-brain framework meta-wiki.
Pages created: architecture, design-decisions, roadmap, ingest-workflow, query-workflow, lint-workflow, schema-design

## [2026-04-05] created | Added work tracker

Added `tracker.md` as first-class vault file alongside `index.md` and `log.md`.
Resolves: gzohar87/second-brain#1

Pages created:
- [[tracker]]

Pages updated:
- [[index]] — added tracker entry

## [2026-04-07] updated | Replace per-repo linking with global vault registry

Removed `sb link`/`sb unlink` (wrote wiki paths into public repo CLAUDE.md). Replaced with `sb register`/`sb unregister` — stores vault paths in private `~/.claude/sb-vaults.json`, renders into `~/.claude/CLAUDE.md`. Wikis are now assumed private.

Pages updated:
- [[architecture]] — vault model now uses global registry
- [[design-decisions]] — added ADR-6

Files updated:
- `tools/sb` — replaced link/unlink with register/unregister, updated status/update
- `templates/global-claude-md-snippet.md` — updated commands and vault listing

Files removed:
- `templates/claude-md-snippet.md` — per-repo snippet no longer needed

## [2026-04-05] created | Wiki automation — distill & lint scheduling

Added scheduled automation for wiki maintenance:
- `/wiki-distill` skill: reviews CC conversation history, extracts content into `raw/sessions/`, ingests into wiki
- `/wiki-automate` skill: one-time setup to register cron schedules via `/schedule`
- `/wiki-lint` autonomous mode: skip check + auto-fix without user interaction
- `config.yml` per-vault automation config (added to vault scaffold)

Pages created:
- [[distill-workflow]] — concept page for the distill pipeline

Pages updated:
- [[index]] — added distill-workflow entry

Skills created:
- `.claude/skills/wiki-distill/SKILL.md`
- `.claude/skills/wiki-automate/SKILL.md`

Skills updated:
- `.claude/skills/wiki-lint/SKILL.md` — added autonomous mode section

Files updated:
- `tools/sb` — config.yml in init/update, `config` command, pyyaml dep, resolve_vault/load_config helpers
- `templates/config.yml` — new automation config template
- `templates/global-claude-md-snippet.md` — added new skills and automation section

## [2026-04-05] updated | Removed embedded mode, updated ADRs

Embedded mode concept removed from all documentation and skills. Wikis are now always standalone directories linked to repos via `sb link`. ADR-1 updated from "Bash over Python" to "Python with uv". ADR-5 (embedded mode) removed; ADR-6 renumbered to ADR-5.

Pages updated:
- [[architecture]] — replaced deployment modes with vault model
- [[design-decisions]] — rewrote ADR-1, removed ADR-5, renumbered ADR-6

Files updated:
- README.md, docs/getting-started.md
- .claude/skills/wiki-init/SKILL.md, wiki-lint/SKILL.md, wiki-ingest/SKILL.md, wiki-query/SKILL.md
