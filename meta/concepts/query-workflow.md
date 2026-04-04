---
title: "Query Workflow"
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [meta, concept, workflow, query]
---

# Query Workflow

## Overview

Query retrieves and synthesizes knowledge from the wiki. It is one of the core skills in the [[architecture]].

## Pipeline

1. **Search index** — Scan the wiki index and frontmatter to locate relevant pages.
2. **Read pages** — Load and parse the matched wiki pages.
3. **Synthesize** — Combine information across pages into a coherent answer.
4. **Optionally file back** — If the synthesis produces new insight, create or update a wiki page via the ingest flow.
