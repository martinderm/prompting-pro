---
name: prompting-pro
description: Help formulate high-quality prompts for GPT-5.5, GPT-5.4, GPT-5.3-Codex, Gemini 3, and Nano Banana.
---

# Prompting Pro

## Purpose

Help formulate high-quality prompts for specific AI models based on official documentation and curated unofficial tips.

The skill can also operate in a lightweight maintenance mode: on request, it can re-check registered sources, look for newly published models or updated prompting guidance, and update the matching files in `knowledge/`, `docs/`, and `tips/`.

## Usage

1. **Identify the target or active model** (e.g. `gpt-5.5`, `gpt-5.4`, `gpt-5.3-codex`, `gemini-3`, `nano-banana`).
2. **Read the relevant docs and tips** for that model (official reference doc, community tips) from supported models. If model is missing inform user.
3. **Check specialized overlays** and add matching overlays for the task type.
4. **Formulate the prompt** with model-specific constraints, output format, and stop rules.

Overlay routing rule: if an overlay applies, combine model doc + model tips + overlay.

For maintenance or discovery requests, see [knowledge/maintenance-requests.md](knowledge/maintenance-requests.md).

## Supported Models

| Model | Reference Doc | Tips |
|-------|--------------|------|
| GPT-5.5 | [docs/openai/gpt-5.5.md](docs/openai/gpt-5.5.md) | [tips/openai/gpt-5.5.md](tips/openai/gpt-5.5.md) |
| GPT-5.4 | [docs/openai/gpt-5.4.md](docs/openai/gpt-5.4.md) | [tips/openai/gpt-5.4.md](tips/openai/gpt-5.4.md) |
| GPT-5.3-Codex | [docs/openai/gpt-5.3-codex.md](docs/openai/gpt-5.3-codex.md) | [tips/openai/gpt-5.3-codex.md](tips/openai/gpt-5.3-codex.md) |
| Gemini 3 | [docs/google/gemini-3.md](docs/google/gemini-3.md) | - |

## Specialized Overlays

Use these as additional instruction layers for specific task classes.

| Overlay | Applies to | Use when | Reference Doc | Tips |
|---------|------------|----------|---------------|------|
| OpenAI Codex Overlay | `gpt-5.5`, `gpt-5.4`, `gpt-5.4-mini`, `gpt-5.4-nano`, `gpt-5.3-codex` | coding, debugging, verification-heavy tasks | Model-specific docs from Supported Models | [tips/openai/codex.md](tips/openai/codex.md) |
| Nano Banana Image Overlay | `nano-banana` | image generation or editing tasks | [docs/google/nano-banana.md](docs/google/nano-banana.md) | [tips/google/nano-banana.md](tips/google/nano-banana.md) |

### Mini variants

- `gpt-5.4-mini` and `gpt-5.4-nano` are considered operational variants of the GPT-5.4 family.
- They are not documented as standalone models in this repository.
- Use them for cost/latency-sensitive routing and keep prompt shape compatible with GPT-5.4 guidance.

General tips that apply across all models: [tips/general.md](tips/general.md)

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
