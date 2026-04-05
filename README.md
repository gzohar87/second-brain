# Second Brain

A framework for building LLM-maintained personal knowledge bases, based on [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

Instead of RAG, the LLM incrementally builds and maintains a persistent wiki of interlinked markdown files. The wiki grows organically as you feed it information -- subdirectories are proposed dynamically based on domain, not predefined.

## Deployment Modes

- **Standalone** -- the wiki lives in its own git repo (like this one).
- **Embedded** -- the wiki lives in a `<repo-name>-wiki/` directory inside a code repo (customizable via `--name`). In this mode, entries reference live code via file paths rather than copying snippets.

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
# Standalone vault (own git repo)
sb init ~/my-wiki

# Embedded vault inside an existing repo
cd ~/my-project
sb init --embedded                  # creates my-project-wiki/
sb init --embedded --name research  # creates research/
```

Then restart Claude Code and run `/wiki-init` to configure the wiki for your domain.

## Update

```bash
sb update                      # update skills and CLAUDE.md snippet to latest
sb update --name research      # if you used a custom name
```

Wiki content (raw/, wiki/, index.md, log.md) is never touched.

## Uninstall

```bash
sb uninstall                   # removes vault, skills, and CLAUDE.md snippet
sb uninstall --name research   # if you used a custom name
```

## Viewer

The wiki is plain markdown with `[[wikilinks]]`, so [Obsidian](https://obsidian.md) works as a viewer out of the box. Open the vault directory as an Obsidian vault.
