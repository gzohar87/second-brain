---
title: "Architecture"
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [meta, architecture]
---

# Architecture

## Three-Layer Model

The framework organizes knowledge into three layers: raw sources (original materials), wiki (distilled pages), and schema (CLAUDE.md + skills). Each layer serves a distinct role in the pipeline from ingestion to retrieval.

## Vault Model

Wikis are always standalone directories with their own git repo. A wiki can be linked to a code repo via `sb link`, which injects wiki conventions into the repo's CLAUDE.md. When linked, wiki pages can cite file paths in the repo (e.g., `src/auth/handler.ts:45`) rather than copying code — keeping the wiki in sync with the codebase.

## Skills-Based Operation

Workflows are encapsulated as skills rather than inlined into a monolithic config. Each skill (ingest, query, lint) is invoked on demand — see [[schema-design]].

## Framework vs Vault

The second-brain is a framework (reusable scaffold with conventions) not a vault (a personal knowledge dump). The meta-wiki documents the framework itself; user content lives in the wiki layer.
