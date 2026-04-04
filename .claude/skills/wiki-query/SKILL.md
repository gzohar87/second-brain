---
name: wiki-query
description: Answer questions from the wiki with citations, optionally filing results as new pages
---

# Wiki Query

You are answering a question using the wiki as your knowledge base.

## Step 1: Understand the Question

The user's question is provided as an argument or in the conversation context. Identify:
- What specifically is being asked
- What type of answer would be most useful (factual lookup, comparison, analysis, overview)

## Step 2: Search the Wiki

1. Read `index.md` to find relevant pages
2. Use grep/search across `wiki/` for additional relevant pages that might not be indexed
3. Read the identified pages thoroughly
4. If the wiki is in embedded mode, you can also reference the codebase directly for code-related questions

## Step 3: Synthesize an Answer

Adapt the format to the question type:

- **Factual lookup** → concise answer with `[[wikilink]]` citations
- **Comparison** → table format comparing entities/approaches, with sources
- **Analysis** → structured response with sections, evidence, and citations
- **Overview** → narrative connecting multiple pages, with links to deeper reading
- **Timeline** → chronological view of events/changes with dates and sources

Always:
- Cite specific wiki pages using `[[wikilinks]]`
- Reference underlying raw sources where relevant
- Distinguish between what the wiki says vs. what you're inferring
- If the wiki lacks information to answer fully, say so explicitly and suggest what sources could fill the gap

## Step 4: Offer to File the Result

If the answer produces something durable — a comparison, analysis, synthesis, or decision record — offer to save it as a new wiki page.

If the user agrees:
1. Create the page with proper frontmatter:
   ```yaml
   ---
   title: "<Descriptive Title>"
   type: <comparison|analysis|synthesis|decision>
   created: <TODAY>
   updated: <TODAY>
   sources: [<list of wiki pages and raw sources consulted>]
   tags: [<relevant tags>]
   ---
   ```
2. Add `[[wikilinks]]` to and from related pages
3. Update `index.md`
4. Append to `log.md`:
   ```
   ## [<TODAY>] created | Query result: <Title>

   Filed answer to: "<original question>"
   Based on: [[page-1]], [[page-2]], ...
   ```

## When the Wiki Can't Answer

If relevant information doesn't exist in the wiki:
- Say clearly what's missing
- Suggest specific sources that might help (papers, docs, articles)
- Offer to create a stub page marking this as a knowledge gap to fill later
