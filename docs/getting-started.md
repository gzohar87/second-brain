# Getting Started with LLM Wiki

LLM Wiki turns Claude Code into a knowledge-management agent. You drop source material (docs, notes, code) into a `raw/` folder and use Claude Code skills to ingest, organize, and query a wiki of interlinked Markdown pages — viewable in Obsidian or any Markdown reader.

## Prerequisites

- **Git** — any recent version
- **Claude Code** — [claude.ai/download](https://claude.ai/download)
- **Obsidian** (recommended) — for graph view, wikilinks, and Dataview queries

## Quick Start

### 1. Clone the framework repo

```bash
git clone <repo-url> second-brain
```

### 2. Bootstrap a vault

**Standalone** — creates a new git repo for your wiki:

```bash
second-brain/tools/sb init ~/my-wiki
```

**Embedded** — adds a `.wiki/` folder inside an existing repo:

```bash
cd ~/my-project
~/second-brain/tools/sb init --embedded
```

### 3. Configure the wiki structure

Open the vault in Claude Code and run:

```
/wiki-init
```

Claude will scan your project, propose subdirectories and an initial page outline, and set up the wiki skeleton.

### 4. Ingest sources

Drop files (Markdown, PDFs, code, screenshots) into `raw/`, then run:

```
/wiki-ingest
```

Claude reads the new material, creates or updates wiki pages, and maintains the index and log.

## Available Skills

| Skill | Purpose |
|-------|---------|
| `/wiki-init` | Propose directory structure and scaffold wiki pages |
| `/wiki-ingest` | Process new sources in `raw/` into wiki pages |
| `/wiki-query` | Answer questions using the wiki as context |
| `/wiki-lint` | Check for broken links, missing frontmatter, and stale index entries |

## Tips

- **Obsidian Web Clipper** — save articles and web pages directly into `raw/` for ingestion.
- **Graph view** — open Obsidian's graph view to visualize how wiki pages link together.
- **Dataview queries** — use the Dataview plugin to query frontmatter fields (`type`, `tags`, `sources`) across all pages.
- **Keep `raw/` sacred** — never edit files in `raw/`; it is the source-of-truth archive. All synthesis goes in `wiki/`.
- **Log everything** — `/wiki-ingest` appends to `log.md` automatically, but you can add manual entries too.
