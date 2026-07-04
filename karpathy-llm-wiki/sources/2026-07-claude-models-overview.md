# Source: Anthropic docs — Claude models overview & pricing

- URL: https://platform.claude.com/docs/en/about-claude/models/overview and https://platform.claude.com/docs/en/pricing
- Captured: 2026-07-04 (reading notes on Anthropic's public documentation)

## Notes

Claude ships in tiers trading capability against speed and cost. Current lineup (July 2026):

- **Claude 5 family** — a new Mythos-class tier above Opus: Claude Fable 5 (generally available, $10/$50 per MTok, 1M context) and Claude Mythos 5 (same model, available to approved organizations via Project Glasswing). Announcement: https://www.anthropic.com/news/claude-fable-5-mythos-5
- **Claude Opus 4.8** (`claude-opus-4-8`) — most capable Opus-tier model; $5/$25 per MTok; 1M context, 128K max output; recommended default for coding and agents.
- **Claude Sonnet 5** (`claude-sonnet-5`) — near-Opus quality on coding at $3/$15 ($2/$10 introductory through 2026-08-31); 1M context; new tokenizer (~30% more tokens for the same text than the prior Sonnet).
- **Claude Haiku 4.5** (`claude-haiku-4-5`) — fastest/cheapest at $1/$5; 200K context, 64K max output.

API surface notes: on Opus 4.7+ and Sonnet 5, extended-thinking `budget_tokens` is removed in favor of **adaptive thinking** (`thinking: {type: "adaptive"}`), controlled by an `effort` parameter (`low`–`max`, with `xhigh` added in Opus 4.7); sampling parameters (`temperature`/`top_p`/`top_k`) are removed; assistant prefills return 400.

Everything is served by a single stateless endpoint, `POST /v1/messages`.
