# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A documentation-only demo comparing two formats for agent-friendly knowledge bases, both covering the same knowledge domain (Anthropic's Claude platform: model lineup, Messages API, prompt caching) so the formats can be compared side by side:

- `karpathy-llm-wiki/` — the **llm-wiki pattern** (Karpathy, April 2026): an LLM incrementally maintains a personal wiki of markdown pages.
- `google-okf/` — **Google's Open Knowledge Format (OKF) v0.1** (June 2026): a portable bundle format that formalizes the same pattern.

There is no build, lint, or test tooling — every file is hand-maintained markdown. "Correctness" means conformance to each demo's own conventions, described below.

## Working in `karpathy-llm-wiki/`

`karpathy-llm-wiki/CLAUDE.md` is part of the demo itself (the pattern's "schema" layer) **and** the authoritative rules for editing that subtree. Follow it exactly. Key constraints:

- `sources/` is immutable — read, never write.
- Every wiki page has `kind`/`tags`/`updated` YAML frontmatter, links via Obsidian-style `[[wikilinks]]`, and ends with a `## Sources` section.
- `wiki/index.md` catalogs every page; `wiki/log.md` is append-only (never edit past entries).
- The defined workflows are `ingest sources/<file>`, `query: <question>`, and `lint`.

## Working in `google-okf/`

`google-okf/bundle/` must stay conformant to OKF v0.1 (the spec is summarized in `google-okf/README.md`):

- Each non-reserved `.md` file is one concept. Frontmatter `type` is required; `title`, `description`, `resource`, `tags`, `timestamp` are recommended.
- `index.md` and `log.md` are reserved. Index files are per-directory catalogs of `* [Title](url) - description` entries with no frontmatter — except the bundle root `index.md`, which declares `okf_version: "0.1"`. `log.md` records changes newest-first under `## YYYY-MM-DD` headings.
- This demo deliberately uses *relative* links inside the bundle (so navigation works on GitHub) rather than the spec-recommended bundle-absolute form (`/models/claude-sonnet-5.md`) — keep that choice consistent.
- Conventional body headings consumers may look for: `# Schema`, `# Examples`, `# Citations`.

## Cross-cutting conventions

- The two demos intentionally hold identical knowledge. A factual update to one should usually be mirrored in the other, and reflected in the respective index and log files.
- Filenames are lowercase, hyphen-separated.
- Each folder's `README.md` explains its format; the root `README.md` compares them. Structural changes need matching README updates.
