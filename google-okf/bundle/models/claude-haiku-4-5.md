---
type: Model
title: Claude Haiku 4.5
description: Fastest and most cost-effective model for simple tasks.
resource: https://platform.claude.com/docs/en/about-claude/models/overview
tags: [anthropic, claude, haiku]
timestamp: 2026-07-04T00:00:00Z
---

The small, fast tier — for classification, routing, extraction, and other speed- or cost-critical tasks that don't need frontier intelligence.

# Schema

| Property | Value |
|----------|-------|
| Model ID | `claude-haiku-4-5` (full ID `claude-haiku-4-5-20251001`) |
| Context window | 200K tokens |
| Max output | 64K tokens |
| Pricing | $1 / $5 per million input/output tokens |

# Examples

```python
response = client.messages.create(
    model="claude-haiku-4-5",
    max_tokens=256,
    messages=[{"role": "user", "content": "Classify as positive/negative/neutral: 'It works great!'"}],
)
```

# Citations

[1] [Models overview — Claude docs](https://platform.claude.com/docs/en/about-claude/models/overview)
