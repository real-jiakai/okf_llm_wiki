# Wiki schema — read this before touching the wiki

You (the LLM) maintain the wiki in `wiki/`. The human maintains `sources/`. This file defines the structure, conventions, and workflows. Follow them exactly; update this file only when the human agrees to a convention change.

## Layout

```
sources/                  IMMUTABLE. Raw curated documents. Read, never write.
wiki/
├── index.md              Catalog of every page, grouped by category, one-line summary each.
├── log.md                Append-only operation log. Never edit past entries.
├── summaries/            Exactly one page per ingested source.
├── concepts/             One page per concept (ideas, methods, formats).
└── entities/             One page per entity (people, organizations, products).
```

## Page conventions

- Filenames: lowercase, hyphen-separated, e.g. `open-knowledge-format.md`.
- Every page starts with YAML frontmatter:

  ```yaml
  ---
  kind: concept | entity | summary
  tags: [two, or, three]
  updated: YYYY-MM-DD
  ---
  ```

- Link related pages with `[[wikilinks]]` using the target's filename without `.md`, e.g. `[[llm-wiki]]`.
- Every page ends with a `## Sources` section listing where its claims come from (files in `sources/` and/or external URLs).
- Keep pages short and factual. Prefer updating an existing page over creating a near-duplicate.

## Workflows

### Ingest (`ingest sources/<file>`)
1. Read the source in full.
2. Write `wiki/summaries/<source-slug>.md`: key takeaways, notable quotes, open questions.
3. Create or update every concept/entity page the source touches. Add `[[wikilinks]]` in both directions.
4. Add the new pages to `wiki/index.md` under the right category.
5. Append to `wiki/log.md`: `## [YYYY-MM-DD] ingest | <source title>` plus a bullet list of pages created/updated.

### Query (`query: <question>`)
1. Read `wiki/index.md`, open only the relevant pages.
2. Answer with citations to wiki pages and original sources.
3. If the synthesis is valuable and non-obvious, file it as a new concept page and log it: `## [YYYY-MM-DD] query | <question>`.

### Lint (`lint`)
1. Check for: contradictions between pages, stale claims, orphan pages (no inbound links), missing cross-references, index entries pointing nowhere.
2. Fix what is unambiguous; list the rest for the human.
3. Log it: `## [YYYY-MM-DD] lint | <n> issues found, <m> fixed`.
