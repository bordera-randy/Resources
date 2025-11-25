# AI Ethics & Safety Guide

Best practices for responsible, compliant, and secure AI use.

---

## 🔒 1. Data Privacy
Do NOT include:
- PII (names, email, addresses)  
- Credentials  
- Internal-only data  
- Sensitive corporate info  

Always sanitize data first.

---

## 🧩 2. Compliance Considerations
For regulated environments (HIPAA, FedRAMP, CJIS, 800-171):
- Remove identifiable data  
- Use abstractions or placeholders  
- Avoid proprietary details  
- Validate outputs manually  

---

## 🧪 3. Verification Before Use
Humans must verify:
- Technical accuracy  
- Compliance  
- Security implications  
- Business impact  

AI-generated work = **draft**, not an authoritative source.

---

## ⚖️ 4. Ethical Usage
AI should never:
- Replace human judgment  
- Be used to deceive  
- Be used to manipulate  
- Generate unsafe content  

---

## 📁 5. Safe Prompting
Safe structure:
- “Assume fictional data”  
- “Use sample placeholders”  
- “Generalize this for training purposes”  

