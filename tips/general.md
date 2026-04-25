# General Prompting Tips

Tips in this file are **model-agnostic** — they improve prompts regardless of which LLM you are targeting.

---

## Clarity & Structure

Sources: [1], [7]

Grounding:

- [1]: Recommends clear structure, explicit instructions, and delimiter-style segmentation for better adherence.
- [7]: Practitioner writeups consistently report better reliability with strongly structured prompts.
- Change applied: Treat XML tags as one practical delimiter pattern, not a mandatory format.

### Use XML-style tags for long prompts

Wrapping sections in `<context>`, `<task>`, and `<format>` tags makes the prompt easier to scan for both humans and models.

```
<context>
You are a customer support agent for Acme Corp.
</context>

<task>
Summarise the following complaint in one sentence.
</task>

<format>
Plain sentence, no bullet points.
</format>
```

### Lead with the task, not the background

Models pay more attention to content at the beginning and end of a prompt. Put the core instruction early.

> ❌ "Here is some background… (500 words) … now please summarise."
> ✅ "Summarise the following text in 3 bullet points.\n\n<text>…</text>"

### Use positive instructions, not just prohibitions

Tell the model what you *want* it to do, not only what to avoid.

> ❌ "Don't use technical jargon."
> ✅ "Use plain language suitable for a non-technical audience. Avoid acronyms."

---

## Few-Shot Examples

Sources: [2]

Grounding:

- [2]: Explicitly describes pattern learning through consistent examples and task-format alignment.
- [2]: Demonstrates that example diversity (including edge behavior) improves robustness.

### Match example format to desired output format

If you want JSON output, your few-shot examples should also be JSON.

### Use boundary examples

Include at least one easy case and one edge case in your few-shot set to teach the model the full range of expected behaviour.

### Keep examples consistent

All examples should follow the same template; inconsistent examples confuse the model more than no examples at all.

---

## Context Management

Sources: [1], [3], [7]

Grounding:

- [1]: Emphasizes prioritizing salient instructions and reducing ambiguity in long prompts.
- [3]: ReAct framing supports controlled multi-step behavior and explicit stopping conditions.
- [7]: Field usage reports support periodic summarization and context pruning for long threads.

### Summarise long conversations periodically

When a multi-turn conversation grows long, inject a "conversation summary so far" message to refresh the model's working context.

### Put the most important instructions last in long prompts

Recency bias means models weight recent content more heavily. Restate key constraints just before the final instruction.

### Remove irrelevant context

Every token of irrelevant context competes with the relevant parts. Trim aggressively.

### Define stop rules for multi-step tasks

State when the model should stop iterating, ask a clarifying question, or provide a fallback answer.

---

## Output Control

Sources: [1], [5]

Grounding:

- [1]: Supports explicit output contracts and constrained response formats.
- [5]: Production patterns favor deterministic output shapes and explicit quality checks.

### Use a "format header" at the top of the system message

```
Always respond with valid JSON matching this schema: { ... }
```

### Ask for confidence or uncertainty

```
After your answer, rate your confidence from 1–5 and explain any uncertainty.
```

### Request self-review

```
Review your answer for errors or omissions, then provide a final corrected version.
```

### Set explicit verbosity and length

For production answers, define target length and formatting density up front (for example: concise paragraphs, no extra sections).

---

## Cost & Latency

Sources: [5], [7]

Grounding:

- [5]: System design patterns stress minimizing unnecessary tokens and routing by task complexity.
- [7]: Practitioner notes reinforce concise prompts and staged model routing in real deployments.
- Change applied: Removed provider-specific caching claim and kept provider-agnostic guidance.

### Shorten prompts for high-volume applications

Every saved token compounds at scale. Use abbreviations in internal pipelines where readability for humans is not required.

### Reuse stable instruction blocks

Keep stable instruction blocks short and reusable so they can be shared across requests without repeated re-authoring.

### Use a smaller model for triage

Route simple requests to a smaller/cheaper model; escalate to a larger model only when complexity warrants it.

---

## Safety & Reliability

Sources: [4], [5], [7]

Grounding:

- [4]: Function-calling reliability improves with explicit tool constraints and failure handling.
- [5]: LLM product patterns emphasize validation gates, guardrails, and explicit fallback behavior.
- [7]: Practitioner reports highlight adversarial testing and iterative hardening as ongoing practice.

### Anchor the model's persona with explicit constraints

```
You are a financial assistant. You do not provide specific investment advice. If asked, redirect to a licensed advisor.
```

### Test adversarial inputs

Always test your prompt against inputs designed to make the model break its instructions (prompt injection, edge cases, off-topic requests).

### Use structured output validation

When expecting JSON or a specific schema, validate the response programmatically and retry with an error message on failure.

### Add retrieval budgets for grounded responses

Define when additional retrieval is justified and when current evidence is sufficient to answer.

---

Community source index: [knowledge/sources/openai.md](../knowledge/sources/openai.md#community-sources)
