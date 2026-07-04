---
kind: concept
tags: [claude, api, cost-optimization]
updated: 2026-07-04
---

# Prompt caching

[[anthropic]]'s mechanism for making repeated large contexts cheap on the Claude API.

**The one invariant: it's a prefix match.** The cache key is the exact bytes of the rendered prompt up to each `cache_control` breakpoint, in render order `tools` → `system` → `messages`. Any byte change anywhere in the prefix invalidates everything after it.

Mechanics:

- Mark blocks with `"cache_control": {"type": "ephemeral"}`; max 4 breakpoints per request.
- TTL is 5 minutes by default (`"1h"` available). Reads cost ~0.1× the input price; writes cost 1.25× (5m) or 2× (1h).
- Verify with `usage.cache_read_input_tokens`. Zero reads on identical requests means a *silent invalidator*: a timestamp in the system prompt, unsorted JSON serialization, or a tool set that varies per request.
- Caches are model-scoped — switching models in the [[claude-model-lineup]] rewrites the cache.

Design rule: freeze the system prompt, serialize tools deterministically, and push volatile content after the last breakpoint.

## Sources

- [[prompt-caching-docs]] → `sources/2026-07-prompt-caching-docs.md`
