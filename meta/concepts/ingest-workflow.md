---
title: "Ingest Workflow"
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [meta, concept, workflow, ingest]
---

# Ingest Workflow

## Overview

Ingest transforms a raw source into structured wiki knowledge. It is one of the core skills in the [[architecture]].

## Pipeline

1. **Read source** — Load the original material (article, paper, transcript, code).
2. **Discuss** — Interactive Q&A to clarify key ideas and resolve ambiguities.
3. **Organize** — Produce a structured, readable version of the source. This is not a summary — it preserves the substance while removing noise (filler, repetition, tangents) and reorganizing by topic/theme. Specific examples, arguments, and nuance are kept.
4. **Cross-reference** — Add `[[wikilinks]]` to related existing pages.
5. **Update index/log** — Append the new page to the wiki index and record the action in the log.

## Design Philosophy

The wiki page is the **readable version** of the raw material, not a lossy summary. The raw file (`raw/`) remains the source of truth and is always referenced in frontmatter, but the wiki page should be complete enough that going back to the raw file is rarely needed.
