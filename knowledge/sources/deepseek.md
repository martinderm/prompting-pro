# DeepSeek Documentation Sources

This file tracks official and community sources used by prompting-pro.

## Format

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|

## Official Sources

| Provider | Model / Scope | URL | First added | Last checked | Status |
|----------|--------------|-----|-------------|--------------|--------|
| DeepSeek | Chat Completions API reference (model IDs, thinking, reasoning_effort, sampling, tools, response_format, vision blocks, usage/cache fields) | <https://api-docs.deepseek.com/api/create-chat-completion/> | 2026-11 | 2026-11 | active |
| DeepSeek | Thinking Mode guide (toggle + effort mapping, multi-turn reasoning_content rules, tool-loop replay) | <https://api-docs.deepseek.com/guides/thinking_mode/> | 2026-11 | 2026-11 | active |
| DeepSeek | Vision guide (image_url / base64 / Files API, detail levels, limits, token usage) | <https://api-docs.deepseek.com/guides/vision/> | 2026-11 | 2026-11 | active |
| DeepSeek | Tool Calls guide (JSON schema functions, strict mode beta, web tools) | <https://api-docs.deepseek.com/guides/tool_calls/> | 2026-11 | 2026-11 | active |
| DeepSeek | JSON Output guide (response_format json_object + prompt instruction required) | <https://api-docs.deepseek.com/guides/json_mode/> | 2026-11 | 2026-11 | active |
| DeepSeek | Models & Pricing (deepseek-flash served by V4.1-Flash-1017; 1M context, 384K max output; peak/off-peak; cache-hit pricing; retired aliases) | <https://api-docs.deepseek.com/quick_start/pricing/> | 2026-11 | 2026-11 | active |
| DeepSeek | API docs home / first call (base_url https://api.deepseek.com, quick start) | <https://api-docs.deepseek.com/> | 2026-11 | 2026-11 | active |
| DeepSeek | Change Log (V4 family release, legacy ID retirements, pricing changes) | <https://api-docs.deepseek.com/updates/> | 2026-11 | 2026-11 | active |
| DeepSeek | News: DeepSeek-V4.1-Flash-1017 (2026-10-17) | <https://api-docs.deepseek.com/news/news261017/> | 2026-11 | 2026-11 | active |
| DeepSeek | Hugging Face model card DeepSeek-V4.1-Flash-1017 (MIT weights, prompt format reference) | <https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017> | 2026-11 | 2026-11 | active |
| Mistral AI | Third-party hosting on La Plateforme: `vv4.1-flash-1017` model card (public preview, text+image, 1M ctx, 128k out, long-context coding/agentic) | <https://docs.mistral.ai/models/deepseek-v4-flash-1017> | 2026-11 | 2026-11 | active |
| Mistral AI | Models overview (third-party models section) | <https://docs.mistral.ai/models> | 2026-11 | 2026-11 | active |

## Community Sources

Use these compact references when citing community input in docs and tips.

| Ref | Source | URL | First added | Last checked | Status |
|-----|--------|-----|-------------|--------------|--------|
| [1] | Prompt Engineering Guide (community curation; shared with the other provider registries) | <https://www.promptingguide.ai/> | 2026-11 | 2026-11 | active |

## Notes

- **Status** values: `active` (content current), `outdated` (needs review), `archived` (model deprecated).
- A source is considered **outdated** if it has not been checked within 90 days or if DeepSeek has published a newer version.
- Retired API IDs still route to DeepSeek-V4.1-Flash-1017 at the Flash price but should not be used in new code: `deepseek-chat`, `deepseek-reasoner` (retired 2026-07-24), `deepseek-v4-flash`, `deepseek-v4-flash-vision-exp` (retired 2026-09-10). Current IDs: `deepseek-flash`, `deepseek-v4-pro`.
- `deepseek-v4-pro` (1.6T / 49B active, text-only, no vision) is the larger sibling and not yet covered by a dedicated `docs/` file.
- The same model is hosted third-party on Mistral La Plateforme as `vv4.1-flash-1017`; cross-reference [mistral.md](mistral.md).
