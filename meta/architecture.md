---
title: "Architecture"
type: concept
created: 2026-04-05
updated: 2026-04-07
sources: []
tags: [meta, architecture]
---

# Architecture

## Three-Layer Model

The framework organizes knowledge into three layers: raw sources (original materials), wiki (distilled pages), and schema (CLAUDE.md + skills). Each layer serves a distinct role in the pipeline from ingestion to retrieval.

## Vault Model

Wikis are always standalone private directories with their own git repo. Vaults are registered globally via `sb register`, which adds them to `~/.claude/sb-vaults.json` and renders them into `~/.claude/CLAUDE.md`. Every Claude Code session sees all registered vaults without any per-repo configuration. See [[design-decisions]] ADR-6.

## Skills-Based Operation

Workflows are encapsulated as skills rather than inlined into a monolithic config. Each skill (ingest, query, lint) is invoked on demand — see [[schema-design]].

## Framework vs Vault

The second-brain is a framework (reusable scaffold with conventions) not a vault (a personal knowledge dump). The meta-wiki documents the framework itself; user content lives in the wiki layer.
