---
title: "Design Decisions"
type: decision-log
created: 2026-04-05
updated: 2026-04-07
sources: []
tags: [meta, decisions, adr]
---

# Design Decisions

## ADR-1: Python with uv for tooling

The CLI (`tools/sb`) is a Python script using click for argument parsing and loguru for logging. It runs via `uv run --script`, which resolves dependencies on the fly — no virtual environment or install step required. Originally bash, rewritten in Python for richer argument handling and cleaner code.

## ADR-2: Dynamic wiki subdirs over predefined categories

Wiki subdirectories are created organically as topics emerge rather than from a fixed taxonomy. This avoids empty placeholder dirs and lets structure follow content.

## ADR-3: Skills over monolithic CLAUDE.md

Workflows live in separate skill files loaded on demand, keeping CLAUDE.md small and focused on always-on conventions. See [[schema-design]].

## ADR-4: Fully agentic lint over bash scripts

Lint is performed by the agent reading and reasoning about pages, not by regex-based shell scripts. This enables semantic checks (e.g., stale cross-references) that scripts cannot do. See [[lint-workflow]].

## ADR-5: Wikilinks over standard markdown links

Internal references use `[[wikilinks]]` for brevity and tooling compatibility (Obsidian, Foam, etc.). Standard markdown links are reserved for external URLs.

## ADR-6: Global vault registry over per-repo linking

Previously, `sb link` injected a wiki path into a repo's CLAUDE.md. This exposed private wiki paths in potentially public repos. Replaced with `sb register/unregister`, which stores vault paths in `~/.claude/sb-vaults.json` (private) and renders them into `~/.claude/CLAUDE.md`. Every CC session sees registered vaults without any repo-level configuration.
