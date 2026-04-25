# Documentation Sources Registry

This file tracks every official documentation source used by prompting-pro.  
Update it whenever a source changes or a new model reference is added.

## Format

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|

## OpenAI

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|
| OpenAI | GPT-5.5 — Model overview | <https://developers.openai.com/api/docs/models/gpt-5.5> | 2026-04 | 2026-04 | active |
| OpenAI | GPT-5.4 — Model overview | <https://developers.openai.com/api/docs/models/gpt-5.4> | 2026-04 | 2026-04 | active |
| OpenAI | GPT-5.3-Codex — Model overview | <https://developers.openai.com/api/docs/models/gpt-5.3-codex> | 2026-04 | 2026-04 | active |
| OpenAI | Model catalog (variants incl. mini/nano) | <https://developers.openai.com/api/docs/models> | 2026-04 | 2026-04 | active |
| OpenAI | Prompt guidance (general) | <https://developers.openai.com/api/docs/guides/prompt-engineering> | 2026-04 | 2026-04 | active |
| OpenAI | Reasoning guide | <https://developers.openai.com/api/docs/guides/reasoning> | 2026-04 | 2026-04 | active |
| OpenAI | Function calling | <https://developers.openai.com/api/docs/guides/function-calling> | 2026-04 | 2026-04 | active |
| OpenAI | Images and vision | <https://developers.openai.com/api/docs/guides/images> | 2026-04 | 2026-04 | active |
| OpenAI | GPT-5.3-Codex prompting guide (Cookbook) | <https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide> | 2026-04 | 2026-04 | active |

## Notes

- **Status** values: `active` (content current), `outdated` (needs review), `archived` (model deprecated).
- Add rows for new providers (Anthropic, Google, Meta …) under a new `## <Provider>` section.
- A source is considered **outdated** if it has not been checked within 90 days or if the provider has published a newer version.
