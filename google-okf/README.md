# Google's Open Knowledge Format (OKF) — Demo

On June 12, 2026, Google Cloud [announced](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) the **Open Knowledge Format (OKF)** — an open, vendor-neutral specification for the knowledge AI agents need: table schemas, metric definitions, runbooks, API docs. It formalizes Andrej Karpathy's [llm-wiki pattern](../karpathy-llm-wiki/) (see that folder) into a portable, interoperable format. The [v0.1 spec](https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md) intentionally fits on a single page.

Design goals: **readable by humans without tooling, parseable by agents without bespoke SDKs, diffable in version control, portable across tools, organizations, and time.**

## The spec in five rules

1. **A bundle is a directory of markdown files.** Distribute it as a git repo, tarball, zip, or a subdirectory of a larger repo (like [`bundle/`](./bundle/) here). Each non-reserved `.md` file is one **concept** — a table, metric, API, playbook, anything.

2. **Every concept file has YAML frontmatter.** `type` is the only *required* field (free-form, e.g. `BigQuery Table`, `Playbook`). Recommended: `title`, `description`, `resource` (URI of the underlying asset), `tags`, `timestamp` (ISO 8601). Producers may add extra keys; consumers must tolerate and preserve unknown ones.

3. **`index.md` and `log.md` are reserved.** `index.md` is a per-directory catalog for progressive disclosure (grouped `* [Title](url) - description` entries, no frontmatter — except the bundle root may declare `okf_version`). `log.md` records change history, newest first, under `## YYYY-MM-DD` headings.

4. **Cross-links are plain markdown links.** The spec recommends bundle-absolute paths like `/tables/customers.md`; relative paths like `./customers.md` are also fine. Links assert relationships; the prose around them supplies the semantics. Consumers must tolerate broken links.

5. **Consumption is permissive.** Missing optional fields, unknown `type` values, unrecognized frontmatter keys, broken links, missing indexes — none of these are grounds for rejecting a bundle.

> **Note on links in this demo:** we use *relative* links inside the bundle so navigation works when browsing on GitHub. In a bundle consumed by agents, the spec's bundle-absolute form (`/tables/customers.md`) is the recommended default.

## Anatomy of a concept file

From [`bundle/models/claude-haiku-4-5.md`](./bundle/models/claude-haiku-4-5.md) in this demo:

```markdown
---
type: Model
title: Claude Haiku 4.5
description: Fastest and most cost-effective model for simple tasks.
resource: https://platform.claude.com/docs/en/about-claude/models/overview
tags: [anthropic, claude, haiku]
timestamp: 2026-07-04T00:00:00Z
---

The small, fast tier — for classification, routing, extraction...

# Schema
| Property | Value |
|----------|-------|
| Model ID | `claude-haiku-4-5` |
| Context window | 200K tokens |

# Citations
[1] [Models overview — Claude docs](https://platform.claude.com/docs/en/about-claude/models/overview)
```

Body sections are free-form markdown; `# Schema`, `# Examples`, and `# Citations` are conventional headings consumers may look for. (The original announcement's example was a BigQuery `Orders` table with `type: BigQuery Table` — any descriptive `type` string works.)

## The demo bundle

[`bundle/`](./bundle/) is a conformant OKF v0.1 bundle about **Anthropic's Claude platform** — the model lineup, the Messages API, prompt caching, and a migration playbook. Start at [`bundle/index.md`](./bundle/index.md) — the same entry point an agent would use:

```
bundle/
├── index.md                  Root catalog (declares okf_version: "0.1")
├── log.md                    Change history
├── models/                   One concept file per model (type: Model)
│   ├── index.md
│   ├── claude-opus-4-8.md
│   ├── claude-sonnet-5.md
│   └── claude-haiku-4-5.md
├── api/
│   ├── index.md
│   └── messages-api.md       An API endpoint concept (type: API Endpoint)
├── guides/
│   ├── index.md
│   └── prompt-caching.md     A how-it-works guide (type: Guide)
└── playbooks/
    ├── index.md
    └── model-migration.md    An operational checklist (type: Playbook)
```

Why this matters: an agent asked *"which Claude model should this service use, and what breaks when we upgrade?"* can read `index.md`, discover `models/`, compare pricing and context windows from the frontmatter and Schema tables, and follow links to the migration playbook and the caching guide (whose cache-invalidation warning is exactly the kind of tribal knowledge that usually lives in someone's head) — all without a proprietary catalog API.
