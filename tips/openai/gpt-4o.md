# GPT-4o — Unofficial Tips

Tips specific to `gpt-4o` and `gpt-4o-mini`. These are community-sourced and may not apply equally to all versions.

---

## System Message Design

### Use a short, punchy system prompt + rich user turn
GPT-4o tends to perform better when the system message establishes persona and hard constraints (≤ 200 tokens), and the user message carries all task-specific context.  
Longer system prompts can dilute instruction-following fidelity on complex tasks.

### Separate "who you are" from "how to respond"
```
[SYSTEM — persona]
You are a senior software engineer who values clean, idiomatic code.

[SYSTEM — format rules]
Always return code in fenced Markdown blocks. Include a brief comment on each non-obvious line.
```

---

## Multimodal Tips

### Describe what you want from the image explicitly
GPT-4o reads images well but responds to what you ask. If you want data extracted, say "extract all visible text and numbers". If you want interpretation, say "describe what this chart shows".

### Combine text and image context
Grounding the image query in text context (e.g. "This is a screenshot from our CI dashboard — explain the failure highlighted in red") produces more relevant answers than an image alone.

### Resize large images before sending
Images are internally re-encoded; very large images consume more tokens. Resize to ≤ 2048 pixels on the long side for most tasks.

---

## Structured Output

### Use `response_format: json_schema` with a strict schema
GPT-4o's native JSON mode with `strict: true` almost never produces invalid JSON. Prefer this over asking for JSON in the prompt.

```json
{
  "type": "json_schema",
  "json_schema": {
    "name": "result",
    "strict": true,
    "schema": { ... }
  }
}
```

### Combine function calling with a fallback
If a function call fails validation, send the error back in the next user turn:  
"Your previous JSON was invalid: `<error>`. Please correct and try again."  
GPT-4o self-corrects reliably on the second attempt.

---

## Reasoning & Accuracy

### Ask for a plan before the answer on complex tasks
Even though GPT-4o does not have hidden chain-of-thought, asking it to outline a plan first improves answer accuracy on multi-step problems.

```
First, outline the steps you will follow. Then execute each step.
```

### Use "best of N" for high-stakes generation
Generate 3 candidate answers (`n=3` in the API) and then ask the model to select the best one with justification. Useful for creative tasks or when correctness is hard to verify automatically.

### Temperature guidance
| Use-case | Recommended `temperature` |
|----------|--------------------------|
| Factual Q&A, extraction | 0 – 0.2 |
| Summarisation | 0.2 – 0.5 |
| Creative writing | 0.7 – 1.0 |
| Brainstorming / ideation | 1.0 – 1.2 |

---

## Cost Optimisation

### Use `gpt-4o-mini` for classification and triage
`gpt-4o-mini` is significantly cheaper and fast enough for routing, classification, and simple extraction tasks.

### Batch non-urgent requests
The Batch API offers ~50 % cost reduction for tasks that do not need a real-time response.

---

## Known Quirks

- **Markdown rendering**: GPT-4o loves Markdown by default. If your downstream system renders plain text, add "Do not use Markdown formatting" to the system message.
- **Verbosity**: without an explicit length constraint, GPT-4o often over-explains. Add "Be concise" or a word/sentence limit.
- **Sycophancy**: the model may agree with incorrect premises in the user prompt. Counter with: "Do not assume my premises are correct; challenge them if needed."
