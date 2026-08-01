# GPT-5.6 - Official Prompt Guidance

| Field | Value |
|-------|-------|
| **Model family** | `gpt-5.6-sol`, `gpt-5.6-terra`, `gpt-5.6-luna` |
| **Alias** | `gpt-5.6` routes to `gpt-5.6-sol` |
| **Provider** | OpenAI |
| **Source** | [GPT-5.6 model guidance](https://developers.openai.com/api/docs/guides/latest-model?model=gpt-5.6) |
| **Last reviewed** | 2026-08-01 |

---

## Key Characteristics

- Use `gpt-5.6-sol` for flagship capability, `gpt-5.6-terra` for a quality/cost balance, and `gpt-5.6-luna` for efficient high-volume work.
- Expect concise default responses, strong intent inference, improved token efficiency, and stronger frontend design judgment.
- Choose `reasoning.effort` deliberately from `none`, `low`, `medium`, `high`, `xhigh`, or `max`; use `medium` as a balanced starting point and reserve `max` for measured quality-first gains.
- Treat standard mode and `reasoning.mode: "pro"` as separate evaluation targets. Pro mode increases model work, latency, and token use and does not require a separate model slug.

---

## Official Prompting Guidance

### 1. Favor lean prompts

- State each instruction once and remove repeated guidance.
- Expose only task-relevant tools and keep tool descriptions concise and precise.
- Retain examples or style rules only when they encode a product requirement or fix a measured gap.
- Simplify one instruction group at a time and rerun representative evaluations after each change.

### 2. Define autonomy and approval boundaries once

- Distinguish read-only requests such as answering, reviewing, diagnosing, or planning from requests that authorize implementation.
- Permit safe, in-scope local actions explicitly so the model can complete work without unnecessary pauses.
- Require confirmation for external writes, destructive actions, purchases, and material scope expansion.
- Avoid repeating approval rules in multiple sections because repetition can trigger unnecessary confirmation requests.

### 3. Specify outcomes, constraints, and ambiguity handling

- State the goal, relevant context, hard constraints, required evidence, success criteria, and output format.
- Let the model infer routine execution details instead of prescribing every step.
- Tell the model which important ambiguities require a question and where safe assumptions are acceptable.

### 4. Control response length and tone precisely

- Reassess broad brevity instructions when migrating because GPT-5.6 is more concise by default than GPT-5.5.
- Set `text.verbosity` to `low`, `medium`, or `high` for the default detail level, then specify task-specific requirements in the prompt.
- For short answers, name the facts, evidence, caveats, decisions, and next actions that must remain.
- Describe concrete writing choices instead of relying only on broad tone labels such as "friendly" or "empathetic".

### 5. Use pro mode selectively

- Enable pro mode in the API, not by asking the model to "think harder" in the prompt.
- Keep the same outcome-focused prompt in standard and pro modes.
- Compare task success, completeness, evidence, tokens, latency, and cost on representative tasks.
- Prefer standard mode for routine, latency-sensitive, or high-volume work unless evaluations show a meaningful pro-mode gain.

### 6. Route Programmatic Tool Calling explicitly

- Use Programmatic Tool Calling for bounded filtering, joining, ranking, deduplication, aggregation, or validation over tool results.
- Prefer direct tool calls when one call is enough, intermediate results are small, each result changes the next decision, approval is required, or native citations/artifacts must be preserved.
- Name the bounded stage, eligible tools, output schema, evidence requirements, concurrency, retries, stop condition, and direct-call handoff.
- Validate both the structured `program_output` and the final assistant message.

---

## Prompt Template

```text
[DEVELOPER]
Goal: <user-visible outcome>

Context:
<only relevant domain and task context>

Constraints:
- <hard constraint>
- <approval or scope boundary>

Success criteria:
- <observable completion condition>
- <required evidence or validation>

Output:
- <format, length, and required content>

Ambiguity handling:
- Ask only when <material blocking condition>.
- Otherwise make <allowed safe assumptions> explicit.

[USER]
<task>
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Repeating instructions across prompt sections | State each rule once and evaluate after removing duplication |
| Keeping generic brevity rules from older prompts | Test without them; use `text.verbosity` and explicit content priorities |
| Asking the prompt to activate pro mode | Configure `reasoning.mode: "pro"` in the API request |
| Using Programmatic Tool Calling merely because calls are parallel | Route by bounded processing shape and define a direct-call handoff |
| Defaulting every difficult task to maximum effort | Compare effort levels and modes on representative evaluations |
