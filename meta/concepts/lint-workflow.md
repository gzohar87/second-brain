---
title: "Lint Workflow"
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [meta, concept, workflow, lint]
---

# Lint Workflow

## Overview

Lint scans the wiki for structural and semantic issues. It is one of the core skills in the [[architecture]] and is fully agentic — see [[design-decisions#ADR-4]].

## Pipeline

1. **Scan** — Enumerate all wiki pages and their frontmatter.
2. **Mechanical checks** — Validate frontmatter fields, broken wikilinks, missing index entries.
3. **Semantic checks** — Detect stale content, redundant pages, orphaned references.
4. **Report** — Present findings grouped by severity.
5. **Offer fixes** — Propose and optionally apply corrections interactively.
