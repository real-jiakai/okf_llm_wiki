---
type: API Endpoint
title: Messages API
description: The single endpoint behind every Claude request.
resource: https://api.anthropic.com/v1/messages
tags: [anthropic, api]
timestamp: 2026-07-04T00:00:00Z
---

Everything goes through `POST /v1/messages` — chat, vision, tool use, structured outputs, and thinking are all features of this one endpoint, not separate APIs. The API is stateless: send the full conversation history on every request.

# Schema

Required headers:

| Header | Value |
|--------|-------|
| `x-api-key` | Your API key |
| `anthropic-version` | `2023-06-01` |
| `content-type` | `application/json` |

Required body fields: `model` (see [models](../models/index.md)), `max_tokens`, and `messages` (first message must have role `user`).

# Examples

```bash
curl https://api.anthropic.com/v1/messages \
  -H "x-api-key: $ANTHROPIC_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "content-type: application/json" \
  -d '{
    "model": "claude-opus-4-8",
    "max_tokens": 1024,
    "messages": [{"role": "user", "content": "Hello, Claude"}]
  }'
```

Repeated large contexts should use [prompt caching](../guides/prompt-caching.md).

# Citations

[1] [Claude API reference](https://platform.claude.com/docs/en/api)
