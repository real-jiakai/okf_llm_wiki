---
type: Model
title: Claude Opus 4.8
description: Anthropic's most capable Opus-tier model for long-horizon agentic work.
resource: https://platform.claude.com/docs/en/about-claude/models/overview
tags: [anthropic, claude, opus]
timestamp: 2026-07-04T00:00:00Z
---

The flagship Opus-tier model — highly autonomous, state-of-the-art on long-horizon agentic execution, knowledge work, and memory. The recommended default for coding and agent workloads.

# Schema

| Property | Value |
|----------|-------|
| Model ID | `claude-opus-4-8` |
| Context window | 1M tokens (standard pricing, no long-context premium) |
| Max output | 128K tokens (streaming required for large outputs) |
| Pricing | $5 / $25 per million input/output tokens |
| Thinking | Adaptive only (`thinking: {"type": "adaptive"}`); fixed `budget_tokens` removed |
| Sampling params | `temperature` / `top_p` / `top_k` removed — steer with prompting |
| Vision | High-resolution (up to 2576 px long edge) |
| Fast mode | Supported (beta) — same model, up to 2.5× output speed at premium pricing |

# Examples

```python
import anthropic

client = anthropic.Anthropic()
response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=16000,
    thinking={"type": "adaptive"},
    output_config={"effort": "high"},
    messages=[{"role": "user", "content": "Explain prompt caching in one paragraph."}],
)
```

For upgrade steps from older models, see the [model migration playbook](../playbooks/model-migration.md).

# Citations

[1] [Models overview — Claude docs](https://platform.claude.com/docs/en/about-claude/models/overview)
