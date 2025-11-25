# **The Best Way to Use AI**

*A practical framework for consistently getting high-quality work from AI systems*

## **Overview**

Most people use AI reactively: they ask a question, accept the answer, and stumble forward.
This framework forces discipline. You slow the model down, you force it to think, and you get results that are accurate, explainable, and aligned with what you really need.

Use this process anytime the task matters—writing, engineering, troubleshooting, strategy, architecture, creative work, or analysis.

---

# **1. Clarity Stage — Make the AI Think Before It Acts**

```md
Before producing anything, list:

1. Assumptions  
   - What must the model assume to proceed?

2. Constraints  
   - Hard boundaries (tech stack, budget, time, rules, formatting, tone).

3. Missing Information  
   - What would meaningfully improve accuracy if provided?

4. Top 3 Risks  
   - Where this approach can fail.
   - What misunderstandings are most likely.
   - What will break if requirements change.

Do NOT produce the final output yet.
```

**Why this matters:**
You’re forcing the AI to surface hidden uncertainty. That prevents hallucination, scope drift, and bad guesses.

---

# **2. Architect Stage — Design Before Building**

```md
Based on the Clarity Stage, produce:

- A high-level architecture  
  (overall structure, components, dependencies)

- A step-by-step approach  
  (the execution plan in logical order)

- A decision tree showing tradeoffs  
  (if X: do A; if Y: do B)

- A contingency plan  
  (what changes if requirements shift)
  
Do not implement anything yet.
```

**Why this matters:**
You’re forcing the model to commit to reasoning, not output.
This is where it proves it actually understands what it’s about to build.

---

# **3. Execute Stage — Build Only What Was Designed**

```md
Now implement the solution exactly according to the architecture.

If something is ambiguous:
- Pause
- Ask the user for clarification
- Do not guess
```

**Why this matters:**
Skipping clarification is how you get broken code, mediocre writing, or incorrect analysis.
This step ensures discipline and prevents silent errors.

---

# **4. Audit Stage — Treat the Output Like a PR Review**

```md
Switch to audit mode.

Evaluate the solution like a senior engineer reviewing a pull request:

- Identify flaws or incorrect logic
- Call out ambiguities
- Find missing edge cases
- Flag anything that violates best practices
- Recommend specific improvements

Do **not** rewrite the solution yet.
```

**Why this matters:**
Auditing is where quality happens.
You separate creation mode from critique mode so you can actually catch mistakes.

---

# **5. Improvement Stage — Apply Fixes**

```md
Apply the recommended improvements from the audit step.
Produce the corrected, final version.
```

**Why this matters:**
This is the refinement pass. You’re iterating intentionally—not randomly rewriting.

---

# **When to Use This Framework**

Use this process whenever:

* Accuracy matters
* You’re building something complex
* You need explainable reasoning
* You want consistency across iterations
* You’re delegating work to AI like a team member

Avoid it only when speed matters more than precision (quick chats, brainstorming, rewriting short text).

---

# **Optional Add-Ons**

**To elevate results even more, add these:**

### **🔍 “Role Mode”**

Define the perspective the AI should take:
*senior cloud architect*, *editor*, *investigator*, *policy analyst*, *attack-surface reviewer*, etc.

### **📏 “Quality Bar”**

Tell the model the standard it must meet:
“Enterprise-ready,”
“Senior engineer level,”
“New York Times editorial quality,”
“Clear enough for a junior to implement,”
etc.

### **🛑 “Refusal Rules”**

Tell the model what NOT to do:

* Don’t hallucinate missing data
* Don’t assume configurations
* Don’t skip the clarity stage
* Don’t produce code without validation

---

# **Copy-Paste Starter Prompt**

```md
You will follow this workflow:

1. **Clarity Stage** – list assumptions, constraints, missing info, and top 3 risks.
2. **Architect Stage** – design the structure, steps, decision tree, and contingencies.
3. **Execute Stage** – implement exactly according to the architecture.
4. **Audit Stage** – critique the implementation.
5. **Improvement Stage** – apply improvements.

Do not skip stages.
Do not guess.
Seek clarification when needed.
```
