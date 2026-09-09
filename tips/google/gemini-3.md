# Gemini 3 Family (incl. Gemini 3.8 Flash) - Practical & Community Tips

Curated prompting patterns and operational tips for the `Gemini 3` family, with special focus on `gemini-3.8-flash`, interactive chat applications (Gemini Web, Gems), and code execution.

---

## Mental Model for Gemini 3.8 Flash

Sources: Google DeepMind Prompting Guidance, Community Evals [2026-09]

1. **Critical Rules First:** Always place the most critical behavioral guardrails and negative constraints at the very top of the prompt or system instructions. Gemini 3.8 Flash anchors strongly on top-level directives.
2. **Dynamic Thinking Levels:** Gemini 3.8 Flash utilizes native reasoning depth:
   - `thinking_level: low` / `medium`: Fast conversational chat, summarization, extraction.
   - `thinking_level: high`: Complex coding, multi-step debugging, mathematical reasoning, logic puzzles.
   - Avoid manual step-by-step chain-of-thought micro-management ("first think X, then Y, then Z in tags"). Let the model's internal reasoning engine operate freely.
3. **Structured Context Layout:** Format context with clear Markdown headings or XML delimiters (`<context>`, `<task>`). For long documents, place the document text first, followed by the specific question anchored with a bridging phrase (*"Based on the provided information..."*).

---

## Sensible Default Instructions for Chat Apps & Custom Gems

Adapted from [LLM-Sensible-Default-Instructions](https://github.com/martinderm/LLM-Sensible-Default-Instructions):

### 1. Epistemic Stance & Anti-Sycophancy
- **Truth over agreement:** Instruct the model to prioritize factual accuracy over polite validation. Correct flawed user premises clearly and neutrally.
- **Constructive skepticism:** For consequential or disputed assertions, surface key assumptions, present at least one credible counterpoint, and test the reasoning for gaps without being reflexively contrarian.
- **Explicit confidence closing:** On ambiguous, rapidly changing, or weakly evidenced topics, mandate a closing line:
  - `Confidence: High / Medium / Low` + 1-sentence rationale.

### 2. UI-Specific Form Factor (Gemini vs. ChatGPT)
- **ChatGPT:** Constrained by ~1,500 characters per custom instruction box -> use compressed, dense paragraphs (e.g. `condensed-instructions.md`).
- **Gemini (Advanced / Custom Gems):** Supports up to 10,000 characters. Take advantage of this by using cleanly structured Markdown headings, bullet points, and explicit sections (`full-instructions.md`). Flash parses structured lists with higher fidelity than monolithic text blocks.

### 3. Proactive Search Grounding Trigger
To prevent hallucinations on current events or verifiable empirical facts, include an explicit tool-trigger constraint:
> *"When an answer depends on up-to-date, external, or verifiable information, use Google Search to verify facts, or plainly state the uncertainty."*

---

## Coding & Technical Tasks Pattern

When configuring Gemini 3.8 Flash for coding or technical pair-programming:

1. **Dual-Layer Communication:**
   - **Explanations:** Plain, clear language suitable for a smart reader.
   - **Internal execution:** Fully technical, rigorous, and uncompromised.
2. **Finishing Criteria (Definition of Done):**
   - Require the model to establish internal completion criteria before declaring a task finished.
3. **Mandatory Verification Step & Tri-State Reporting:**
   Google specifically recommends requiring a verification step before final output. In the final response, enforce a tri-state status breakdown:
   - **Directly confirmed:** What was executed and verified to work.
   - **Partially checked:** What was inspected without full end-to-end execution.
   - **Unverified:** What could not be checked, accompanied by specific blocker reasons.

---

## Chat Ergonomics vs. Agent-Framework Overhead

When configuring instructions for everyday chat use (Gemini Web, Gems, mobile app), keep the instructions **chat-native**:
- Avoid injecting multi-agent harness overhead (e.g. Dual Evidence matrices, file receipts, stage contracts) into standard chat windows.
- In a pure conversational UI without filesystem tools, formal audit protocols degrade user ergonomics and clutter conversation context.
- Keep the prompt focused on epistemic discipline, tone, and reasoning quality.
