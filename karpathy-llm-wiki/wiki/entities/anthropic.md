---
kind: entity
tags: [organization, ai]
updated: 2026-07-04
---

# Anthropic

AI safety and research company; maker of the Claude family of models and the Claude API. Ships models in capability tiers (see [[claude-model-lineup]]) served through a single stateless endpoint, `POST /v1/messages`.

Notable platform design choices covered in this wiki: reasoning is controlled through [[adaptive-thinking]] rather than fixed token budgets, and repeated context is made cheap through [[prompt-caching]].

## Sources

- [[claude-models-overview]] → `sources/2026-07-claude-models-overview.md`
- [[prompt-caching-docs]] → `sources/2026-07-prompt-caching-docs.md`
