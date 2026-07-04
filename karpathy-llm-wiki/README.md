# Karpathy's LLM-Wiki Pattern — Demo

In April 2026, Andrej Karpathy published a [gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) describing a simple but powerful idea: instead of doing RAG over raw documents on every question, have the LLM **incrementally build and maintain a wiki** — so knowledge compounds instead of evaporating between sessions.

> Ask a subtle question that requires synthesizing five documents, and a RAG system has to find and piece together the relevant fragments *every time*. With a maintained wiki, the synthesis happened once — the wiki is a persistent, compounding artifact. The cross-references are already there.

## The three layers

| Layer | In this demo | Who writes it |
|---|---|---|
| **Raw sources** | [`sources/`](./sources/) | Human curates; LLM reads but **never modifies** |
| **The wiki** | [`wiki/`](./wiki/) | LLM owns this layer entirely |
| **The schema** | [`CLAUDE.md`](./CLAUDE.md) | Human + LLM; tells the LLM how the wiki is structured, what the conventions are, and what workflows to follow |

## The three core operations

- **Ingest** — read a new source, discuss key takeaways, write a summary page, update the index, and revise every entity/concept page it touches. A single source might touch 10–15 wiki pages.
- **Query** — search relevant pages, synthesize an answer with citations. Valuable answers get filed back into the wiki as new pages.
- **Lint** — health-check the wiki: contradictions, stale claims, orphan pages, missing cross-references, data gaps.

## Special files

- [`wiki/index.md`](./wiki/index.md) — a content-oriented catalog organized by category, with links and one-line summaries. Agents read this first to find relevant pages before drilling deeper (progressive disclosure).
- [`wiki/log.md`](./wiki/log.md) — append-only chronological record with parseable entry prefixes, e.g. `## [2026-07-04] ingest | Article Title`.

## Conventions in this demo

- Pages are markdown with Obsidian-style `[[wikilinks]]` between related pages. (GitHub doesn't render `[[...]]` as links — tools like Obsidian do; the convention is what matters.)
- Light YAML frontmatter (`kind`, `tags`, `updated`) for tooling like Obsidian Dataview.
- Every claim traces back to a source: pages end with a **Sources** section.

## Why it works

The tedious part of maintaining a knowledge base is not the reading or the thinking — it's the **bookkeeping**. LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass. Human responsibility: curating sources, directing analysis, asking good questions. LLM responsibility: everything else.

## The demo content

This demo wiki's *subject* is **Anthropic and the Claude models**: the two sources in `sources/` are reading notes on Anthropic's models/pricing docs and prompt-caching docs, and the wiki pages that "grew" from ingesting them cover [[claude-model-lineup]], [[adaptive-thinking]], [[prompt-caching]], and the [[anthropic]] entity page. Browse [`wiki/index.md`](./wiki/index.md) to start — exactly the way an agent would.
