---
kind: concept
tags: [claude, api, reasoning]
updated: 2026-07-04
---

# Adaptive thinking

How reasoning is controlled on current Claude models (see [[claude-model-lineup]]).

Older models used a fixed thinking budget: `thinking: {type: "enabled", budget_tokens: N}`. On Opus 4.7+ and Sonnet 5 that form is **removed** (returns a 400). Instead:

- `thinking: {type: "adaptive"}` — the model decides when and how much to think, and automatically interleaves thinking between tool calls.
- `output_config: {effort: "low" | "medium" | "high" | "xhigh" | "max"}` — the depth/cost dial. `high` is the default; `xhigh` (added with Opus 4.7) is the recommended setting for hard coding and agentic work.
- Sampling parameters (`temperature`, `top_p`, `top_k`) are removed on the same models — behavior is steered by prompting, not sampling knobs.

On Sonnet 5, omitting `thinking` entirely runs adaptive by default; the visible thinking text defaults to omitted (`display: "summarized"` opts back into readable summaries).

## Sources

- [[claude-models-overview]] → `sources/2026-07-claude-models-overview.md`
