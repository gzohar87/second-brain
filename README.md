# Second Brain

A framework for building LLM-maintained personal knowledge bases, based on [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

Instead of RAG, the LLM incrementally builds and maintains a persistent wiki of interlinked markdown files. The wiki grows organically as you feed it information -- subdirectories are proposed dynamically based on domain, not predefined.

## Deployment Modes

- **Standalone** -- the wiki lives in its own git repo (like this one).
- **Embedded** -- the wiki lives in a `.wiki/` directory inside a code repo. In this mode, entries reference live code via file paths rather than copying snippets.

## Operations

All operations are available as Claude Code skills:

| Skill | Purpose |
|-------|---------|
| `/wiki-init` | Configure a new wiki (set domain, create initial structure) |
| `/wiki-ingest` | Feed new information into the wiki |
| `/wiki-query` | Ask questions against the wiki |
| `/wiki-lint` | Check for broken links, stale entries, structural issues |

## Quick Start

```bash
tools/sb init <path>   # bootstrap directory structure
```

Then run `/wiki-init` in Claude Code to configure the wiki for your domain.

## Viewer

The wiki is plain markdown with `[[wikilinks]]`, so [Obsidian](https://obsidian.md) works as a viewer out of the box. Open the repo root (or `.wiki/` in embedded mode) as an Obsidian vault.
