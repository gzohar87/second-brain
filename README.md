# Second Brain

A framework for building LLM-maintained personal knowledge bases, based on [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

Instead of RAG, the LLM incrementally builds and maintains a persistent wiki of interlinked markdown files. The wiki grows organically as you feed it information -- subdirectories are proposed dynamically based on domain, not predefined.

Wikis are standalone directories that can be linked to any code repo via `sb link`. When linked, wiki pages can cite file paths in the repo for code-adjacent documentation.

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
sb init ~/my-wiki              # create a new wiki vault
sb link ~/my-wiki --repo .     # link the current repo to it
```

Then restart Claude Code and run `/wiki-init` to configure the wiki for your domain.

## Update

```bash
sb update                      # update skills and CLAUDE.md snippet to latest
```

Wiki content (raw/, wiki/, index.md, log.md) is never touched.

## Viewer

The wiki is plain markdown with `[[wikilinks]]`, so [Obsidian](https://obsidian.md) works as a viewer out of the box. Open the vault directory as an Obsidian vault.
