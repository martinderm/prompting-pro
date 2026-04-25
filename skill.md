---
name: prompting-pro
description: Help formulate high-quality prompts for GPT-5.5, GPT-5.4, GPT-5.3-Codex, Gemini 3, and Nano Banana.
---

# Prompting Pro

## Purpose

Help formulate high-quality prompts for specific AI models based on official documentation and curated unofficial tips.

The skill can also operate in a lightweight maintenance mode: on request, it can re-check registered sources, look for newly published models or updated prompting guidance, and update the matching files in `knowledge/`, `docs/`, and `tips/`.

## Usage

1. **Identify the target model** (e.g. `gpt-5.5`, `gpt-5.4`, `gpt-5.3-codex`, `gemini-3`, `nano-banana`).
2. **Describe your task** — what you want the model to do.
3. The skill applies model-specific guidance and returns an optimised prompt.

For maintenance or discovery requests, ask explicitly for a source refresh or provider check.

## Supported Models

| Model | Reference Doc | Tips |
|-------|--------------|------|
| GPT-5.5 | [docs/openai/gpt-5.5.md](docs/openai/gpt-5.5.md) | [tips/openai/gpt-5.5.md](tips/openai/gpt-5.5.md) |
| GPT-5.4 | [docs/openai/gpt-5.4.md](docs/openai/gpt-5.4.md) | [tips/openai/gpt-5.4.md](tips/openai/gpt-5.4.md) |
| GPT-5.3-Codex | [docs/openai/gpt-5.3-codex.md](docs/openai/gpt-5.3-codex.md) | [tips/openai/gpt-5.3-codex.md](tips/openai/gpt-5.3-codex.md) |
| Gemini 3 | [docs/google/gemini-3.md](docs/google/gemini-3.md) | - |
| Nano Banana | [docs/google/nano-banana.md](docs/google/nano-banana.md) | [tips/google/nano-banana.md](tips/google/nano-banana.md) |

### Mini variants

- `gpt-5.4-mini` and `gpt-5.4-nano` are considered operational variants of the GPT-5.4 family.
- They are not documented as standalone models in this repository.
- Use them for cost/latency-sensitive routing and keep prompt shape compatible with GPT-5.4 guidance.

General tips that apply across all models: [tips/general.md](tips/general.md)

## Self-Learning Maintenance Requests

Use these request patterns when you want the skill to update its knowledge base on demand:

- `Check <provider> for new models or prompt-guidance updates.`
- `Refresh all outdated sources for <provider>.`
- `Compare the registered sources with the current provider docs.`
- `Add a newly discovered official model to knowledge and docs.`
- `Evaluate a new blog post as a community tip and wire it into tips/ and knowledge/.`

Expected workflow:

1. Revisit the relevant URLs in `knowledge/sources/<provider>.md`.
2. Identify new models, changed guidance, or newly relevant community sources.
3. Classify findings as official or community.
4. Update the matching files in `knowledge/`, `docs/`, and `tips/`.
5. Keep source registries, model tables, and file references consistent.

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
