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

## [2026-04-05] updated | Removed embedded mode, updated ADRs

Embedded mode concept removed from all documentation and skills. Wikis are now always standalone directories linked to repos via `sb link`. ADR-1 updated from "Bash over Python" to "Python with uv". ADR-5 (embedded mode) removed; ADR-6 renumbered to ADR-5.

Pages updated:
- [[architecture]] — replaced deployment modes with vault model
- [[design-decisions]] — rewrote ADR-1, removed ADR-5, renumbered ADR-6

Files updated:
- README.md, docs/getting-started.md
- .claude/skills/wiki-init/SKILL.md, wiki-lint/SKILL.md, wiki-ingest/SKILL.md, wiki-query/SKILL.md
