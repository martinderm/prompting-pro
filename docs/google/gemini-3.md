# Gemini 3 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `Gemini 3` family |
| **Provider** | Google |
| **Source** | [Gemini 3 guide](https://ai.google.dev/gemini-api/docs/gemini-3), [Prompting strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies) |
| **Last reviewed** | 2026-04 |

---

## Key Characteristics

- Reasoning-first model family for agentic, coding, and multimodal workloads.
- Main tracked variants include `gemini-3.1-pro-preview`, `gemini-3-flash-preview`, and `gemini-3.1-flash-lite-preview`.
- Uses `thinking_level` instead of OpenAI-style `reasoning.effort`; defaults are model-dependent and generally tuned for dynamic reasoning.
- Supports long context, built-in tools, structured outputs, multimodal inputs, and multimodal function responses.

---

## Family Positioning

- `Gemini 3.1 Pro` is the strongest fit for complex reasoning, deeper world knowledge, and demanding multimodal work.
- `Gemini 3 Flash` aims for Pro-level intelligence with lower latency and lower cost.
- `Gemini 3.1 Flash-Lite` is the cost-sensitive option for high-volume workloads.
- Native image-generation variants are covered separately in [nano-banana.md](nano-banana.md).

---

## Official Prompting Guidance

### 1. Keep prompts direct and concise

- Gemini 3 responds best to short, explicit instructions.
- Avoid carrying over overly elaborate prompt-engineering scaffolding from older models.
- State the task, constraints, and desired output clearly.

### 2. Use a stable prompt structure

- Separate role, constraints, context, and task with clear delimiters.
- Use either XML-style tags or Markdown headings consistently inside a single prompt.
- Define ambiguous parameters explicitly instead of leaving them implicit.

### 3. Place critical instructions where they matter most

- Put high-priority behavior constraints and output requirements at the start of the prompt or in system instructions.
- For long-context tasks, place the large context first and the precise question at the end.
- After long context blocks, anchor the request with a bridging phrase such as "Based on the information above...".

### 4. Let the model reason without over-prescribing the process

- Prefer clear goals over detailed chain-of-thought scripting.
- Use `thinking_level` as the main control for reasoning depth.
- For difficult tasks, a light instruction such as "think carefully before answering" is usually enough.

### 5. Keep Gemini 3 defaults unless you have eval evidence

- Leave `temperature` at the default `1.0` unless testing shows a real benefit.
- Lowering temperature can hurt reasoning quality or cause looping on Gemini 3.
- Do not send `thinking_level` and the legacy `thinking_budget` in the same request.

### 6. Use tools intentionally for grounding and calculation

- Enable Google Search when the answer depends on current or obscure facts.
- Enable Code Execution when arithmetic, counting, or programmatic inspection is required.
- Gemini 3 can combine built-in tools and custom function calls in the same workflow.

### 7. Preserve thought signatures in replay workflows

- Thought signatures maintain reasoning continuity across tool calls and multi-turn workflows.
- For function-calling workflows, missing required signatures can trigger strict validation errors.
- For image-editing workflows, returning thought signatures is required to preserve composition and avoid failures.

### 8. Use structured outputs and multimodal controls deliberately

- Prefer structured outputs for machine-consumed responses.
- Use `media_resolution` when image or video detail quality materially affects results.
- Treat text, images, audio, and video as equal prompt inputs and reference them explicitly when needed.

---

## Prompt Template

```text
<role>
You are Gemini 3, a specialized assistant for <domain>.
</role>

<constraints>
- <constraint 1>
- <constraint 2>
</constraints>

<context>
<relevant documents, code, or data>
</context>

<task>
<specific request>
</task>

<final_instruction>
Think carefully, stay grounded in the provided context, and return the requested format.
</final_instruction>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Over-engineered prompts from older model generations | Shorten the prompt and keep instructions direct |
| Lowering `temperature` for determinism without testing | Keep the default `1.0` unless evals justify changing it |
| Mixing `thinking_level` with `thinking_budget` | Use only one reasoning-control mechanism per request |
| Missing tool grounding for current facts | Enable Google Search when freshness matters |
| Dropping thought signatures in replay flows | Preserve and resend signatures exactly when required |
