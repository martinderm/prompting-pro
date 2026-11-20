# Codestral - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `codestral-2508` (alias `codestral-latest`) |
| **Provider** | Mistral AI |
| **Source** | [Codestral model card](https://docs.mistral.ai/models/codestral-25-08), [Models overview](https://docs.mistral.ai/models), [FIM API endpoint](https://docs.mistral.ai/api/endpoint/fim), [Chat API endpoint](https://docs.mistral.ai/api/endpoint/chat), [Prompting guide](https://docs.mistral.ai/guides/prompting_capabilities), [Vibe Code docs](https://docs.mistral.ai/vibe/code/overview) |
| **Last reviewed** | 2026-11 |

---

## Key Characteristics

- Premier-tier specialist model for code: low-latency, high-frequency tasks such as fill-in-the-middle (FIM) and code generation. Trained on 80+ programming languages.
- 128k context window; text input and output; status GA (released 2025-07-30, version 25.08).
- Features: FIM endpoint, chat completions, function calling, structured outputs, predicted outputs, document QnA, prefix, batching.
- Two usage modes: the dedicated `/v1/fim/completions` endpoint (prefix + suffix around the cursor) for IDE autocomplete, and `/v1/chat/completions` with `codestral-latest` for instruct-style coding tasks (generation, explanation, correction, test generation).

---

## What Codestral Is Not

- Codestral is a completion model, not an agentic planner. Multi-file refactors, autonomous PR work, or agent loops across a large codebase are not prompt-level use cases for Codestral.
- Agentic software-engineering work moved to `mistral-medium-3-5` / `mistral-large-4` / `mistral-small-4` and Mistral's Vibe Code agent (the Devstral line is deprecated; see the [models overview](https://docs.mistral.ai/models)).

---

## Official Prompting Guidance

The provider-wide [prompting guide](https://docs.mistral.ai/guides/prompting_capabilities) applies (shared rules summarized in [mistral-large-4.md](mistral-large-4.md#official-prompting-guidance)). Codestral specifics:

### 1. Use the FIM endpoint for autocomplete

- Send `prompt` (code before the cursor) and `suffix` (code after the cursor) to `/v1/fim/completions`; FIM uses bidirectional context, which produces completions that integrate with the surrounding code.
- Keep `max_tokens` tight for inline suggestions; FIM requests reusing a long prompt prefix benefit from prompt caching.

### 2. Use the chat endpoint for task-level coding

- For generation, explanation, code correction, or test generation, use chat completions with `codestral-latest` and a precise instruction: target language, framework, constraints, and expected output format.

### 3. Provide the relevant code context

- Include imports, function signatures, and surrounding code the change must fit; state what must stay unchanged.

### 4. Keep code output deterministic

- Use a low `temperature` within the recommended 0.0-0.7 range (e.g. 0.2) for focused, deterministic code; tune `temperature` or `top_p`, not both.

### 5. Use structured outputs and function calling when integrating

- Custom structured outputs (`response_format` with JSON schema) are the reliable option; describe tools with precise JSON schemas (name, description, parameters, required).

### 6. Use predicted outputs for repeated edits

- Predicted outputs speed up workflows where the expected output is largely known (e.g. applying a known diff pattern).

### 7. Route agentic work elsewhere

- For end-to-end coding tasks, use Vibe Code (CLI / VS Code / web) or the generalist models; do not prompt Codestral to plan multi-step changes across files.

---

## Prompt Template

```text
[SYSTEM]
You are a code assistant. Your task is to <code task>.

# Rules
- Target language/framework: <language>
- Keep changes minimal and consistent with the existing style.
- Do not change <parts that must stay unchanged>.

# Response Format
- Return only the code to insert/replace, no explanations, unless asked.

[USER]
# Context
<prefix code, relevant files, signatures>

# Task
<specific coding request>
```

For FIM (IDE autocomplete), no prompt template is needed - the endpoint takes `prompt`/`suffix` directly.

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Using Codestral for multi-file planning or agent loops | Route to `mistral-large-4` / `mistral-small-4` or Vibe Code |
| Chat-style long instructions for inline completion | Use `/v1/fim/completions` with prefix/suffix and small `max_tokens` |
| High temperature for code generation | Use low temperature (e.g. 0.2) within the 0.0-0.7 range |
| Expecting explanations by default | State explicitly whether you want code only or code + explanation |
| Using deprecated Devstral slugs for agentic coding | Migrate per the deprecation table (Medium 3.5 / Small 4 / Large 4) |
