# Source: Anthropic docs — Prompt caching

- URL: https://platform.claude.com/docs/en/build-with-claude/prompt-caching
- Captured: 2026-07-04 (reading notes on Anthropic's public documentation)

## Notes

Prompt caching lets repeated large contexts (system prompts, documents, tool definitions) be reused across requests at ~0.1× the input price.

Core mechanics:

- It is a **prefix match** on the exact rendered bytes, in render order `tools` → `system` → `messages`. One changed byte invalidates everything after it.
- Mark cache points with `"cache_control": {"type": "ephemeral"}` on a content block; max 4 breakpoints per request.
- TTL: 5 minutes by default, `"1h"` available. Writes cost 1.25× (5m) or 2× (1h); reads ~0.1×.
- Verify with `usage.cache_read_input_tokens`; if it's zero on identical requests, a "silent invalidator" is at work (timestamps in the system prompt, unsorted JSON, per-request tool sets).
- Changing the model invalidates the cache — caches are model-scoped.

Design implication: freeze the system prompt, serialize tools deterministically, and put volatile content (per-request questions, timestamps) after the last breakpoint.
