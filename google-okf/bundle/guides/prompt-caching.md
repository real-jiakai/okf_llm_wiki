---
type: Guide
title: Prompt caching
description: How prefix caching works and how to avoid silent cache misses.
resource: https://platform.claude.com/docs/en/build-with-claude/prompt-caching
tags: [anthropic, api, cost-optimization]
timestamp: 2026-07-04T00:00:00Z
---

Prompt caching is a **prefix match**: the cache key is the exact bytes of the rendered prompt up to each `cache_control` breakpoint. Any byte change anywhere in the prefix — a timestamp, a reordered JSON key, a different tool — invalidates everything after it. Render order is `tools` → `system` → `messages`, so keep stable content first and volatile content last.

# Schema

| Fact | Value |
|------|-------|
| Marker | `"cache_control": {"type": "ephemeral"}` on a content block |
| TTL | 5 minutes default; `"ttl": "1h"` available |
| Cache read cost | ~0.1× base input price |
| Cache write cost | 1.25× (5m TTL) or 2× (1h TTL) base input price |
| Max breakpoints | 4 per request |
| Verify hits | `usage.cache_read_input_tokens` in the response |

# Examples

```python
response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=1024,
    system=[{
        "type": "text",
        "text": LARGE_STABLE_PROMPT,
        "cache_control": {"type": "ephemeral"},
    }],
    messages=[{"role": "user", "content": "Summarize the key points"}],
)
```

If `cache_read_input_tokens` stays zero across identical requests, hunt for a silent invalidator: `datetime.now()` in the system prompt, unsorted JSON serialization, or a tool set that varies per request.

# Citations

[1] [Prompt caching — Claude docs](https://platform.claude.com/docs/en/build-with-claude/prompt-caching)
