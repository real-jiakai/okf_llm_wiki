# OKF & LLM-Wiki — Two Formats for Agent-Friendly Knowledge

This repo is a hands-on demo of two closely related ways to organize knowledge so that **both humans and AI agents** can read, maintain, and build on it:

| | [`karpathy-llm-wiki/`](./karpathy-llm-wiki/) | [`google-okf/`](./google-okf/) |
|---|---|---|
| **What it is** | A *pattern*: an LLM incrementally builds and maintains a personal wiki of markdown pages | A *specification*: Google's Open Knowledge Format (OKF) v0.1, which formalizes the llm-wiki pattern into a portable, interoperable bundle format |
| **Origin** | Andrej Karpathy's gist, April 2026 | Google Cloud announcement, June 12, 2026 |
| **Unit of knowledge** | An entity/concept page (one markdown file) | A "concept" document (one markdown file with YAML frontmatter) |
| **Structure** | Three layers: raw sources → wiki → schema (`CLAUDE.md`) | A bundle: a directory tree of concept files, plus reserved `index.md` / `log.md` files |
| **Linking** | Obsidian-style `[[wikilinks]]` (by convention) | Standard markdown links, bundle-absolute (`/tables/customers.md`) or relative |
| **Metadata** | Optional YAML frontmatter, conventions are yours to define | Required frontmatter: `type` is mandatory; `title`, `description`, `resource`, `tags`, `timestamp` recommended |
| **Sweet spot** | Personal / team knowledge that compounds: research notes, reading, projects | Organizational knowledge exchanged between tools and agents: tables, metrics, APIs, runbooks |

## Why these two together?

Karpathy's insight: the tedious part of maintaining a knowledge base is not the reading or the thinking — it's the **bookkeeping**. LLMs don't get bored, don't forget to update a cross-reference, and can touch 15 files in one pass. So let the LLM own the wiki; the human curates sources and asks questions.

Google's OKF takes that pattern and pins down just enough convention (frontmatter, reserved filenames, linking rules, conformance criteria) that a wiki written by one producer/agent can be consumed by any other agent **without translation**. Producers export knowledge to OKF once; every agent benefits.

In short: **llm-wiki is the workflow, OKF is the wire format.**

## What's in this repo

Both demos use the same knowledge domain — **Anthropic and the Claude models** (model lineup, pricing, the Messages API, prompt caching) — so you can compare how the two formats organize identical knowledge.

```
.
├── karpathy-llm-wiki/        Demo of the llm-wiki pattern
│   ├── README.md             The pattern explained
│   ├── CLAUDE.md             The "schema" layer — conventions the LLM follows
│   ├── sources/              Layer 1: immutable raw sources (LLM reads, never edits)
│   └── wiki/                 Layer 2: the LLM-maintained wiki
│       ├── index.md          Catalog of all pages, by category
│       ├── log.md            Append-only operation log
│       ├── summaries/        One summary page per ingested source
│       ├── concepts/         Concept pages (model lineup, adaptive thinking, caching)
│       └── entities/         Entity pages (Anthropic)
│
└── google-okf/               Demo of Open Knowledge Format v0.1
    ├── README.md             The spec explained
    └── bundle/               A conformant OKF bundle about the Claude platform
        ├── index.md          Bundle root index (declares okf_version)
        ├── log.md            Change history
        ├── models/           One concept file per Claude model
        ├── api/              The Messages API concept
        ├── guides/           Prompt caching guide
        └── playbooks/        Model migration playbook
```

Each folder's own `README.md` walks through the format in detail. Every file follows the real conventions, so you can use either folder as a starting template for your own knowledge.

## Try it yourself

1. **llm-wiki**: copy `karpathy-llm-wiki/` into a new repo, replace the sources with your own documents, point Claude Code (or any coding agent) at it, and say *"ingest sources/<file>"*. The `CLAUDE.md` tells the agent everything else.
2. **OKF**: copy `google-okf/bundle/`, replace the concepts with your own tables/metrics/runbooks, and any OKF-aware agent can consume it as grounding context.

## Sources

- Andrej Karpathy, [llm-wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) (April 2026)
- Google Cloud, [How the Open Knowledge Format can improve data sharing](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) (June 12, 2026)
- [OKF v0.1 specification](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md) (`GoogleCloudPlatform/knowledge-catalog`)
