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

## Deployment Modes

Two modes are supported: standalone (the framework is the repo) and embedded (the framework lives inside another project). Embedded mode is the primary focus — see [[design-decisions]].

## Live Code References

In embedded mode, wiki pages cite file paths rather than copying code. This keeps the wiki in sync with the codebase and avoids stale snippets.

## Skills-Based Operation

Workflows are encapsulated as skills rather than inlined into a monolithic config. Each skill (ingest, query, lint) is invoked on demand — see [[schema-design]].

## Framework vs Vault

The second-brain is a framework (reusable scaffold with conventions) not a vault (a personal knowledge dump). The meta-wiki documents the framework itself; user content lives in the wiki layer.
