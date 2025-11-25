# AI Prompt Patterns

These patterns help guide the AI into structured, predictable reasoning.

---

## 🔍 Role Prompting
“Act as a **{{role}}** with 10+ years of experience.  
Use best practices and industry standards.”

Examples:
- Senior cloud architect  
- Security engineer  
- Editor  
- Product manager  
- Forensics analyst  

---

## 🧱 Multi-Stage Prompting
Break complex work into stages:

1. Clarify  
2. Architect  
3. Execute  
4. Audit  
5. Improve  

This avoids wrong assumptions and hallucinations.

---

## 🔄 Reflection Prompting
Ask the AI to critique itself:

- “What is the weakest part of your answer?”  
- “List ambiguous areas.”  
- “List assumptions you made.”  
- “Challenge your own solution.”

---

## ⚖️ Tradeoff Prompting
Ask for competing options:

“Give 3 approaches, compare pros/cons, and recommend one based on constraints.”

---

## 🧪 Adversarial Prompting
Stress test logic:

“Assume this solution is wrong.  
Explain how you would prove it.”

---

## 🧵 Chain-of-Thought (Condensed)
“Show your reasoning **briefly** in bullet points before answering.”

---

## 🧼 Constraint Prompting
“Tight constraints produce better output.”

Example constraints:
- Format  
- Tone  
- Length  
- Audience  
- Region  
- Compliance frameworks  

---

## 🧭 Decision Trees
“Create a decision tree covering all major branches of this problem.”

Great for architecture, troubleshooting, writing choices, logic design.

