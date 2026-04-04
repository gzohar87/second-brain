---
title: "Design Decisions"
type: decision-log
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [meta, decisions, adr]
---

# Design Decisions

## ADR-1: Bash over Python for tooling

All tooling scripts use bash. This keeps the framework zero-dependency — any machine with a shell can run it. No virtual environments, no package managers.

## ADR-2: Dynamic wiki subdirs over predefined categories

Wiki subdirectories are created organically as topics emerge rather than from a fixed taxonomy. This avoids empty placeholder dirs and lets structure follow content.

## ADR-3: Skills over monolithic CLAUDE.md

Workflows live in separate skill files loaded on demand, keeping CLAUDE.md small and focused on always-on conventions. See [[schema-design]].

## ADR-4: Fully agentic lint over bash scripts

Lint is performed by the agent reading and reasoning about pages, not by regex-based shell scripts. This enables semantic checks (e.g., stale cross-references) that scripts cannot do. See [[lint-workflow]].

## ADR-5: Embedded mode as primary focus

The framework is designed first for embedding inside existing projects. Standalone mode is supported but secondary. See [[architecture]].

## ADR-6: Wikilinks over standard markdown links

Internal references use `[[wikilinks]]` for brevity and tooling compatibility (Obsidian, Foam, etc.). Standard markdown links are reserved for external URLs.
