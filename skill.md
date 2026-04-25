---
name: prompting-pro
description: Help formulate high-quality prompts for GPT-5.5, GPT-5.4, GPT-5.3-Codex, Gemini 3, and Nano Banana.
---

# Prompting Pro

## Purpose

Help formulate high-quality prompts for specific AI models based on official documentation and curated unofficial tips.

## Usage

1. **Identify the target model** (e.g. `gpt-5.5`, `gpt-5.4`, `gpt-5.3-codex`, `gemini-3`, `nano-banana`).
2. **Describe your task** — what you want the model to do.
3. The skill applies model-specific guidance and returns an optimised prompt.

## Supported Models

| Model | Reference Doc | Tips |
|-------|--------------|------|
| GPT-5.5 | [docs/openai/gpt-5.5.md](docs/openai/gpt-5.5.md) | [tips/openai/gpt-5.5.md](tips/openai/gpt-5.5.md) |
| GPT-5.4 | [docs/openai/gpt-5.4.md](docs/openai/gpt-5.4.md) | [tips/openai/gpt-5.4.md](tips/openai/gpt-5.4.md) |
| GPT-5.3-Codex | [docs/openai/gpt-5.3-codex.md](docs/openai/gpt-5.3-codex.md) | [tips/openai/gpt-5.3-codex.md](tips/openai/gpt-5.3-codex.md) |
| Gemini 3 | [docs/google/gemini-3.md](docs/google/gemini-3.md) | - |
| Nano Banana | [docs/google/nano-banana.md](docs/google/nano-banana.md) | - |

### Mini variants

- `gpt-5.4-mini` and `gpt-5.4-nano` are considered operational variants of the GPT-5.4 family.
- They are not documented as standalone models in this repository.
- Use them for cost/latency-sensitive routing and keep prompt shape compatible with GPT-5.4 guidance.

General tips that apply across all models: [tips/general.md](tips/general.md)

## Suggested Prompt Structure

Use this compact structure for complex prompts, then specialize by model:

```text
Role: <1-2 sentence role definition>

# Personality
<tone and collaboration style>

# Goal
<target outcome>

# Success criteria
<what must be true before final answer>

# Constraints
- <policy / safety / business limits>
- <evidence and tool limits>

# Output
<format, length, audience>

# Stop rules
<when to continue, ask, fallback, or stop>
```

## Adding a New Model

1. Add a reference doc in `docs/<provider>/<model>.md` (official guidance only).
2. Optionally add tips in `tips/<provider>/<model>.md` (unofficial / community tips).
3. Register the official documentation source in `knowledge/sources/<provider>.md` (and in [knowledge/sources.md](knowledge/sources.md) only if it is a new provider).
4. Add a row to the table above.

## Repository Layout

```
skill.md            ← this file (kept compact)
docs/               ← official model-specific prompt guidance
knowledge/          ← registry of documentation sources (self-learning)
tips/               ← unofficial tips, general and model-specific
```
