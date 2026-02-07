
# 🤖 AI Ethics & Safety Guide

<p align="right"><sub>Last updated: January 31, 2026</sub></p>

**Best practices for responsible, compliant, and secure AI use in cloud, engineering, and business.**

<p align="center">
	<a href="#data-privacy">Data Privacy</a> •
	<a href="#compliance">Compliance</a> •
	<a href="#verification">Verification</a> •
	<a href="#ethical-usage">Ethical Usage</a> •
	<a href="#safe-prompting">Safe Prompting</a>
</p>

---

## 🔒 Data Privacy
<a id="data-privacy"></a>
**Never include:**
- PII (names, emails, addresses)
- Credentials or secrets
- Internal-only or confidential data
- Sensitive corporate or customer info

**Always sanitize data before using AI.**

---

## 🧩 Compliance Considerations
<a id="compliance"></a>
For regulated environments (HIPAA, FedRAMP, CJIS, 800-171, GDPR):
- Remove or mask identifiable data
- Use abstractions or placeholders
- Avoid proprietary or export-controlled details
- Validate outputs for compliance before use

---

## 🧪 Verification Before Use
<a id="verification"></a>
**Human review is required for:**
- Technical accuracy
- Compliance and legal risk
- Security implications
- Business or reputational impact

> AI-generated work = **draft**. Never treat as authoritative without review.

---

## ⚖️ Ethical Usage
<a id="ethical-usage"></a>
AI must **never** be used to:
- Replace critical human judgment
- Deceive, manipulate, or mislead
- Generate unsafe, discriminatory, or harmful content
- Violate user consent or privacy

**If in doubt, escalate to a human reviewer.**

---

## 📁 Safe Prompting
<a id="safe-prompting"></a>
**Prompt structure for safety:**
- “Assume fictional/sample data”
- “Use placeholders, not real customer info”
- “Generalize for training/demo purposes”

**Example:**
> "Generate a sample Azure policy using only fictional resource names and no real user data."

---

<p align="right"><a href="#top">Back to Top</a></p>

