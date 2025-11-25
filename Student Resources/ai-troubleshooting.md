# AI Troubleshooting Guide

How to fix bad AI answers, hallucinations, and unclear outputs.

---

## 🚨 Common Symptoms & Fixes

### **1. AI Guessing / Hallucinating**
**Fix:**  
Add constraints:  
“Do not guess.  
If something is missing, ask.”

---

### **2. Vague / Low-Quality Output**
**Fix:**  
Specify:
- Role  
- Audience  
- Purpose  
- Format  
- Depth level  

---

### **3. Too Wordy**
**Fix:**  
“Rewrite concisely with no filler.”

---

### **4. Missing Critical Details**
**Fix:**  
Ask:  
“List assumptions and missing information.”  
Then provide missing data.

---

### **5. Wrong Technical Answer**
**Fix:**  
- Provide error messages  
- Provide logs  
- Provide environment context  
- Ask for step-by-step troubleshooting

---

## 🧪 Debugging a Bad Answer

1. Ask:  
   “What assumptions did you make here?”

2. Ask:  
   “Rewrite with correct assumptions only.”

3. Add constraints  
   (version numbers, architecture, environment).

4. Run an **audit pass**:  
   “Review this answer for errors, ambiguities, and missed edge cases.”

5. Apply improvements.

---

## 🔐 Preventing Future Problems
- Use multi-stage prompting  
- Require clarifying questions  
- Provide constraints upfront  
- Avoid asking multiple things in one message  

