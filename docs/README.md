# Model Prompt-Guidance Reference Docs

Each file in this directory contains **official** prompt-guidance for a specific model or model family, derived from the provider's public documentation.

## Index

| Provider | Model / Family | File | Source |
|----------|---------------|------|--------|
| OpenAI | GPT-4o | [openai/gpt-4o.md](openai/gpt-4o.md) | [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) |
| OpenAI | GPT-4 | [openai/gpt-4.md](openai/gpt-4.md) | [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) |
| OpenAI | o1 / o1-mini | [openai/o1.md](openai/o1.md) | [OpenAI o1 System Card & Docs](https://platform.openai.com/docs/guides/reasoning) |

## Conventions

- One file per model **version** (or closely related family where guidance is identical).
- Each file starts with a `Source` field linking to the canonical documentation page.
- Keep content faithful to the source; do not mix in unofficial tips (use `tips/` for that).
- When official guidance is updated, update the corresponding file and bump the `Last reviewed` date.
