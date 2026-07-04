---
type: Playbook
title: Model migration
description: Checklist for moving code to a newer Claude model.
resource: https://platform.claude.com/docs/en/about-claude/models/migration-guide
tags: [anthropic, migration, oncall]
timestamp: 2026-07-04T00:00:00Z
---

Follow this when upgrading application code to a newer Claude model (e.g. to [Claude Opus 4.8](../models/claude-opus-4-8.md) or [Claude Sonnet 5](../models/claude-sonnet-5.md)).

# Steps

1. **Confirm the scope** — which files/services call the API — before editing anything.
2. **Swap the model ID** to the exact new alias (never invent date suffixes).
3. **Replace fixed thinking budgets**: `thinking: {"type": "enabled", "budget_tokens": N}` returns a 400 on Opus 4.7+ and Sonnet 5 — use `thinking: {"type": "adaptive"}` plus `output_config: {"effort": ...}`.
4. **Remove sampling parameters** (`temperature`, `top_p`, `top_k`) — rejected on Opus 4.7+; steer with prompting instead.
5. **Remove assistant-turn prefills** — they 400 on current models; use structured outputs (`output_config.format`) instead.
6. **Re-baseline token counts** with the `count_tokens` endpoint — tokenizers changed across generations, so `max_tokens` limits and cost dashboards need refreshing.
7. **Run one test request** and check `response.model`, `stop_reason`, and `usage` before rolling out.

# Examples

Note that changing the model string invalidates the existing [prompt cache](../guides/prompt-caching.md) — the first request on the new model rewrites the cache.

# Citations

[1] [Model migration guide — Claude docs](https://platform.claude.com/docs/en/about-claude/models/migration-guide)
