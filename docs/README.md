# Model Prompt-Guidance Reference Docs

Each file in this directory contains **official** prompt-guidance for a specific model or model family, derived from the provider's public documentation.

## Index

| Provider | Model / Family | File | Source |
|----------|---------------|------|--------|
| OpenAI | GPT-5.5 | [openai/gpt-5.5.md](openai/gpt-5.5.md) | [GPT-5.5 model page](https://developers.openai.com/api/docs/models/gpt-5.5) |
| OpenAI | GPT-5.4 | [openai/gpt-5.4.md](openai/gpt-5.4.md) | [GPT-5.4 model page](https://developers.openai.com/api/docs/models/gpt-5.4) |
| OpenAI | GPT-5.3-Codex | [openai/gpt-5.3-codex.md](openai/gpt-5.3-codex.md) | [GPT-5.3-Codex model page](https://developers.openai.com/api/docs/models/gpt-5.3-codex) |
| Google | Gemini 3 family | [google/gemini-3.md](google/gemini-3.md) | [Gemini 3 guide](https://ai.google.dev/gemini-api/docs/gemini-3) |
| Google | Nano Banana image family | [google/nano-banana.md](google/nano-banana.md) | [Gemini image generation guide](https://ai.google.dev/gemini-api/docs/image-generation) |

## Conventions

- One file per model **version** (or closely related family where guidance is identical).
- Each file starts with a `Source` field linking to the canonical documentation page.
- Keep content faithful to the source; do not mix in unofficial tips (use `tips/` for that).
- When official guidance is updated, update the corresponding file and bump the `Last reviewed` date.
- Mini and nano variants (for example `gpt-5.4-mini`) are covered inside the corresponding family file, not as standalone docs.
