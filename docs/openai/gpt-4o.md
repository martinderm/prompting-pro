# GPT-4o — Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model** | `gpt-4o` (and `gpt-4o-mini`) |
| **Provider** | OpenAI |
| **Source** | [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) |
| **Last reviewed** | 2025-04 |

---

## Key Characteristics

- **Multimodal**: accepts text, images, and audio; returns text (and optionally audio).
- **Context window**: 128 000 tokens (gpt-4o), 128 000 tokens (gpt-4o-mini).
- **Instruction following**: highly capable; follows complex, multi-step system prompts reliably.
- **Default behaviour**: responds immediately — no internal chain-of-thought pause (use explicit CoT instructions when needed).

---

## Official Strategies

The six strategies below are taken directly from OpenAI's Prompt Engineering guide.

### 1. Write clear instructions

- **Be explicit**: if you want a short reply, say "Reply in 2–3 sentences." If you want code without an explanation, say so.
- **Adopt a persona**: use the system message to set tone and role (e.g. "You are a senior Python engineer who values simplicity.").
- **Use delimiters** (triple backticks, XML tags, `###`) to separate distinct sections of the prompt.
- **Specify output format**: JSON, Markdown table, numbered list — be precise.
- **Provide examples**: few-shot examples inside the prompt are highly effective for complex or unusual output formats.

### 2. Provide reference text

- Include background documents, knowledge-base snippets, or code in the prompt when the answer must be grounded in specific information.
- Instruct the model to "answer using only the provided text" to reduce hallucinations.
- Ask the model to cite the source passage when it draws on reference material.

### 3. Split complex tasks into simpler subtasks

- Decompose a long workflow into a pipeline of shorter prompts; pass outputs forward as inputs.
- Use **intent classification** in a first step to route the request before constructing a full response.
- For long conversations, periodically summarise earlier context and inject the summary to stay within the window.

### 4. Give the model time to "think"

- Ask the model to reason step-by-step before giving a final answer: "Think through this carefully before responding."
- Instruct it to write out a scratchpad or plan first, then produce the answer.
- For classification tasks, ask the model to list supporting evidence before declaring a label.

### 5. Use external tools

- Use **function calling** (tool use) to delegate retrieval, calculation, or action to external systems — do not ask the model to hallucinate facts it cannot know.
- Combine prompting with retrieval-augmented generation (RAG) for knowledge-intensive tasks.

### 6. Test changes systematically

- Evaluate prompt changes against a representative set of examples; do not rely on a single test case.
- Use a consistent scoring rubric (automated or human) to measure whether a prompt change is actually an improvement.

---

## Prompt Template (text-only)

```
[SYSTEM]
You are <persona>. <Behavioural constraints>. <Output format instructions>.

[USER]
Context:
"""
<reference text or data>
"""

Task:
<Clear, specific instruction>

Requirements:
- <Requirement 1>
- <Requirement 2>
```

## Prompt Template (vision / multimodal)

```
[SYSTEM]
You are <persona>.

[USER]
<Text instruction about the image>

[IMAGE]
<base64 or URL>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Vague instructions ("make it better") | Specify the exact dimension to improve (clarity, brevity, tone …) |
| Omitting output format | Always state the desired format explicitly |
| Over-long system prompts | Keep system prompts focused; move reference material to the user turn |
| Asking for facts the model cannot know | Use function calling + retrieval instead |
