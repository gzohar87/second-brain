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
3. **Summarize** — Produce a wiki page with frontmatter, headers, and concise prose.
4. **Cross-reference** — Add `[[wikilinks]]` to related existing pages.
5. **Update index/log** — Append the new page to the wiki index and record the action in the log.
