
# 🤖 AI Workflow Guide

<p align="right"><sub>Last updated: February 1, 2026</sub></p>

**A practical, step-by-step framework for consistently getting high-quality, explainable results from AI.**

<p align="center">
  <a href="#clarity-stage">Clarity</a> •
  <a href="#architect-stage">Architect</a> •
  <a href="#execute-stage">Execute</a> •
  <a href="#audit-stage">Audit</a> •
  <a href="#improvement-stage">Improve</a> •
  <a href="#add-ons">Add-Ons</a> •
  <a href="#starter-prompt">Starter Prompt</a>
</p>

---

## Overview

Most people use AI reactively: ask a question, accept the answer, move on. This guide enforces discipline—forcing the model to think, clarify, and reason before acting. Use this process for any important task: writing, engineering, troubleshooting, strategy, architecture, creative work, or analysis.

---

# 1. Clarity Stage — Make the AI Think
<a id="clarity-stage"></a>

> **Before producing any output, force the AI to clarify:**

- **Assumptions:** What must be assumed to proceed?
- **Constraints:** Hard boundaries (tech stack, budget, time, rules, formatting, tone).
- **Missing Information:** What would improve accuracy if provided?
- **Top 3 Risks:** Where can this approach fail? What misunderstandings are likely? What breaks if requirements change?

<sub>Do **not** produce the final output yet.</sub>

> **Goal:** Surface ambiguity before it becomes a hallucination or error.

---

# 2. Architect Stage — Design Before Building
<a id="architect-stage"></a>

> **Turn the clarified problem into a deliberate plan:**

- **High-Level Architecture:** Structure, components, dependencies
- **Step-by-Step Plan:** Logical execution order
- **Decision Tree:** If X → do A; if Y → do B
- **Contingency Plan:** What changes if requirements shift?

<sub>Do **not** implement anything yet.</sub>

> **Goal:** Lock in reasoning before creation.

---

# 3. Execute Stage — Build Only What Was Designed
<a id="execute-stage"></a>

> **Now — and only now — implement the solution exactly as designed.**

- Follow the architecture precisely
- No improvisation or skipping steps
- If something is unclear: **pause and ask for clarification**

> **Goal:** Clean execution without hallucination or scope drift.

---

# 4. Audit Stage — Review Like a Senior Engineer
<a id="audit-stage"></a>

> **Switch to audit mode. Review the output as if doing a pull request:**

- Identify flaws or incorrect logic
- Call out ambiguities
- Find missing edge cases
- Flag best practice violations
- Recommend specific improvements

<sub>Do **not** rewrite the solution yet.</sub>

> **Goal:** Separate creation from critique to catch mistakes.

---

# 5. Improvement Stage — Apply Fixes
<a id="improvement-stage"></a>

> **Apply the audit feedback. Produce the improved, final version.**

> **Goal:** Intentional refinement, not random rewriting.

---

# When to Use This Framework

Use this process when:
- Accuracy matters
- The task is complex
- You need explainable reasoning
- You want consistency across iterations
- You’re delegating work to AI like a team member

Skip only when speed matters more than precision (quick chats, brainstorming, rewriting short text).

---

# Add-Ons: Elevate Your Results
<a id="add-ons"></a>

**Enhance your workflow with these options:**

### 🔍 Role Mode
Define the AI’s perspective: *senior cloud architect*, *editor*, *investigator*, *policy analyst*, *attack-surface reviewer*, etc.

### 📏 Quality Bar
Set the standard: “Enterprise-ready,” “Senior engineer level,” “NYT editorial quality,” “Clear enough for a junior to implement,” etc.

### 🛑 Refusal Rules
Tell the model what **not** to do:
- Don’t hallucinate missing data
- Don’t assume configurations
- Don’t skip the clarity stage
- Don’t produce code without validation

---


# Copy-Paste Starter Prompt
<a id="starter-prompt"></a>

```md
You will follow this workflow:

1. **Clarity Stage** — assumptions, constraints, missing info, risks.
2. **Architect Stage** — structure, step-by-step plan, decision tree, contingencies.
3. **Execute Stage** — implement exactly to the plan; ask if unclear.
4. **Audit Stage** — critique the output (no rewriting).
5. **Improvement Stage** — apply fixes.

Do not skip stages. Do not guess. Ask when required.
```

---

<p align="right"><a href="../README.md">Back to Student Resources</a></p>
