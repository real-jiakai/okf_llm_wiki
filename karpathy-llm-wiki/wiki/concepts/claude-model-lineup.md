---
kind: concept
tags: [claude, models, pricing]
updated: 2026-07-04
---

# Claude model lineup

[[anthropic]]'s models come in tiers trading capability against speed and cost (as of July 2026):

| Tier | Model ID | Context | Pricing (in/out per MTok) | Sweet spot |
|------|----------|---------|---------------------------|------------|
| Claude 5 family (Fable 5 / Mythos 5) | — | 1M | $10 / $50 | Most demanding reasoning and long-horizon agentic work |
| Opus 4.8 | `claude-opus-4-8` | 1M | $5 / $25 | Default for coding and agents |
| Sonnet 5 | `claude-sonnet-5` | 1M | $3 / $15 (intro $2 / $10 through 2026-08-31) | High-volume production |
| Haiku 4.5 | `claude-haiku-4-5` | 200K | $1 / $5 | Fast, cheap, simple tasks |

Notes:

- The Claude 5 family is a new Mythos-class tier above Opus; Fable 5 is generally available, Mythos 5 is limited to approved organizations via Project Glasswing.
- Max output is 128K tokens on the 1M-context models (streaming required) and 64K on Haiku 4.5.
- Model IDs are exact strings — never append date suffixes to aliases.
- Reasoning depth on current models is controlled via [[adaptive-thinking]]; switching models invalidates any [[prompt-caching]] entries, since caches are model-scoped.

## Sources

- [[claude-models-overview]] → `sources/2026-07-claude-models-overview.md`
