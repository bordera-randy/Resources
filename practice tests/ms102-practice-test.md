---
title: "MS-102 Practice Test - 50 Questions"
description: "Comprehensive 50-question practice test for MS-102 Microsoft 365 Administrator certification exam with concise answer explanations."
tags: ["MS-102", "Practice Test", "Microsoft 365", "Admin", "Exam Prep"]
updated: "2026-02-06"
---

# 🧪 MS-102 Practice Test - 50 Questions

<p align="right"><a href="../README.md">Back to Student Resources</a></p>

---

## ℹ️ Test Information

- **Exam Code**: MS-102
- **Questions**: 50
- **Time**: 120 minutes (recommended ~2.4 min per question)
- **Passing Score**: 70% (35/50 questions)
- **Format**: Multiple choice and scenario-based

**Instructions**: Answer all questions. Focus on real-world admin tasks. Try to complete within 120 minutes.

---

## 📝 Questions

### Question 1
**Where do you assign Microsoft 365 licenses to users?**

A) Exchange admin center  
B) Teams admin center  
C) Microsoft 365 admin center  
D) SharePoint admin center  

<details>
<summary>Answer</summary>
<b>C) Microsoft 365 admin center</b>

Licenses are assigned to users in the Microsoft 365 admin center (or via Azure AD / PowerShell). Service-specific admin centers don’t assign licenses.
</details>

---

### Question 2
**Which record must be added to verify a custom domain in Microsoft 365?**

A) MX record  
B) TXT record  
C) SRV record  
D) A record  

<details>
<summary>Answer</summary>
<b>B) TXT record</b>

Domain verification uses a TXT record in DNS to prove ownership before services are configured.
</details>

---

### Question 3
**A user cannot access Teams. Their license is assigned. What’s the most likely cause?**

A) Exchange Online license missing  
B) Teams service disabled in the license  
C) SharePoint license missing  
D) OneDrive license missing  

<details>
<summary>Answer</summary>
<b>B) Teams service disabled in the license</b>

Each license has service toggles. If Teams is disabled within the license, the user cannot access Teams.
</details>

---

### Question 4
**Which admin center is used to manage mailbox policies and mail flow rules?**

A) Microsoft 365 admin center  
B) Exchange admin center  
C) SharePoint admin center  
D) Teams admin center  

<details>
<summary>Answer</summary>
<b>B) Exchange admin center</b>

Exchange admin center manages mailboxes, mail flow, and transport rules.
</details>

---

### Question 5
**You need to create a distribution list for a department. Where should you do this?**

A) Teams admin center  
B) Exchange admin center  
C) SharePoint admin center  
D) Security & Compliance center  

<details>
<summary>Answer</summary>
<b>B) Exchange admin center</b>

Distribution lists are created and managed in Exchange admin center.
</details>

---

### Question 6
**Which feature allows multiple users to own and manage a shared mailbox?**

A) Mail flow rule  
B) Shared mailbox permissions  
C) Distribution group settings  
D) Transport rules  

<details>
<summary>Answer</summary>
<b>B) Shared mailbox permissions</b>

Shared mailboxes use Full Access and Send As permissions to allow multiple owners.
</details>

---

### Question 7
**What is the primary purpose of Microsoft 365 Groups?**

A) Enforce MFA  
B) Provide a shared workspace across apps (Outlook, Teams, SharePoint)  
C) Replace security groups  
D) Control billing  

<details>
<summary>Answer</summary>
<b>B) Provide a shared workspace across apps</b>

Microsoft 365 Groups provide membership and shared resources across Teams, Outlook, SharePoint, and Planner.
</details>

---

### Question 8
**Which admin center controls Teams meeting policies?**

A) Teams admin center  
B) Exchange admin center  
C) SharePoint admin center  
D) Microsoft 365 admin center  

<details>
<summary>Answer</summary>
<b>A) Teams admin center</b>

Meeting policies are managed in the Teams admin center.
</details>

---

### Question 9
**How do you enable external sharing for SharePoint Online?**

A) Teams admin center  
B) SharePoint admin center  
C) Exchange admin center  
D) Microsoft 365 admin center only  

<details>
<summary>Answer</summary>
<b>B) SharePoint admin center</b>

External sharing settings for SharePoint and OneDrive are configured in the SharePoint admin center.
</details>

---

### Question 10
**Which policy controls how long emails are retained before deletion?**

A) DLP policy  
B) Retention policy  
C) Conditional access policy  
D) Audit policy  

<details>
<summary>Answer</summary>
<b>B) Retention policy</b>

Retention policies define how long content is kept or deleted for compliance.
</details>

---

### Question 11
**What does MFA protect against most effectively?**

A) Power outages  
B) Credential theft  
C) Storage limits  
D) Licensing errors  

<details>
<summary>Answer</summary>
<b>B) Credential theft</b>

MFA reduces risk from stolen passwords by requiring an additional authentication factor.
</details>

---

### Question 12
**A user leaves the company. What is the best practice for their mailbox?**

A) Delete it immediately  
B) Convert to shared mailbox and grant access if needed  
C) Export to PST only  
D) Leave it active indefinitely  

<details>
<summary>Answer</summary>
<b>B) Convert to shared mailbox and grant access if needed</b>

Shared mailboxes preserve data while saving a license (if under size limits).
</details>

---

### Question 13
**Which role is required to manage Exchange Online?**

A) Teams Administrator  
B) Global Administrator or Exchange Administrator  
C) SharePoint Administrator only  
D) User Administrator only  

<details>
<summary>Answer</summary>
<b>B) Global Administrator or Exchange Administrator</b>

Exchange management requires Exchange Admin or Global Admin roles.
</details>

---

### Question 14
**Which PowerShell module is commonly used to manage Microsoft 365 users?**

A) AzureAD or Microsoft Graph  
B) SharePointPnP only  
C) Teams only  
D) Windows PowerShell only  

<details>
<summary>Answer</summary>
<b>A) AzureAD or Microsoft Graph</b>

User management is typically handled via AzureAD or Microsoft Graph PowerShell modules.
</details>

---

### Question 15
**What is the purpose of Service Health in Microsoft 365 admin center?**

A) Monitor mailbox size  
B) View service incidents and advisories  
C) Set password policies  
D) Create Teams policies  

<details>
<summary>Answer</summary>
<b>B) View service incidents and advisories</b>

Service Health provides status of Microsoft 365 services and active incidents.
</details>

---

### Question 16
**Which feature prevents users from sharing files externally?**

A) DLP only  
B) SharePoint external sharing settings  
C) Exchange transport rules  
D) Teams meeting policies  

<details>
<summary>Answer</summary>
<b>B) SharePoint external sharing settings</b>

External sharing is controlled at the SharePoint/OneDrive tenant level.
</details>

---

### Question 17
**What is the primary difference between security groups and Microsoft 365 groups?**

A) Security groups are for permissions; Microsoft 365 groups include shared resources across apps  
B) They are identical  
C) Microsoft 365 groups cannot be used for permissions  
D) Security groups include Teams automatically  

<details>
<summary>Answer</summary>
<b>A) Security groups are for permissions; Microsoft 365 groups include shared resources across apps</b>

Security groups manage access, while Microsoft 365 groups provide collaborative resources like Teams and SharePoint.
</details>

---

### Question 18
**Which admin center manages OneDrive sharing settings?**

A) OneDrive admin center  
B) SharePoint admin center  
C) Microsoft 365 admin center  
D) Exchange admin center  

<details>
<summary>Answer</summary>
<b>B) SharePoint admin center</b>

OneDrive settings are managed within the SharePoint admin center.
</details>

---

### Question 19
**What is the recommended approach for bulk user creation?**

A) Create each user manually  
B) Use CSV import in Microsoft 365 admin center  
C) Ask users to self-register  
D) Use Teams only  

<details>
<summary>Answer</summary>
<b>B) Use CSV import in Microsoft 365 admin center</b>

Bulk user creation uses CSV import for efficiency and accuracy.
</details>

---

### Question 20
**Which policy controls guest access in Microsoft Teams?**

A) Exchange policy  
B) Teams org-wide settings  
C) SharePoint retention policy  
D) Azure AD password policy  

<details>
<summary>Answer</summary>
<b>B) Teams org-wide settings</b>

Guest access is enabled/disabled at the Teams org-wide level in Teams admin center.
</details>

---

### Question 21
**You need to prevent users from deleting a SharePoint site. Which feature should you use?**

A) Retention policy  
B) Site lock or permissions  
C) DLP policy  
D) Conditional access  

<details>
<summary>Answer</summary>
<b>B) Site lock or permissions</b>

Locking a site or restricting permissions prevents deletions.
</details>

---

### Question 22
**What is the default storage size for OneDrive in most Microsoft 365 plans?**

A) 5 GB  
B) 100 GB  
C) 1 TB  
D) Unlimited  

<details>
<summary>Answer</summary>
<b>C) 1 TB</b>

Most business plans include 1 TB of OneDrive storage per user.
</details>

---

### Question 23
**Which Microsoft 365 feature provides audit logs for user activities?**

A) Compliance Center audit logs  
B) Teams chat history  
C) Exchange rules  
D) SharePoint version history  

<details>
<summary>Answer</summary>
<b>A) Compliance Center audit logs</b>

Audit logs are accessed in the Microsoft Purview compliance portal.
</details>

---

### Question 24
**What is the purpose of a retention label?**

A) Encrypt files automatically  
B) Apply retention settings to specific items  
C) Create distribution groups  
D) Manage licensing  

<details>
<summary>Answer</summary>
<b>B) Apply retention settings to specific items</b>

Retention labels can be applied to items to enforce retention or deletion rules.
</details>

---

### Question 25
**Which setting controls whether users can create Microsoft 365 Groups?**

A) Teams policy  
B) Azure AD group creation settings  
C) Exchange mailbox policy  
D) SharePoint site policy  

<details>
<summary>Answer</summary>
<b>B) Azure AD group creation settings</b>

Group creation can be restricted in Azure AD to specific users/groups.
</details>

---

### Question 26
**Where do you configure organization-wide password policies?**

A) Exchange admin center  
B) Azure AD/Entra ID  
C) Teams admin center  
D) SharePoint admin center  

<details>
<summary>Answer</summary>
<b>B) Azure AD/Entra ID</b>

Password policies are enforced in Azure AD for Microsoft 365 tenants.
</details>

---

### Question 27
**Which feature helps prevent accidental data deletion?**

A) Retention policies  
B) MFA  
C) Conditional access  
D) Audit logs  

<details>
<summary>Answer</summary>
<b>A) Retention policies</b>

Retention policies can keep data even if a user tries to delete it.
</details>

---

### Question 28
**What is the best way to manage external sharing in OneDrive?**

A) Teams admin center  
B) SharePoint admin center  
C) Exchange admin center  
D) Security center  

<details>
<summary>Answer</summary>
<b>B) SharePoint admin center</b>

OneDrive external sharing settings are managed in the SharePoint admin center.
</details>

---

### Question 29
**Which policy determines how long Teams messages are retained?**

A) Exchange retention policy  
B) Teams retention policy in Compliance portal  
C) Teams meeting policy  
D) SharePoint retention policy only  

<details>
<summary>Answer</summary>
<b>B) Teams retention policy in Compliance portal</b>

Teams chats and channel messages retention is managed via Microsoft Purview retention policies.
</details>

---

### Question 30
**Which admin role can manage SharePoint Online?**

A) Teams Administrator  
B) SharePoint Administrator or Global Administrator  
C) Exchange Administrator only  
D) User Administrator only  

<details>
<summary>Answer</summary>
<b>B) SharePoint Administrator or Global Administrator</b>

SharePoint administration requires SharePoint Admin or Global Admin roles.
</details>

---

### Question 31
**What is the primary use of Microsoft Purview compliance portal?**

A) Managing Teams meetings  
B) Managing compliance, retention, and auditing  
C) Managing licensing only  
D) Managing OneDrive sync  

<details>
<summary>Answer</summary>
<b>B) Managing compliance, retention, and auditing</b>

Purview is the central portal for compliance, data governance, DLP, and auditing.
</details>

---

### Question 32
**Which tool helps monitor user adoption and usage statistics?**

A) Service Health  
B) Microsoft 365 Usage Reports  
C) Exchange Admin Center  
D) PowerShell only  

<details>
<summary>Answer</summary>
<b>B) Microsoft 365 Usage Reports</b>

Usage reports provide adoption and activity insights for services.
</details>

---

### Question 33
**What should you configure to allow users to recover deleted files in OneDrive?**

A) MFA  
B) OneDrive recycle bin and retention settings  
C) Teams policies  
D) Exchange transport rules  

<details>
<summary>Answer</summary>
<b>B) OneDrive recycle bin and retention settings</b>

The recycle bin and retention controls allow user recovery of deleted files.
</details>

---

### Question 34
**Which setting controls whether users can create Teams?**

A) Teams creation policy (Azure AD group creation settings)  
B) Exchange admin center  
C) SharePoint admin center  
D) Compliance portal  

<details>
<summary>Answer</summary>
<b>A) Teams creation policy (Azure AD group creation settings)</b>

Teams creation is controlled via Azure AD group creation settings since Teams are backed by M365 Groups.
</details>

---

### Question 35
**What is the best practice for admin access security?**

A) Share admin passwords  
B) Use least privilege and MFA for admin accounts  
C) Disable MFA to reduce friction  
D) Use personal accounts for admin tasks  

<details>
<summary>Answer</summary>
<b>B) Use least privilege and MFA for admin accounts</b>

Least privilege and MFA for admins reduces attack surface and prevents unauthorized changes.
</details>

---

### Question 36
**Which policy controls external users in SharePoint sites?**

A) Teams org settings  
B) SharePoint external sharing policy  
C) Exchange admin policy  
D) DLP policy  

<details>
<summary>Answer</summary>
<b>B) SharePoint external sharing policy</b>

External sharing for SharePoint is controlled in the SharePoint admin center.
</details>

---

### Question 37
**Which feature helps prevent accidental data exposure via email?**

A) DLP  
B) Microsoft Forms  
C) Bookings  
D) Teams announcements  

<details>
<summary>Answer</summary>
<b>A) DLP</b>

DLP policies can block or warn users about sending sensitive data via email.
</details>

---

### Question 38
**Where do you manage DNS records for Microsoft 365 services?**

A) Microsoft 365 admin center only  
B) Your DNS hosting provider  
C) Exchange admin center  
D) Teams admin center  

<details>
<summary>Answer</summary>
<b>B) Your DNS hosting provider</b>

DNS records are managed with your domain registrar or DNS provider, not in Microsoft 365.
</details>

---

### Question 39
**What is the purpose of tenant-wide security defaults?**

A) Disable all security  
B) Apply baseline protections like MFA and block legacy auth  
C) Only enable Teams  
D) Only enable OneDrive  

<details>
<summary>Answer</summary>
<b>B) Apply baseline protections like MFA and block legacy auth</b>

Security defaults enforce a baseline security posture without advanced configuration.
</details>

---

### Question 40
**Which feature provides legal hold on Teams messages?**

A) Retention policy in Purview  
B) Teams meeting policy  
C) OneDrive retention only  
D) Exchange transport rules  

<details>
<summary>Answer</summary>
<b>A) Retention policy in Purview</b>

Retention policies apply to Teams messages and preserve content for compliance.
</details>

---

### Question 41
**Which service is used for identity synchronization with on-premises AD?**

A) Azure AD Connect  
B) Teams  
C) Exchange Online  
D) SharePoint Online  

<details>
<summary>Answer</summary>
<b>A) Azure AD Connect</b>

Azure AD Connect synchronizes on-premises users/groups with Azure AD.
</details>

---

### Question 42
**What is the purpose of Exchange Online Protection (EOP)?**

A) Manage Teams meetings  
B) Provide basic email protection against spam and malware  
C) Manage user licenses  
D) Configure SharePoint sites  

<details>
<summary>Answer</summary>
<b>B) Provide basic email protection against spam and malware</b>

EOP provides baseline email filtering and protection for Exchange Online.
</details>

---

### Question 43
**Which of the following is a SharePoint admin task?**

A) Configure transport rules  
B) Manage site collections and sharing settings  
C) Configure Teams calling plans  
D) Manage user sign-in logs only  

<details>
<summary>Answer</summary>
<b>B) Manage site collections and sharing settings</b>

SharePoint admins handle site collections, storage, and sharing settings.
</details>

---

### Question 44
**How do you restrict who can create Microsoft 365 Groups?**

A) Exchange admin center  
B) Azure AD group creation policy  
C) Teams admin center  
D) SharePoint admin center  

<details>
<summary>Answer</summary>
<b>B) Azure AD group creation policy</b>

Azure AD group creation settings can limit group creation to specific users/groups.
</details>

---

### Question 45
**Which admin center manages Teams calling policies?**

A) Teams admin center  
B) Exchange admin center  
C) Microsoft 365 admin center  
D) SharePoint admin center  

<details>
<summary>Answer</summary>
<b>A) Teams admin center</b>

Calling and voice policies are managed in Teams admin center.
</details>

---

### Question 46
**Which compliance tool allows you to search mailbox content across users?**

A) Content search in Purview  
B) Exchange rules  
C) Teams policy  
D) Azure AD access reviews  

<details>
<summary>Answer</summary>
<b>A) Content search in Purview</b>

Content search in Purview allows searching mailboxes and SharePoint/OneDrive content.
</details>

---

### Question 47
**Which setting determines default sharing links in SharePoint?**

A) Azure AD  
B) SharePoint admin center  
C) Exchange admin center  
D) Teams admin center  

<details>
<summary>Answer</summary>
<b>B) SharePoint admin center</b>

Default link types are controlled in SharePoint admin center.
</details>

---

### Question 48
**Which feature helps track administrative actions across Microsoft 365?**

A) Audit logs  
B) Teams usage report  
C) Exchange mailbox rules  
D) OneDrive sync  

<details>
<summary>Answer</summary>
<b>A) Audit logs</b>

Audit logs record admin and user activities across Microsoft 365 services.
</details>

---

### Question 49
**Which action requires Global Administrator privileges?**

A) View Teams usage reports  
B) Reset user passwords  
C) Assign admin roles  
D) Create SharePoint sites  

<details>
<summary>Answer</summary>
<b>C) Assign admin roles</b>

Assigning admin roles typically requires Global Admin or Privileged Role Admin roles.
</details>

---

### Question 50
**What is the best way to keep Microsoft 365 secure over time?**

A) Configure once and never change  
B) Regularly review Secure Score, audit logs, and compliance reports  
C) Disable MFA after setup  
D) Limit monitoring to yearly reviews  

<details>
<summary>Answer</summary>
<b>B) Regularly review Secure Score, audit logs, and compliance reports</b>

Ongoing monitoring and reviews ensure configurations remain secure as threats evolve.
</details>

---

## 📊 Score Interpretation

| Score | Result | Recommendation |
|-------|--------|-----------------|
| **35-50** (70-100%) | **PASS** ✅ | Ready to take the exam! |
| **28-34** (56-68%) | **Review** ⚠️ | Review tenant management and compliance areas |
| **0-27** (<56%) | **Study More** ❌ | Focus on admin centers and service configuration |

---

<p align="right"><a href="../readme.md">Back to Certifications</a></p>
