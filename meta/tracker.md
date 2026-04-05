---
title: "second-brain"
type: tracker
created: 2026-04-05
updated: 2026-04-05
tags: []
---

# Work Tracker

## Work Items

### Framework Development

- [x] `done` `high` Foundation — directory structure, CLAUDE.md, basic wiki layout, initial tooling scripts — output: [[architecture]]
- [x] `done` `high` Skills — ingest, query, and lint skills extracted into standalone skill files — output: [[architecture]]
- [x] `done` `medium` Meta-wiki buildout — internal documentation of the framework itself — output: [[index]]
- [x] `done` `high` Work tracker — tracker.md as first-class vault file — output: [[design-decisions]]
- [ ] `todo` `medium` Bootstrap script + docs — single command to scaffold into new/existing repo, user-facing documentation — output: TBD
- [ ] `todo` `low` Search integration — full-text retrieval across wiki pages (qmd) — output: TBD
- [ ] `todo` `low` Marp slide generation — present wiki content as slides — output: TBD
- [ ] `todo` `low` Dataview-style queries — dynamic indexes from frontmatter — output: TBD

### Improvements

- [ ] `todo` `high` `sb status` command — show installed skills, linked wikis, vault health — output: TBD
- [ ] `todo` `high` CLI tests — integration tests for marker-based CLAUDE.md editing (link/unlink) — output: TBD
- [ ] `todo` `medium` `--dry-run` flag for `link`/`unlink` commands — output: TBD
- [ ] `todo` `medium` Log rotation strategy — `log.md` grows unbounded, needs archival — output: [[design-decisions]]
- [ ] `todo` `medium` Index scalability — flat `index.md` won't scale past 50+ pages — output: [[design-decisions]]
- [ ] `todo` `medium` Tag consumption — frontmatter `tags` field exists but nothing queries them — output: TBD
- [ ] `todo` `low` More user docs — troubleshooting, raw/ content examples, skill reference — output: TBD
- [ ] `todo` `low` Obsidian coupling — commit to hard requirement or provide markdown link fallback — output: [[design-decisions]]
- [ ] `todo` `low` Skill scoping — per-repo visibility instead of global-only — output: [[design-decisions]]

## Lint Findings

<!-- Populated by /wiki-lint -->
