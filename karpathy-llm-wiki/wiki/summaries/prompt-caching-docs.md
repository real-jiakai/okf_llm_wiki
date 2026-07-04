---
kind: summary
tags: [source-summary, prompt-caching]
updated: 2026-07-04
---

# Summary: Prompt caching (Anthropic docs)

Source: `sources/2026-07-prompt-caching-docs.md` · [original docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)

## Key takeaways

- Caching is a byte-exact **prefix match** in render order `tools` → `system` → `messages` — details in [[prompt-caching]].
- Economics: reads ~0.1×, writes 1.25×–2× depending on TTL; break-even after roughly two requests on the default TTL.
- The failure mode is silent: watch `usage.cache_read_input_tokens` and hunt for invalidators (timestamps, unsorted JSON, varying tools).
- Caches are model-scoped, which links cache strategy to [[claude-model-lineup]] choices.

## Open questions

- How should an agent structure a *wiki like this one* to be cache-friendly when injected as context? (Stable pages first, volatile pages last.)
