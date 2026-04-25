# Documentation Sources Registry

This file tracks every official documentation source used by prompting-pro.  
Update it whenever a source changes or a new model reference is added.

## Format

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|

## OpenAI

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|
| OpenAI | All models — Prompt Engineering Guide | https://platform.openai.com/docs/guides/prompt-engineering | 2025-04 | 2025-04 | active |
| OpenAI | o1 / o1-mini — Reasoning Models Guide | https://platform.openai.com/docs/guides/reasoning | 2025-04 | 2025-04 | active |
| OpenAI | GPT-4o — Model overview | https://platform.openai.com/docs/models/gpt-4o | 2025-04 | 2025-04 | active |
| OpenAI | Function calling | https://platform.openai.com/docs/guides/function-calling | 2025-04 | 2025-04 | active |
| OpenAI | Vision / Multimodal | https://platform.openai.com/docs/guides/vision | 2025-04 | 2025-04 | active |

## Notes

- **Status** values: `active` (content current), `outdated` (needs review), `archived` (model deprecated).
- Add rows for new providers (Anthropic, Google, Meta …) under a new `## <Provider>` section.
- A source is considered **outdated** if it has not been checked within 90 days or if the provider has published a newer version.
