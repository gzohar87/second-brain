---
title: "Schema Design"
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [meta, concept, schema]
---

# Schema Design

## Overview

The schema layer defines how the agent understands and operates on the wiki. It splits configuration into two tiers — see [[architecture]] and [[design-decisions#ADR-3]].

## Minimal CLAUDE.md

CLAUDE.md contains only always-on conventions: directory layout, frontmatter format, linking style, and naming rules. It is loaded on every invocation and must stay small.

## Skills for On-Demand Workflows

Each workflow (ingest, query, lint) is a separate skill file loaded only when invoked. This keeps the base context lean and lets workflows evolve independently.
