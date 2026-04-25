# OpenAI Codex Overlay - Unofficial Tips

Shared coding-task overlay for OpenAI coding models (`gpt-5.5`, `gpt-5.4`, `gpt-5.4-mini`, `gpt-5.4-nano`, `gpt-5.3-codex`).

Apply this file in addition to the model-specific tip file when the task is implementation-heavy, verification-heavy, or agentic.

---

## Operator Communication and Done Criteria

Sources: [8]

Grounding:

- [8]: Recommends a strict separation between technical execution and plain-language reporting in final user-facing updates.
- [8]: Recommends defining completion criteria up front and verifying outputs before reporting completion.

### Add a plain-language reporting contract

Instruct the model to keep internal work technical, but present final updates in clear language for non-code reviewers.

### Define "done" before implementation

Require a short checklist before coding starts (for example: target behavior, passing checks, and no regressions in touched flows).

### Enforce verify-before-report

Ask the model to run available checks and only report completion after validation; if blocked, report the blocker and next-best validation path.

### Prompt snippet

```text
Before you start, define completion criteria as a checklist.
Before reporting back, verify your work with available checks.
Final response style: plain, clear English with outcomes and evidence; avoid implementation-heavy jargon.
If verification is blocked, state exactly why and what you validated instead.
```

---

Community source index: [knowledge/sources/openai.md](../../knowledge/sources/openai.md#community-sources)
