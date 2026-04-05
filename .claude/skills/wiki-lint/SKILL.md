---
name: wiki-lint
description: Fully agentic wiki health check — find contradictions, orphans, stale content, and suggest improvements
---

# Wiki Lint

You are performing a comprehensive health check on the wiki. This is a fully agentic process — read, reason, and report.

## Step 1: Scan the Wiki

1. Read `index.md` to get the page catalog
2. List all `.md` files in `wiki/` recursively
3. Read each wiki page (if the wiki is very large — over ~50 pages — read a representative sample and flag that a full audit wasn't done)
4. Also read `log.md` for recent activity context

## Step 2: Mechanical Checks

### Orphan pages
Wiki pages with **no inbound `[[wikilinks]]`** from any other page. Check every page in `wiki/` — is it linked to from at least one other page or from `index.md`?

### Broken links
`[[wikilinks]]` that point to pages that **don't exist** as files. Scan all pages for `[[...]]` patterns and verify each target exists.

### Index drift
- Pages in `wiki/` that are **not listed** in `index.md`
- Entries in `index.md` that point to pages that **no longer exist**

### Missing frontmatter
Pages without proper YAML frontmatter, or missing required fields (`title`, `type`, `created`, `updated`).

### Empty / stub pages
Pages with very little content — under ~5 lines of actual content (excluding frontmatter).

### Stale file-path references
For embedded (code-adjacent) wikis: code paths cited in wiki pages (e.g., `src/foo.ts:12`) where the **file no longer exists** in the repo. Scan for patterns like backtick-wrapped file paths and verify they exist.

## Step 3: Semantic Checks

These require reading and reasoning about content — the high-value part of this lint.

### Contradictions
Claims in one page that **conflict** with claims in another page, where the contradiction is not acknowledged. Look for:
- Different dates, numbers, or facts about the same entity
- Conflicting assessments or conclusions
- Superseded information that wasn't marked as such

### Stale content
Pages that reference topics covered by **newer sources** but haven't been updated. Cross-reference `log.md` timestamps with page `updated` dates.

### Missing pages
Concepts or entities **frequently mentioned** across multiple pages (via `[[wikilinks]]` or plain text) but lacking their own dedicated page.

### Missing cross-references
Pages covering **related topics** that should link to each other but don't. Look for topical overlap, shared tags, or shared source references.

### Synthesis gaps
Areas where **multiple sources** touch on a topic but no comparison or synthesis page exists to tie them together.

## Step 4: Produce Report

Structure the report by severity:

### Errors (should fix)
- Broken links
- Index drift (missing entries or stale entries)
- Missing frontmatter

### Warnings (should review)
- Contradictions
- Stale content
- Stale file-path references
- Orphan pages

### Suggestions (could improve)
- Missing pages to create
- Missing cross-references to add
- Synthesis gaps to fill
- New sources to seek
- New questions to investigate

For each finding: describe the issue, list the files involved, and suggest a specific fix.

## Step 5: Update Tasks Page

After producing the report, update the wiki's `wiki/tasks.md` (or create it if it doesn't exist):

1. **Read the current tasks page** to see what's already tracked
2. **Remove stale items** — if a previously logged lint finding has been resolved (the issue no longer appears in this lint run), mark it `[x]` or remove it
3. **Add new findings** under a `## Wiki Lint` section, organized by severity:
   - Errors as `- [ ] **[ERROR]** <description> — <files involved>`
   - Warnings as `- [ ] **[WARN]** <description> — <files involved>`
   - Suggestions as `- [ ] **[SUGGEST]** <description> — <files involved>`
4. **Don't duplicate** — if a finding is already tracked (same issue, same files), leave the existing item. Only add genuinely new findings
5. **Update the date** in the tasks page frontmatter (`updated` field) to today

## Step 6: Offer to Fix

After presenting the report:
- **Mechanical fixes** (broken index entries, missing frontmatter, orphan links): offer to fix these automatically
- **Semantic fixes** (contradictions, stale content, new pages): discuss with the user first — these require judgment

If fixes are applied, update `log.md`:
```
## [<TODAY>] updated | Lint pass

Findings: <N> errors, <N> warnings, <N> suggestions
Fixed: <list what was auto-fixed>
Deferred: <list what needs user input>
```
