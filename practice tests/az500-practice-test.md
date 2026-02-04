# 📝 AZ-500 Practice Test

<p align="right"><sub>Last updated: February 1, 2026</sub></p>

**Practice Exam for Microsoft Azure Security Technologies (AZ-500)** — Test your knowledge with 65 realistic questions covering all exam domains.

<p align="center">
    <a href="#instructions">Instructions</a> •
    <a href="#section1">Identity & Access</a> •
    <a href="#section2">Platform Protection</a> •
    <a href="#section3">Security Operations</a> •
    <a href="#section4">Data & Applications</a> •
    <a href="#answers">Answer Key</a>
</p>

---

## 📋 Test Instructions
<a id="instructions"></a>

- **Total Questions:** 65
- **Time Limit:** 120 minutes (recommended)
- **Passing Score:** 70% (46/65 correct)
- **Question Types:** Multiple choice, multiple select, scenario-based
- **Note:** Some questions may have multiple correct answers

**Exam Domain Breakdown:**
- Manage Identity & Access (30-35%) — Questions 1-23
- Implement Platform Protection (15-20%) — Questions 24-37
- Manage Security Operations (25-30%) — Questions 38-52
- Secure Data & Applications (20-25%) — Questions 53-65

---

## 🔐 Section 1: Manage Identity & Access (23 Questions)
<a id="section1"></a>

### Question 1
You need to ensure that all Azure resources in a subscription can only be accessed from specific IP addresses. What should you configure?

A) Network Security Groups (NSGs)  
B) Azure Firewall  
C) Azure Policy  
D) Conditional Access policies

---

### Question 2
Which Azure service provides centralized policy management and compliance assessment across your subscriptions?

A) Azure Monitor  
B) Azure Security Center  
C) Azure Policy  
D) Azure Advisor

---

### Question 3
You need to ensure MFA for all users accessing Azure portal from outside the corporate network. What should you configure?

A) Azure AD Identity Protection  
B) Azure AD Conditional Access  
C) Azure AD Privileged Identity Management  
D) Network Security Groups

---

### Question 4
Which authentication method provides the highest level of security for Azure AD?

A) Password + SMS  
B) Password + Microsoft Authenticator (notification)  
C) FIDO2 security keys  
D) Password only

---

### Question 5
You need to monitor and get alerts when privileged operations occur in Azure AD. What should you use?

A) Azure Monitor Activity Logs  
B) Azure AD Privileged Identity Management (PIM)  
C) Azure Security Center  
D) Azure Sentinel

---

### Question 6
You need to delegate the ability to reset passwords for non-admin users. Which role should you assign?

A) User Administrator  
B) Password Administrator  
C) Helpdesk Administrator  
D) Global Administrator

---

### Question 7
Which feature allows you to test Azure AD Conditional Access policies without impacting users?

A) Sign-in logs  
B) What If tool  
C) Access reviews  
D) Risk policies

---

### Question 8
What is the default session timeout for Azure AD Conditional Access policies?

A) 1 hour  
B) 8 hours  
C) 24 hours  
D) 90 days

---

### Question 9
Which Azure AD feature automatically blocks sign-ins from unfamiliar locations?

A) Conditional Access  
B) Identity Protection  
C) Privileged Identity Management  
D) Access Reviews

---

### Question 10
What is the purpose of Azure AD Connect?

A) Synchronize on-premises identities with Azure AD  
B) Connect Azure resources to on-premises networks  
C) Monitor Azure AD security  
D) Backup Azure AD data

---

### Question 11
Which protocol does Azure AD use for federation with external identity providers?

A) LDAP  
B) Kerberos  
C) SAML 2.0  
D) NTLM

---

### Question 12
What is the purpose of Azure AD B2B collaboration?

A) Manage business-to-business transactions  
B) Share resources with external users  
C) Backup Azure AD data  
D) Monitor business metrics

---

### Question 13
You need to implement just-in-time privileged access for Azure AD roles. What should you use?

A) Conditional Access  
B) Privileged Identity Management  
C) Identity Protection  
D) Access Reviews

---

### Question 14
What is the maximum number of Azure AD tenants a single user account can be a member of?

A) 50  
B) 100  
C) 500  
D) Unlimited

---

### Question 15
What is the purpose of Azure AD Identity Governance?

A) Monitor identity security  
B) Manage identity lifecycle and access  
C) Backup identity data  
D) Encrypt identity information

---

### Question 16
What is the purpose of Azure AD administrative units?

A) Measure resource usage  
B) Delegate administration for specific users or groups  
C) Monitor administrative activities  
D) Backup administrative settings

---

### Question 17
You need to protect against brute force attacks on Azure AD. What should you enable?

A) Conditional Access  
B) Smart lockout  
C) Identity Protection  
D) MFA

---

### Question 18
What is the purpose of Azure AD Seamless SSO?

A) Enable single sign-on for domain-joined devices  
B) Monitor sign-in activities  
C) Backup authentication data  
D) Encrypt authentication tokens

---

### Question 19
What is the purpose of Azure AD entitlement management?

A) Monitor entitlements  
B) Automate access request and approval workflows  
C) Backup entitlement data  
D) Encrypt entitlement information

---

### Question 20
You need to implement certificate-based authentication for Azure AD. What should you configure?

A) Conditional Access  
B) Certificate authorities in Azure AD  
C) Key Vault certificates  
D) Application Gateway

---

### Question 21
Which Azure AD feature provides periodic access reviews for privileged roles?

A) Conditional Access  
B) Access Reviews  
C) Identity Protection  
D) Privileged Identity Management

---

### Question 22
What is the purpose of Azure AD Domain Services?

A) Manage domain names  
B) Provide managed domain services without domain controllers  
C) Monitor domain activities  
D) Backup domain data

---

### Question 23
Which Azure AD feature requires users to re-authenticate when risk level changes?

A) Conditional Access  
B) Identity Protection  
C) Privileged Identity Management  
D) Access Reviews

---

## 🛡️ Section 2: Implement Platform Protection (14 Questions)
<a id="section2"></a>

### Question 24
You need to prevent accidental deletion of a critical resource group. What should you configure?

A) Azure Policy  
B) Resource lock (Delete)  
C) RBAC deny assignment  
D) Azure Backup

---

### Question 25
You need to encrypt traffic between Azure VMs in different virtual networks. What should you implement?

A) Azure VPN Gateway  
B) Azure Firewall  
C) Network Security Groups  
D) TLS certificates

---

### Question 26
Which Azure service provides DDoS protection at the network layer?

A) Azure Firewall  
B) Application Gateway WAF  
C) Azure DDoS Protection Standard  
D) Network Security Groups

---

### Question 27
You need to ensure that administrators can only access Azure VMs during specific hours. What should you use?

A) Network Security Groups  
B) Azure Policy  
C) Just-in-Time VM access  
D) Azure Bastion

---

### Question 28
You need to ensure that virtual machines can only access specific Azure PaaS services. What should you configure?

A) Network Security Groups  
B) Service endpoints  
C) Azure Firewall  
D) Application Security Groups

---

### Question 29
You need to implement network segmentation in Azure. What should you use?

A) Network Security Groups  
B) Subnets  
C) Application Security Groups  
D) All of the above

---

### Question 30
Which Azure service provides web application firewall capabilities?

A) Azure Firewall  
B) Application Gateway with WAF  
C) Network Security Groups  
D) Azure Front Door

---

### Question 31
Which Azure service provides centralized management of firewall rules across multiple subscriptions?

A) Azure Firewall Manager  
B) Network Security Groups  
C) Azure Policy  
D) Azure Security Center

---

### Question 32
What is the maximum number of rules allowed in a single Network Security Group?

A) 200  
B) 500  
C) 1,000  
D) 5,000

---

### Question 33
You need to implement network traffic filtering based on application FQDN. What should you use?

A) Network Security Groups  
B) Azure Firewall  
C) Application Security Groups  
D) Route tables

---

### Question 34
You need to ensure that Azure Kubernetes Service clusters use private IP addresses. What should you configure?

A) Network policies  
B) Private clusters  
C) Network Security Groups  
D) Azure Firewall

---

### Question 35
You need to implement zero-trust network security in Azure. What should you configure?

A) Network Security Groups only  
B) Azure Firewall only  
C) Combination of NSGs, Azure Firewall, and micro-segmentation  
D) VPN Gateway only

---

### Question 36
Which Azure service provides a secure tunnel for accessing Azure VMs without exposing RDP/SSH ports?

A) Azure VPN Gateway  
B) Azure Bastion  
C) Azure Firewall  
D) Application Gateway

---

### Question 37
You need to ensure compliance with data residency requirements. What should you configure?

A) Azure Policy  
B) Resource locks  
C) Azure regions  
D) Management groups

---

## 🔍 Section 3: Manage Security Operations (15 Questions)
<a id="section3"></a>

### Question 38
Which Azure service provides SIEM (Security Information and Event Management) capabilities?

A) Azure Monitor  
B) Azure Security Center  
C) Azure Sentinel  
D) Log Analytics

---

### Question 39
You need to monitor for suspicious activities across multiple Azure subscriptions. What should you deploy?

A) Azure Monitor  
B) Azure Sentinel  
C) Network Watcher  
D) Azure Advisor

---

### Question 40
What is the maximum retention period for Azure Activity Logs stored in a Log Analytics workspace?

A) 90 days  
B) 180 days  
C) 2 years  
D) 7 years (with configuration)

---

### Question 41
You need to audit all changes to RBAC role assignments. Where should you review the logs?

A) Azure Monitor Activity Logs  
B) Azure Security Center  
C) Azure Policy  
D) Azure Sentinel

---

### Question 42
Which Azure feature provides automatic security recommendations based on best practices?

A) Azure Policy  
B) Azure Advisor  
C) Azure Monitor  
D) Azure Sentinel

---

### Question 43
You need to ensure compliance with HIPAA regulations in Azure. What should you review?

A) Azure Security Center  
B) Microsoft Trust Center and Compliance Manager  
C) Azure Policy  
D) Azure Advisor

---

### Question 44
What is the purpose of Azure Security Benchmark?

A) Performance testing  
B) Security best practices and recommendations  
C) Cost optimization  
D) Resource monitoring

---

### Question 45
Which Azure service provides automated incident response capabilities?

A) Azure Monitor  
B) Azure Security Center  
C) Azure Sentinel with playbooks  
D) Azure Automation

---

### Question 46
Which Azure service provides vulnerability assessment for virtual machines?

A) Azure Policy  
B) Azure Defender for servers  
C) Network Watcher  
D) Azure Monitor

---

### Question 47
You need to scan container images for vulnerabilities before deployment. What should you use?

A) Azure Defender for container registries  
B) Azure Policy  
C) Network Security Groups  
D) Azure Firewall

---

### Question 48
You need to ensure that only approved applications can be installed on Azure VMs. What should you use?

A) Azure Policy  
B) Adaptive Application Controls  
C) Just-in-Time VM access  
D) Azure Firewall

---

### Question 49
You need to implement least privilege access for Azure resources. What should you use?

A) Azure RBAC  
B) Azure Policy  
C) Network Security Groups  
D) Conditional Access

---

### Question 50
What is the maximum number of custom roles that can be created in an Azure subscription?

A) 1,000  
B) 2,000  
C) 5,000  
D) Unlimited

---

### Question 51
You need to monitor for anomalous data access patterns in Azure SQL Database. What should you enable?

A) Advanced Threat Protection  
B) Auditing  
C) Transparent Data Encryption  
D) Always Encrypted

---

### Question 52
Which Azure feature provides immutable storage for compliance requirements?

A) Azure Backup  
B) Storage account immutability policies  
C) Resource locks  
D) Azure Site Recovery

---

## 🔒 Section 4: Secure Data & Applications (13 Questions)
<a id="section4"></a>

### Question 53
You need to encrypt data at rest in Azure Storage. Which encryption method is enabled by default?

A) Client-side encryption  
B) Azure Storage Service Encryption (SSE)  
C) Azure Disk Encryption  
D) Transport Layer Security (TLS)

---

### Question 54
What is the purpose of Azure Key Vault?

A) Store virtual machine backups  
B) Safeguard cryptographic keys and secrets  
C) Monitor security threats  
D) Manage user identities

---

### Question 55
You need to protect Azure SQL Database from SQL injection attacks. What should you implement?

A) Azure DDoS Protection  
B) Advanced Threat Protection  
C) Network Security Groups  
D) Azure Firewall

---

### Question 56
What is the minimum TLS version recommended for Azure services?

A) TLS 1.0  
B) TLS 1.1  
C) TLS 1.2  
D) TLS 1.3

---

### Question 57
You need to rotate secrets in Azure Key Vault automatically. What should you configure?

A) Access policies  
B) Soft delete  
C) Rotation policy  
D) Purge protection

---

### Question 58
You need to ensure that all Azure SQL Databases use Transparent Data Encryption. What should you use?

A) Azure Policy  
B) Azure Security Center  
C) Azure Firewall  
D) Network Security Groups

---

### Question 59
What is the default retention period for soft-deleted items in Azure Key Vault?

A) 7 days  
B) 30 days  
C) 90 days  
D) 180 days

---

### Question 60
You need to prevent data exfiltration from Azure SQL Database. What should you implement?

A) Azure Firewall  
B) Private Link  
C) Network Security Groups  
D) DDoS Protection

---

### Question 61
You need to ensure that deleted Azure Key Vault items can be recovered. What should you enable?

A) Backup  
B) Soft delete  
C) Geo-replication  
D) Access policies

---

### Question 62
You need to ensure that all data transfers to Azure Storage use HTTPS. What should you configure?

A) Network Security Groups  
B) Secure transfer required  
C) Azure Firewall  
D) Private endpoints

---

### Question 63
You need to ensure that Azure Storage accounts cannot be accessed over public internet. What should you configure?

A) Firewall rules  
B) Private endpoints  
C) Service endpoints  
D) Network Security Groups

---

### Question 64
You need to ensure that Azure Functions only accept requests from specific domains. What should you configure?

A) CORS settings  
B) Network Security Groups  
C) Azure Firewall  
D) API Management

---

### Question 65
You need to encrypt individual columns in Azure SQL Database. What should you implement?

A) Transparent Data Encryption  
B) Always Encrypted  
C) Azure Disk Encryption  
D) Storage Service Encryption

---

## ✅ Answer Key
<a id="answers"></a>

### Section 1: Manage Identity & Access (Questions 1-23)

**1. Answer: C** - Azure Policy  
*Explanation:* Azure Policy can enforce organizational standards and assess compliance at scale. You can create policies to restrict resource access based on network locations or IP addresses across all resources in a subscription.

**2. Answer: C** - Azure Policy  
*Explanation:* Azure Policy provides centralized policy management and compliance assessment. It evaluates resources against policies and provides compliance reporting across subscriptions.

**3. Answer: B** - Azure AD Conditional Access  
*Explanation:* Conditional Access policies allow you to enforce MFA based on conditions such as location, device, or risk level when accessing Azure resources.

**4. Answer: C** - FIDO2 security keys  
*Explanation:* FIDO2 security keys provide passwordless authentication and are phishing-resistant, offering the highest level of security among the options listed.

**5. Answer: B** - Azure AD Privileged Identity Management (PIM)  
*Explanation:* PIM provides monitoring, alerts, and audit history for privileged role assignments and activations in Azure AD and Azure resources.

**6. Answer: C** - Helpdesk Administrator  
*Explanation:* The Helpdesk Administrator role can reset passwords for non-administrators and other Helpdesk Administrators without having full administrative privileges.

**7. Answer: B** - What If tool  
*Explanation:* The What If tool in Conditional Access allows administrators to test how policies would apply to users without actually enforcing them.

**8. Answer: D** - 90 days  
*Explanation:* By default, Azure AD tokens have a 90-day rolling window for inactive sessions, though this can be configured through Conditional Access session controls.

**9. Answer: B** - Identity Protection  
*Explanation:* Azure AD Identity Protection uses machine learning to detect anomalous sign-in activities, including sign-ins from unfamiliar locations, and can automatically block or require additional verification.

**10. Answer: A** - Synchronize on-premises identities with Azure AD  
*Explanation:* Azure AD Connect synchronizes user identities, groups, and credentials from on-premises Active Directory to Azure AD, enabling hybrid identity scenarios.

**11. Answer: C** - SAML 2.0  
*Explanation:* Azure AD uses SAML 2.0, OAuth 2.0, and OpenID Connect for federation with external identity providers, with SAML 2.0 being the primary protocol for enterprise SSO.

**12. Answer: B** - Share resources with external users  
*Explanation:* Azure AD B2B allows organizations to securely share applications and resources with guest users from external organizations while maintaining control over access.

**13. Answer: B** - Privileged Identity Management  
*Explanation:* Azure AD Privileged Identity Management (PIM) enables just-in-time privileged access to Azure AD and Azure resources, requiring approval and justification for role activation.

**14. Answer: C** - 500  
*Explanation:* A single user account can be a member or guest in up to 500 Azure AD tenants, allowing multi-organization collaboration.

**15. Answer: B** - Manage identity lifecycle and access  
*Explanation:* Azure AD Identity Governance helps organizations balance security and productivity by automating identity lifecycle, access reviews, and privileged access management.

**16. Answer: B** - Delegate administration for specific users or groups  
*Explanation:* Administrative units allow you to subdivide your organization and delegate administrative permissions for specific subsets of users, groups, or devices.

**17. Answer: B** - Smart lockout  
*Explanation:* Azure AD smart lockout helps lock out bad actors trying to guess passwords or use brute force methods while allowing legitimate users to continue accessing their accounts.

**18. Answer: A** - Enable single sign-on for domain-joined devices  
*Explanation:* Azure AD Seamless SSO automatically signs in users when they're on domain-joined devices connected to the corporate network, providing a seamless authentication experience.

**19. Answer: B** - Automate access request and approval workflows  
*Explanation:* Azure AD entitlement management automates access request workflows, approvals, and lifecycle management for access packages containing multiple resources.

**20. Answer: B** - Certificate authorities in Azure AD  
*Explanation:* Azure AD certificate-based authentication requires configuring certificate authorities in Azure AD, enabling users to authenticate using X.509 certificates.

**21. Answer: B** - Access Reviews  
*Explanation:* Azure AD Access Reviews enable periodic certification of user access to groups, applications, and privileged roles, ensuring users retain only necessary access.

**22. Answer: B** - Provide managed domain services without domain controllers  
*Explanation:* Azure AD Domain Services provides managed domain services such as domain join, group policy, LDAP, and Kerberos/NTLM authentication without deploying domain controllers.

**23. Answer: B** - Identity Protection  
*Explanation:* Azure AD Identity Protection can detect risk level changes and automatically require step-up authentication or block access based on configured risk policies.

---

### Section 2: Implement Platform Protection (Questions 24-37)

**24. Answer: B** - Resource lock (Delete)  
*Explanation:* A Delete lock prevents deletion of resources while still allowing modifications. This protects critical resources from accidental deletion.

**25. Answer: A** - Azure VPN Gateway  
*Explanation:* Azure VPN Gateway enables encrypted IPsec/IKE VPN tunnels between virtual networks or between a virtual network and on-premises networks.

**26. Answer: C** - Azure DDoS Protection Standard  
*Explanation:* Azure DDoS Protection Standard provides enhanced DDoS mitigation features tuned specifically to Azure Virtual Network resources, protecting against volumetric and protocol attacks.

**27. Answer: C** - Just-in-Time VM access  
*Explanation:* Just-in-Time (JIT) VM access reduces exposure to attacks by controlling when and for how long management ports are open, including time-based restrictions.

**28. Answer: B** - Service endpoints  
*Explanation:* Virtual Network service endpoints extend your VNet private address space to Azure PaaS services, allowing VMs to access services directly over the Azure backbone network.

**29. Answer: D** - All of the above  
*Explanation:* Effective network segmentation uses multiple layers: subnets for logical separation, NSGs for traffic filtering, and Application Security Groups for application-centric security policies.

**30. Answer: B** - Application Gateway with WAF  
*Explanation:* Azure Application Gateway with Web Application Firewall (WAF) protects web applications from common exploits and vulnerabilities using OWASP core rule sets.

**31. Answer: A** - Azure Firewall Manager  
*Explanation:* Azure Firewall Manager provides central security policy and route management for multiple Azure Firewall instances across subscriptions and regions.

**32. Answer: C** - 1,000  
*Explanation:* A Network Security Group can contain up to 1,000 security rules (default quota is 200, but can be increased to 1,000 through support request).

**33. Answer: B** - Azure Firewall  
*Explanation:* Azure Firewall supports FQDN-based filtering rules, allowing you to control outbound traffic based on fully qualified domain names rather than just IP addresses.

**34. Answer: B** - Private clusters  
*Explanation:* Private AKS clusters use private IP addresses for the API server, ensuring that network traffic between your API server and node pools remains on the private network only.

**35. Answer: C** - Combination of NSGs, Azure Firewall, and micro-segmentation  
*Explanation:* Zero-trust networking requires defense in depth with multiple layers of security controls, including network segmentation, traffic filtering, identity verification, and least privilege access.

**36. Answer: B** - Azure Bastion  
*Explanation:* Azure Bastion provides secure RDP and SSH connectivity to virtual machines directly through the Azure portal without exposing VMs to public internet or requiring public IP addresses.

**37. Answer: C** - Azure regions  
*Explanation:* Azure regions determine the physical location where resources are deployed. Selecting appropriate regions ensures compliance with data residency and sovereignty requirements.

---

### Section 3: Manage Security Operations (Questions 38-52)

**38. Answer: C** - Azure Sentinel  
*Explanation:* Azure Sentinel is a cloud-native SIEM and SOAR solution that provides intelligent security analytics and threat intelligence across the enterprise.

**39. Answer: B** - Azure Sentinel  
*Explanation:* Azure Sentinel is a cloud-native SIEM that can collect data from multiple subscriptions and data sources, providing unified security monitoring and threat detection.

**40. Answer: D** - 7 years (with configuration)  
*Explanation:* Log Analytics workspaces can retain data for up to 7 years (2,555 days) when configured, though longer retention increases costs.

**41. Answer: A** - Azure Monitor Activity Logs  
*Explanation:* Azure Activity Logs record all control plane operations including RBAC role assignments, providing audit trails for who made what changes and when.

**42. Answer: B** - Azure Advisor  
*Explanation:* Azure Advisor provides personalized recommendations for security, cost, performance, operational excellence, and reliability based on best practices.

**43. Answer: B** - Microsoft Trust Center and Compliance Manager  
*Explanation:* The Microsoft Trust Center provides information about compliance offerings, and Compliance Manager helps assess and manage compliance with standards like HIPAA.

**44. Answer: B** - Security best practices and recommendations  
*Explanation:* Azure Security Benchmark provides cloud-centric security recommendations based on common compliance frameworks, helping organizations improve their security posture.

**45. Answer: C** - Azure Sentinel with playbooks  
*Explanation:* Azure Sentinel playbooks use Azure Logic Apps to automate incident response workflows, enabling automated investigation and remediation of security threats.

**46. Answer: B** - Azure Defender for servers  
*Explanation:* Azure Defender for servers includes integrated vulnerability assessment scanning powered by Qualys, identifying security vulnerabilities in your virtual machines.

**47. Answer: A** - Azure Defender for container registries  
*Explanation:* Azure Defender for container registries scans images for vulnerabilities when pushed to the registry, pulled, or imported.

**48. Answer: B** - Adaptive Application Controls  
*Explanation:* Adaptive Application Controls in Azure Defender use machine learning to define allowlists of safe applications for your VMs, blocking unapproved applications.

**49. Answer: A** - Azure RBAC  
*Explanation:* Azure Role-Based Access Control (RBAC) enables fine-grained access management, allowing you to grant users only the permissions they need to perform their jobs.

**50. Answer: C** - 5,000  
*Explanation:* Azure supports up to 5,000 custom role definitions per subscription. This limit applies to custom roles created using Azure RBAC.

**51. Answer: A** - Advanced Threat Protection  
*Explanation:* Advanced Threat Protection for Azure SQL Database uses machine learning to detect anomalous database activities that indicate unusual and potentially harmful access patterns.

**52. Answer: B** - Storage account immutability policies  
*Explanation:* Immutability policies for blob storage allow you to store data in a WORM (Write Once, Read Many) state, meeting regulatory requirements for immutable storage.

---

### Section 4: Secure Data & Applications (Questions 53-65)

**53. Answer: B** - Azure Storage Service Encryption (SSE)  
*Explanation:* Azure Storage Service Encryption is enabled by default for all storage accounts and cannot be disabled. It automatically encrypts data before persisting it to storage.

**54. Answer: B** - Safeguard cryptographic keys and secrets  
*Explanation:* Azure Key Vault is designed to securely store and manage secrets, encryption keys, and certificates used by cloud applications and services.

**55. Answer: B** - Advanced Threat Protection  
*Explanation:* Advanced Threat Protection for Azure SQL Database detects anomalous activities including SQL injection attempts and provides security alerts.

**56. Answer: C** - TLS 1.2  
*Explanation:* TLS 1.2 is the minimum recommended version for Azure services. TLS 1.0 and 1.1 are deprecated due to security vulnerabilities.

**57. Answer: C** - Rotation policy  
*Explanation:* Azure Key Vault supports automatic rotation policies for secrets and certificates, enabling automated lifecycle management without manual intervention.

**58. Answer: A** - Azure Policy  
*Explanation:* Azure Policy can enforce that all SQL Databases must have Transparent Data Encryption enabled, ensuring compliance across subscriptions.

**59. Answer: C** - 90 days  
*Explanation:* Soft-deleted items in Azure Key Vault are retained for 90 days by default, allowing recovery during this period before permanent deletion.

**60. Answer: B** - Private Link  
*Explanation:* Azure Private Link provides private connectivity to Azure SQL Database, eliminating data exposure to the public internet and preventing data exfiltration through network isolation.

**61. Answer: B** - Soft delete  
*Explanation:* Soft delete for Azure Key Vault ensures that deleted vaults and vault objects are retained for 90 days, allowing recovery from accidental deletions.

**62. Answer: B** - Secure transfer required  
*Explanation:* The "Secure transfer required" setting on Azure Storage accounts enforces HTTPS for all requests, rejecting HTTP connections to ensure data is encrypted in transit.

**63. Answer: B** - Private endpoints  
*Explanation:* Private endpoints bring Azure services into your virtual network, making them accessible only through private IP addresses and blocking all public internet access.

**64. Answer: A** - CORS settings  
*Explanation:* Cross-Origin Resource Sharing (CORS) settings in Azure Functions control which domains can make cross-origin requests to your function app.

**65. Answer: B** - Always Encrypted  
*Explanation:* Always Encrypted allows encryption of specific columns in Azure SQL Database, with keys never revealed to the database engine, providing protection against high-privileged unauthorized users.

---

## 📊 Scoring Guide

Calculate your score:
- **59-65 correct (90-100%):** Excellent! You're ready for the exam
- **52-58 correct (80-89%):** Very good! Review missed topics
- **46-51 correct (70-78%):** Good! You're near passing - focus on weak areas
- **39-45 correct (60-69%):** Need more study - review all domains
- **Below 39 (< 60%):** Significant study needed - start with Microsoft Learn modules

---

## 📚 Study Resources

If you scored below 70%, focus on these areas:

### Identity & Access Management
- [Azure AD Identity Protection](https://learn.microsoft.com/en-us/training/modules/protect-identities-with-aad-idp/)
- [Conditional Access Policies](https://learn.microsoft.com/en-us/training/modules/plan-implement-administer-conditional-access/)
- [Privileged Identity Management](https://learn.microsoft.com/en-us/training/modules/azure-ad-privileged-identity-management/)

### Platform Protection
- [Network Security Groups and Service Endpoints](https://learn.microsoft.com/en-us/training/modules/secure-and-isolate-with-nsg-and-service-endpoints/)
- [Azure Firewall](https://learn.microsoft.com/en-us/training/modules/introduction-azure-firewall/)
- [Just-in-Time VM Access](https://learn.microsoft.com/en-us/training/modules/secure-vms-with-azure-security-center/)

### Security Operations
- [Azure Sentinel](https://learn.microsoft.com/en-us/training/paths/security-ops-sentinel/)
- [Azure Security Center](https://learn.microsoft.com/en-us/training/modules/resolve-threats-with-azure-security-center/)
- [Security Monitoring and Logging](https://learn.microsoft.com/en-us/training/modules/monitor-report-aad-security-events/)

### Data & Application Security
- [Azure Key Vault](https://learn.microsoft.com/en-us/training/modules/configure-and-manage-azure-key-vault/)
- [Azure SQL Security](https://learn.microsoft.com/en-us/training/modules/secure-your-azure-sql-database/)
- [Storage Security](https://learn.microsoft.com/en-us/training/modules/secure-azure-storage-account/)

---

## 💡 Exam Tips

1. **Understand security layers** — Azure security uses defense in depth principles
2. **Know identity protection features** — Conditional Access, PIM, and Identity Protection are key
3. **Master network security** — NSGs, Azure Firewall, service endpoints, and private endpoints
4. **Study Key Vault thoroughly** — Key management, secrets, and certificates are frequently tested
5. **Understand threat protection** — Azure Sentinel, Defender, and Advanced Threat Protection
6. **Time management** — Spend about 1.5-2 minutes per question
7. **Read scenario questions carefully** — Many questions describe real-world security situations
8. **Hands-on lab experience** — Practice implementing security controls in Azure

---

## 🎯 Next Steps

1. ✅ Review any questions you got wrong
2. 📖 Study the corresponding Microsoft Learn modules
3. 🔄 Retake this practice test until you consistently score 90%+
4. 🧪 Complete hands-on labs in your own Azure subscription
5. 📝 Take the official Microsoft practice test
6. 📅 Schedule your AZ-500 exam when ready

---

<p align="right"><a href="../README.md">Back to Student Resources</a></p>