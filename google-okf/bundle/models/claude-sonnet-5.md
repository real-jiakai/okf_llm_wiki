---
type: Model
title: Claude Sonnet 5
description: Best speed/intelligence balance; near-Opus quality on coding at Sonnet cost.
resource: https://platform.claude.com/docs/en/about-claude/models/overview
tags: [anthropic, claude, sonnet]
timestamp: 2026-07-04T00:00:00Z
---

The workhorse tier: near-Opus quality on coding and agentic work at Sonnet cost. Recommended for high-volume production workloads.

# Schema

| Property | Value |
|----------|-------|
| Model ID | `claude-sonnet-5` |
| Context window | 1M tokens |
| Max output | 128K tokens |
| Pricing | $3 / $15 per million input/output tokens ($2 / $10 introductory through 2026-08-31) |
| Thinking | Adaptive by default — omitting `thinking` runs adaptive; `{"type": "disabled"}` turns it off |
| Effort | Full range `low` / `medium` / `high` / `xhigh` / `max` — first Sonnet with `xhigh` |
| Tokenizer | New — ~30% more tokens for the same text vs the previous Sonnet generation; re-baseline token budgets with `count_tokens` |

# Examples

Rule of thumb for tier selection: default to [Opus 4.8](./claude-opus-4-8.md) for the hardest work, Sonnet 5 for high-volume production, [Haiku 4.5](./claude-haiku-4-5.md) for simple speed-critical tasks.

# Citations

[1] [Models overview — Claude docs](https://platform.claude.com/docs/en/about-claude/models/overview)
[2] [Pricing — Claude docs](https://platform.claude.com/docs/en/pricing)
