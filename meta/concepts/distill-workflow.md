---
title: "Distill Workflow"
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: []
tags: [workflow, automation]
---

# Distill Workflow

How Claude Code conversations are automatically captured and processed into wiki content.

## Two-Stage Pipeline

```
CC conversations → /wiki-distill → raw/sessions/ → /wiki-ingest → wiki pages
```

Distill never writes wiki pages directly. It extracts conversation content into structured markdown files in `raw/sessions/`, preserving the raw → wiki separation that the framework relies on. The ingest step then processes those raw files into proper wiki pages with cross-references.

## Conversation Access

Claude Code stores full conversation transcripts at `~/.claude/projects/<project-path>/<session-id>.jsonl`. Each line is a JSON object with fields like `type`, `message`, `timestamp`, `cwd`, `sessionId`. A scheduled agent running as the same user can read these directly.

## What Gets Captured

**Included:** decisions and rationale, new facts or corrections, architecture discussions, problem diagnoses, insights and synthesis.

**Skipped:** routine tool calls, mechanical edits, debugging without insights, meta-discussion about the tool.

## Scheduling

Runs as a headless agent via `/schedule` (cron-based). Default: daily. Tracks its last run timestamp in `log.md` to avoid reprocessing.

## Relationship to Other Workflows

- [[ingest-workflow]] — Distill produces raw files that feed into the standard ingest pipeline
- [[lint-workflow]] — Lint catches quality issues in pages created by distill (orphans, missing cross-refs)
