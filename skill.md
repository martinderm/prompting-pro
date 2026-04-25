# prompting-pro skill

## Purpose

Help formulate high-quality prompts for specific AI models based on official documentation and curated unofficial tips.

## Usage

1. **Identify the target model** (e.g. `gpt-4o`, `o1`, `claude-3-5-sonnet`).
2. **Describe your task** — what you want the model to do.
3. The skill applies model-specific guidance and returns an optimised prompt.

## Supported Models

| Model | Reference Doc | Tips |
|-------|--------------|------|
| GPT-4o | [docs/openai/gpt-4o.md](docs/openai/gpt-4o.md) | [tips/openai/gpt-4o.md](tips/openai/gpt-4o.md) |
| GPT-4 | [docs/openai/gpt-4.md](docs/openai/gpt-4.md) | — |
| o1 / o1-mini | [docs/openai/o1.md](docs/openai/o1.md) | [tips/openai/o1.md](tips/openai/o1.md) |

General tips that apply across all models: [tips/general.md](tips/general.md)

## Adding a New Model

1. Add a reference doc in `docs/<provider>/<model>.md` (official guidance only).
2. Optionally add tips in `tips/<provider>/<model>.md` (unofficial / community tips).
3. Register the official documentation source in [knowledge/sources.md](knowledge/sources.md).
4. Add a row to the table above.

## Repository Layout

```
skill.md            ← this file (kept compact)
docs/               ← official model-specific prompt guidance
knowledge/          ← registry of documentation sources (self-learning)
tips/               ← unofficial tips, general and model-specific
```
