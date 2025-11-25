# **Comprehensive AI Workflow Cheat Sheet**

A disciplined process for getting high-quality, predictable, and explainable output from any AI system.

---

# **0. Prep Stage — Set the Context**
Before starting the workflow, define:
- **Role** you want the AI to take  
  (e.g., Senior Cloud Architect, Editor, Threat Analyst, Product Strategist)
- **Quality Bar**  
  (“enterprise-grade,” “senior engineer level,” “NYT quality writing”)
- **Refusal Rules**  
  (“don’t guess,” “don’t invent data,” “don’t skip stages,” “clarify ambiguity”)

---

# **1. Clarity Stage — Define the Problem**
Before producing *any* output, force the AI to think.

### **Deliverables (no implementation allowed):**
- **Assumptions**  
  What must be assumed because the prompt lacks details?

- **Constraints**  
  Hard boundaries (tech stack, compliance, tone, format, region, environment, audience).

- **Missing Information**  
  What would meaningfully improve accuracy if the user provided it?

- **Top 3 Risks**  
  Where the approach could break:
  - misunderstood requirements  
  - ambiguous logic  
  - hidden dependencies  
  - unrealistic constraints  

> **Goal:** Surface ambiguity before it becomes a hallucination.

---

# **2. Architect Stage — Design the Solution**
Turn the clarified problem into a deliberate plan.

### **Deliverables (still no final output):**
- **High-Level Architecture**  
  Structure, components, data flows, logic blocks, narrative beats, etc.

- **Step-by-Step Plan**  
  Clear sequence of operations the AI will follow to execute.

- **Decision Tree With Tradeoffs**  
  If X → do A  
  If Y → do B  
  (ensures the AI can handle variability)

- **Contingency Plan**  
  What changes if:
  - requirements shift  
  - constraints tighten  
  - extra context becomes available  
  - a dependency fails  

> **Goal:** Lock in reasoning before creation.

---

# **3. Execute Stage — Build According to the Architecture**
Now — and only now — the AI produces the requested output.

### **Execution Rules:**
- Follow the architecture exactly  
- No improvisation  
- No skipping steps  
- If something is unclear → **ask instead of guessing**  
- Keep explanations separate from deliverables unless requested  

> **Goal:** Clean execution without hallucination or scope drift.

---

# **4. Audit Stage — Review Like a Senior Engineer**
Switch the model into *critic mode*.

### **Deliverables (no rewriting yet):**
- **Flaws**  
  Incorrect reasoning, invalid assumptions, technical errors.

- **Ambiguities**  
  Steps that are unclear or could be interpreted multiple ways.

- **Missing Edge Cases**  
  What scenarios weren’t covered?

- **Violations of Best Practices**  
  Coding, architecture, narrative, compliance, design, logic.

- **Specific Improvement Recommendations**  
  Not “fix wording” but “tighten characterization,” “improve identity-based controls,” etc.

> **Goal:** Produce a real peer review, not a polite one.

---

# **5. Improvement Stage — Apply Fixes & Finalize**
Now the AI applies the audit feedback.

### **Deliverables:**
- Revised, improved output  
- Corrections applied line-by-line or section-by-section  
- Optional: added commentary explaining what changed and why

> **Goal:** Produce a final version that meets enterprise or professional standards.

---

# **6. Optional Enhancement Tools**

## **A. Mode Switching**
You can instruct the AI to switch modes at any time:
- *Strategist mode*  
- *Engineer mode*  
- *Editor mode*  
- *Debugger mode*  
- *Interviewer mode*  
- *Adversarial reviewer mode*  

## **B. Depth Control**
Choose the level of detail:
- **High-level summary**  
- **Medium depth**  
- **Deep technical**  
- **Full production-ready**  

## **C. Format Control**
Common formats:
- Markdown  
- tables  
- bullet lists  
- diagrams  
- scripts  
- architectural diagrams  
- user stories  
- PRDs  
- Terraform-like structure  
- PowerShell-like structure  

## **D. Verification Prompts**
Useful checks:
- “List all assumptions you made.”  
- “List any ambiguous parts of the prompt.”  
- “Explain this solution back to me in your own words.”  
- “Show where your reasoning is weakest.”  
- “Run an adversarial test against your own output.”  

---

# **7. Red Flags to Avoid**
- Vague prompts (“write something good” → garbage)  
- Asking for the output before the architecture  
- Changing requirements mid-response  
- Not providing constraints  
- Letting the model guess missing details  
- Not reviewing or auditing the output  
- Skipping the clarity stage  

---

# **8. Quick Command Prompt**

Copy/paste this to force the workflow:

```md
You will follow this workflow:

1. **Clarity Stage** — assumptions, constraints, missing info, risks.
2. **Architect Stage** — structure, step-by-step plan, decision tree, contingencies.
3. **Execute Stage** — implement exactly to the plan; ask if unclear.
4. **Audit Stage** — critique the output (no rewriting).
5. **Improvement Stage** — apply fixes.

Do not skip stages. Do not guess. Ask when required.
