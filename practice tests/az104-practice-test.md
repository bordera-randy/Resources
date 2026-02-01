# 📝 AZ-104 Practice Test

<p align="right"><sub>Last updated: February 1, 2026</sub></p>

**Practice Exam for Microsoft Azure Administrator Associate (AZ-104)** — Test your knowledge with 50 realistic questions covering all exam domains.

<p align="center">
  <a href="#instructions">Instructions</a> •
  <a href="#section1">Azure Identity & Governance</a> •
  <a href="#section2">Azure Compute</a> •
  <a href="#section3">Azure Storage</a> •
  <a href="#section4">Azure Networking</a> •
  <a href="#section5">Monitoring & Management</a> •
  <a href="#answers">Answer Key</a>
</p>

---

## 📋 Test Instructions
<a id="instructions"></a>

- **Total Questions:** 50
- **Time Limit:** 90 minutes (recommended)
- **Passing Score:** 70% (35/50 correct)
- **Question Types:** Multiple choice, multiple select, drag-and-drop, case studies
- **Note:** Some questions may have multiple correct answers

**Exam Domain Breakdown:**
- Identity & Governance (20-25%) — Questions 1-12
- Azure Compute (20-25%) — Questions 13-24
- Azure Storage (15-20%) — Questions 25-34
- Azure Networking (20-25%) — Questions 35-44
- Monitoring & Management (10-15%) — Questions 45-50

---

## 🔑 Section 1: Azure Identity & Governance (12 Questions)
<a id="section1"></a>

### Question 1
Which Azure service allows you to manage user identities and control access to resources?

A) Azure Key Vault  
B) Microsoft Entra ID  
C) Azure Policy  
D) Azure Blueprints

---

### Question 2
What is the purpose of Role-Based Access Control (RBAC)?

A) To encrypt data in transit  
B) To assign permissions to users based on their role  
C) To backup resources automatically  
D) To monitor resource usage

---

### Question 3
You need to assign permissions to a user at the subscription level. What built-in role would allow them to manage all resources but not assign access to others?

A) Owner  
B) Contributor  
C) Reader  
D) User Access Administrator

---

### Question 4
**Select all that apply:** Which of the following are components of Azure RBAC? (Multiple answers)

A) Security Principal  
B) Role Definition  
C) Scope  
D) Encryption Key  
E) Assignment

---

### Question 5
What is the difference between a built-in role and a custom role in Azure?

A) Built-in roles are free; custom roles cost extra  
B) Built-in roles are predefined by Microsoft; custom roles are user-defined  
C) Custom roles are more secure than built-in roles  
D) Built-in roles cannot be modified

---

### Question 6
Which service allows you to enforce organizational standards across Azure resources?

A) Azure Advisor  
B) Azure Policy  
C) Azure Blueprints  
D) Azure Monitor

---

### Question 7
**True or False:** Azure Policy can automatically remediate non-compliant resources.

A) True  
B) False

---

### Question 8
What is a Management Group used for?

A) To manage storage accounts  
B) To organize subscriptions and manage policies at scale  
C) To host web applications  
D) To monitor application performance

---

### Question 9
You want to create a reusable set of Azure resources that includes VMs, storage, and networking. What should you use?

A) Azure Blueprints  
B) Azure Resource Manager (ARM) Template  
C) Both A and B  
D) Neither

---

### Question 10
Which authentication method provides the strongest security for Azure administrators?

A) Username and password  
B) Multi-Factor Authentication (MFA)  
C) Passwordless sign-in  
D) Both B and C

---

### Question 11
What is the purpose of Conditional Access policies in Entra ID?

A) To back up user data  
B) To control access based on specific conditions (location, device, risk)  
C) To encrypt passwords  
D) To monitor user activity only

---

### Question 12
**Select all that apply:** Which of the following are best practices for managing Azure identities? (Multiple answers)

A) Enable MFA for all users  
B) Use service principals for application authentication  
C) Share credentials across team members  
D) Implement Conditional Access policies  
E) Use legacy authentication protocols

---

## 💻 Section 2: Azure Compute (12 Questions)
<a id="section2"></a>

### Question 13
You need to deploy a Windows Server 2022 VM. What is the primary tool for initial configuration after deployment?

A) Azure CLI  
B) Remote Desktop Protocol (RDP)  
C) SSH  
D) Azure Portal only

---

### Question 14
What is a Virtual Machine Scale Set (VMSS) used for?

A) To create identical VMs that automatically scale based on demand  
B) To backup virtual machines  
C) To monitor VM performance  
D) To encrypt VM disks

---

### Question 15
**True or False:** Availability Sets and Availability Zones serve the same purpose for ensuring high availability.

A) True  
B) False

---

### Question 16
Which of the following is a characteristic of an Availability Zone?

A) It's a single datacenter  
B) It's a physically separate location within an Azure region with independent infrastructure  
C) It's the same as a region  
D) It provides lower costs than standard deployments

---

### Question 17
You want to deploy containers in Azure without managing Kubernetes. What service should you use?

A) Azure Virtual Machines  
B) Azure Container Instances (ACI)  
C) Azure Kubernetes Service (AKS)  
D) Azure App Service

---

### Question 18
What is Azure Batch used for?

A) Running large-scale parallel computing jobs efficiently  
B) Batch backup of storage accounts  
C) Managing batches of users  
D) Scheduling maintenance windows

---

### Question 19
**Select all that apply:** Which factors should you consider when selecting a VM size? (Multiple answers)

A) CPU cores and memory requirements  
B) Storage needs  
C) Network bandwidth requirements  
D) Company location  
E) The VM's color in the portal

---

### Question 20
What is the difference between a managed disk and an unmanaged disk?

A) Managed disks are automatically backed up; unmanaged disks are not  
B) Microsoft manages the storage account for managed disks; you manage it for unmanaged disks  
C) Managed disks are more expensive  
D) Unmanaged disks have better performance

---

### Question 21
You need to automatically start VMs at 8 AM and stop them at 6 PM. What should you use?

A) Azure Automation runbooks with scheduled triggers  
B) Azure Functions  
C) Manual management  
D) Azure Logic Apps

---

### Question 22
What is the purpose of a Network Interface Card (NIC) in Azure?

A) To provide compute power to VMs  
B) To enable network connectivity for VMs  
C) To store data  
D) To manage user access

---

### Question 23
**True or False:** You can change the VM size of a running VM without stopping it.

A) True  
B) False

---

### Question 24
Which Azure service allows you to host and manage Docker containers with orchestration capabilities?

A) Azure Container Instances  
B) Azure App Service  
C) Azure Kubernetes Service (AKS)  
D) Azure Virtual Machines

---

## 💾 Section 3: Azure Storage (10 Questions)
<a id="section3"></a>

### Question 25
What are the four types of Azure Storage accounts?

A) Standard, Premium, Archive, Hot  
B) Blob, File, Queue, Table  
C) General-purpose v1, General-purpose v2, BlockBlobStorage, FileStorage  
D) Local, Regional, Global, Premium

---

### Question 26
Which Azure Storage service is best for sharing files between on-premises and cloud environments?

A) Blob Storage  
B) Azure Files  
C) Queue Storage  
D) Table Storage

---

### Question 27
**Select all that apply:** What are the access tiers for Azure Blob Storage? (Multiple answers)

A) Hot  
B) Cool  
C) Archive  
D) Standard  
E) Premium

---

### Question 28
What is the purpose of storage account replication?

A) To create backups of data  
B) To copy data to protect against failures  
C) To improve access speed  
D) Both B and C

---

### Question 29
**True or False:** You can change the replication type of an existing storage account without recreating it.

A) True  
B) False

---

### Question 30
Which replication option provides the highest redundancy?

A) Locally Redundant Storage (LRS)  
B) Zone-Redundant Storage (ZRS)  
C) Geo-Redundant Storage (GRS)  
D) Read-Access Geo-Redundant Storage (RA-GRS)

---

### Question 31
What is Azure Table Storage used for?

A) Storing large files  
B) Storing structured, NoSQL data  
C) Creating virtual machines  
D) Managing user identities

---

### Question 32
**Select all that apply:** Which access methods can you use to connect to Azure Files? (Multiple answers)

A) SMB protocol  
B) NFS protocol  
C) HTTPS/REST API  
D) SSH  
E) FTP

---

### Question 33
What should you use to restrict access to a storage account to specific virtual networks?

A) Storage account firewall rules  
B) Network Security Groups  
C) Shared Access Signatures  
D) Storage account keys

---

### Question 34
**True or False:** Blob Storage can store any type of file without limitations.

A) True  
B) False

---

## 🌐 Section 4: Azure Networking (10 Questions)
<a id="section4"></a>

### Question 35
What is the purpose of a Network Security Group (NSG)?

A) To manage DNS resolution  
B) To filter network traffic to Azure resources  
C) To provide encryption  
D) To load balance traffic

---

### Question 36
**Select all that apply:** What information does an NSG security rule contain? (Multiple answers)

A) Priority  
B) Direction (Inbound/Outbound)  
C) Protocol  
D) Source and destination  
E) Action (Allow/Deny)

---

### Question 37
What is the difference between a network security group (NSG) and an Azure Firewall?

A) NSGs are stateless; Azure Firewall is stateful  
B) NSGs work at the subnet level; Azure Firewall works at the network perimeter  
C) Azure Firewall is cheaper  
D) Both A and B

---

### Question 38
You want to connect your on-premises network to Azure securely and permanently. What should you use?

A) VPN Gateway (Site-to-Site VPN)  
B) Azure ExpressRoute  
C) Both can work, but ExpressRoute is more reliable  
D) Internet connection

---

### Question 39
**True or False:** A Virtual Network (VNet) can span multiple Azure regions.

A) True  
B) False

---

### Question 40
What is VNet peering used for?

A) Monitoring VNet performance  
B) Connecting two VNets as if they were on the same network  
C) Encrypting network traffic  
D) Load balancing

---

### Question 41
**Select all that apply:** Which of the following are types of VPN connections? (Multiple answers)

A) Site-to-Site VPN  
B) Point-to-Site VPN  
C) VNet-to-VNet VPN  
D) Peer-to-Peer VPN  
E) ExpressRoute

---

### Question 42
What is Azure Load Balancer's primary function?

A) To manage DNS names  
B) To distribute network traffic across multiple resources  
C) To provide encryption  
D) To monitor network performance

---

### Question 43
What is the difference between a Basic Load Balancer and a Standard Load Balancer?

A) Standard supports more concurrent connections and availability zones  
B) Basic is more expensive  
C) They function identically  
D) Basic only works with VMs

---

### Question 44
**True or False:** You can create a subnet with a /31 CIDR prefix in Azure.

A) True  
B) False

---

## 📊 Section 5: Monitoring & Management (6 Questions)
<a id="section5"></a>

### Question 45
What is Azure Monitor's primary purpose?

A) To manage storage accounts  
B) To collect, analyze, and act on telemetry from Azure resources  
C) To create backups  
D) To manage user identities

---

### Question 46
**Select all that apply:** What types of data can Azure Monitor collect? (Multiple answers)

A) Metrics  
B) Logs  
C) Traces  
D) Documents  
E) Application Insights data

---

### Question 47
What is the purpose of Azure Advisor?

A) To manage costs and provide recommendations for optimization  
B) To back up resources  
C) To monitor VM performance only  
D) To assign RBAC permissions

---

### Question 48
**True or False:** Azure Backup can back up on-premises servers.

A) True  
B) False

---

### Question 49
What is the primary difference between Azure Backup and Azure Site Recovery?

A) Backup backs up data; Site Recovery provides disaster recovery with replication  
B) They serve identical purposes  
C) Site Recovery is only for databases  
D) Backup is more expensive

---

### Question 50
**Select all that apply:** Which of the following are components of an Azure Automation runbook? (Multiple answers)

A) PowerShell scripts  
B) Python code  
C) Graphical workflows  
D) HTML templates  
E) Webhooks for triggering

---

## ✅ Answer Key
<a id="answers"></a>

### Section 1: Azure Identity & Governance (Questions 1-12)

**1. Answer: B** - Microsoft Entra ID  
*Explanation:* Microsoft Entra ID (formerly Azure Active Directory) is Azure's identity and access management service. It provides authentication, user management, and access control to Azure resources.

**2. Answer: B** - To assign permissions to users based on their role  
*Explanation:* Role-Based Access Control (RBAC) is a mechanism to assign permissions based on user roles. This allows fine-grained access control where different users have different levels of permissions.

**3. Answer: B** - Contributor  
*Explanation:* The Contributor role allows users to manage all resources but cannot grant access to others. The Owner role can grant access, while Reader only allows viewing, and User Access Administrator only manages access.

**4. Answer: A, B, C, E** - Security Principal, Role Definition, Scope, Assignment  
*Explanation:* RBAC requires a security principal (user/service), a role definition (permissions), a scope (subscription/resource group), and an assignment (linking them together). Encryption Key is not part of RBAC.

**5. Answer: B** - Built-in roles are predefined by Microsoft; custom roles are user-defined  
*Explanation:* Microsoft provides built-in roles like Owner, Contributor, and Reader. If these don't meet your needs, you can create custom roles with specific permissions.

**6. Answer: B** - Azure Policy  
*Explanation:* Azure Policy is used to create, assign, and manage policies that enforce organizational standards and compliance requirements across Azure resources.

**7. Answer: A** - True  
*Explanation:* Azure Policy includes a "remediation" feature that can automatically correct non-compliant resources according to the policy definition.

**8. Answer: B** - To organize subscriptions and manage policies at scale  
*Explanation:* Management Groups allow you to organize multiple subscriptions into a hierarchy for unified governance, policy management, and compliance across many subscriptions.

**9. Answer: C** - Both A and B  
*Explanation:* Both Azure Blueprints and ARM Templates can define and deploy reusable sets of resources. Blueprints add additional governance features, while ARM Templates are the underlying deployment mechanism.

**10. Answer: D** - Both B and C  
*Explanation:* Both Multi-Factor Authentication (MFA) and passwordless sign-in (using Windows Hello, FIDO2 keys, etc.) provide strong security. Passwordless is increasingly recommended as more secure than MFA.

**11. Answer: B** - To control access based on specific conditions (location, device, risk)  
*Explanation:* Conditional Access in Entra ID allows you to grant or deny access based on conditions such as user location, device compliance, risk level, and other factors.

**12. Answer: A, B, D** - Enable MFA for all users, Use service principals for application authentication, Implement Conditional Access policies  
*Explanation:* These are security best practices. Sharing credentials across team members violates security principles, and legacy authentication protocols are deprecated for security reasons.

---

### Section 2: Azure Compute (Questions 13-24)

**13. Answer: B** - Remote Desktop Protocol (RDP)  
*Explanation:* For Windows VMs, RDP is the primary method to connect and configure the operating system. The Azure Portal can be used to create the VM, but RDP is needed for OS-level configuration.

**14. Answer: A** - To create identical VMs that automatically scale based on demand  
*Explanation:* Virtual Machine Scale Sets automatically create and delete VM instances to match demand. This enables cost-effective scaling without manual intervention.

**15. Answer: B** - False  
*Explanation:* While both provide high availability, Availability Sets protect against datacenter failures within a region, while Availability Zones protect against zone-level failures using physically separate datacenters.

**16. Answer: B** - It's a physically separate location within an Azure region with independent infrastructure  
*Explanation:* Availability Zones are distinct datacenters within a region, each with independent power, cooling, and networking to protect against zone-level failures.

**17. Answer: B** - Azure Container Instances (ACI)  
*Explanation:* Azure Container Instances allows you to run containers without managing Kubernetes infrastructure. It's simpler than AKS for basic container deployments.

**18. Answer: A** - Running large-scale parallel computing jobs efficiently  
*Explanation:* Azure Batch is designed for large-scale parallel and high-performance computing workloads, handling job scheduling, resource management, and task coordination.

**19. Answer: A, B, C** - CPU cores and memory requirements, Storage needs, Network bandwidth requirements  
*Explanation:* VM size selection depends on workload requirements for compute, memory, storage, and network performance. Company location and color are irrelevant factors.

**20. Answer: B** - Microsoft manages the storage account for managed disks; you manage it for unmanaged disks  
*Explanation:* Managed disks are simpler—Microsoft handles the underlying storage accounts. Unmanaged disks require you to create and manage storage accounts yourself.

**21. Answer: A** - Azure Automation runbooks with scheduled triggers  
*Explanation:* Azure Automation allows you to create runbooks that can be scheduled to start and stop VMs at specific times, automating the process.

**22. Answer: B** - To enable network connectivity for VMs  
*Explanation:* A Network Interface Card (NIC) provides the network interface for VMs, enabling communication with other resources on the network and the internet.

**23. Answer: B** - False  
*Explanation:* Most VM size changes require the VM to be stopped. Some minor resizing within the same family might work on running VMs, but full resizing typically requires stopping.

**24. Answer: C** - Azure Kubernetes Service (AKS)  
*Explanation:* AKS provides managed Kubernetes orchestration for containers. Azure Container Instances runs containers without orchestration.

---

### Section 3: Azure Storage (Questions 25-34)

**25. Answer: C** - General-purpose v1, General-purpose v2, BlockBlobStorage, FileStorage  
*Explanation:* Azure storage account types include general-purpose accounts (v1 and v2 for various workloads) and specialized accounts for specific storage types like block blobs and files.

**26. Answer: B** - Azure Files  
*Explanation:* Azure Files provides SMB file shares that can be accessed from on-premises, cloud VMs, and applications, making it ideal for hybrid scenarios.

**27. Answer: A, B, C** - Hot, Cool, Archive  
*Explanation:* These are the three access tiers for Blob Storage, balancing access frequency with cost. Standard and Premium are storage account types, not access tiers.

**28. Answer: D** - Both B and C  
*Explanation:* Replication protects against failures by copying data to other locations. It also improves access speed by distributing data geographically.

**29. Answer: B** - False  
*Explanation:* Changing the replication type of an existing storage account requires recreating the account in most cases.

**30. Answer: D** - Read-Access Geo-Redundant Storage (RA-GRS)  
*Explanation:* RA-GRS provides the highest redundancy by replicating data to a secondary region and allowing read access from the secondary region if the primary fails.

**31. Answer: B** - Storing structured, NoSQL data  
*Explanation:* Azure Table Storage is a NoSQL data store for structured data with flexible schemas, ideal for large-scale unstructured data storage.

**32. Answer: A, B, C** - SMB protocol, NFS protocol, HTTPS/REST API  
*Explanation:* Azure Files supports SMB and NFS for traditional file share access, and HTTPS/REST API for programmatic access. SSH and FTP are not supported.

**33. Answer: A** - Storage account firewall rules  
*Explanation:* Storage account firewall rules restrict access to specific virtual networks and IP addresses, providing network-level access control.

**34. Answer: B** - False  
*Explanation:* While Blob Storage can store most file types, there are limits on individual blob size (4.75 TB for block blobs, 8 TB for page blobs) and storage account capacity.

---

### Section 4: Azure Networking (Questions 35-44)

**35. Answer: B** - To filter network traffic to Azure resources  
*Explanation:* Network Security Groups contain inbound and outbound rules that allow or deny network traffic to Azure resources based on source, destination, port, and protocol.

**36. Answer: A, B, C, D, E** - Priority, Direction (Inbound/Outbound), Protocol, Source and destination, Action (Allow/Deny)  
*Explanation:* Each NSG rule specifies these elements to control which traffic is allowed or denied.

**37. Answer: D** - Both A and B  
*Explanation:* NSGs are stateless filters at the subnet level, while Azure Firewall is a stateful firewall at the network perimeter that can provide additional threat protection.

**38. Answer: C** - Both can work, but ExpressRoute is more reliable  
*Explanation:* Both VPN Gateway and ExpressRoute can connect on-premises networks to Azure. ExpressRoute provides dedicated, more reliable connectivity with better SLAs.

**39. Answer: B** - False  
*Explanation:* A Virtual Network exists within a single region. To connect VNets across regions, you use VNet peering or VPN.

**40. Answer: B** - Connecting two VNets as if they were on the same network  
*Explanation:* VNet peering allows resources in different VNets to communicate directly with low latency and high bandwidth, as if they were on the same network.

**41. Answer: A, B, C** - Site-to-Site VPN, Point-to-Site VPN, VNet-to-VNet VPN  
*Explanation:* These are valid VPN connection types. ExpressRoute is not VPN (it's dedicated connection), and "Peer-to-Peer VPN" is not a standard Azure connection type.

**42. Answer: B** - To distribute network traffic across multiple resources  
*Explanation:* Azure Load Balancer distributes incoming traffic across backend resources to improve availability and performance.

**43. Answer: A** - Standard supports more concurrent connections and availability zones  
*Explanation:* Standard Load Balancer provides better scalability, supports availability zones, and offers more features than Basic Load Balancer.

**44. Answer: B** - False  
*Explanation:* Azure reserves the first and last IP addresses in a subnet. For a /31 subnet (2 addresses), both would be reserved, leaving no usable IPs.

---

### Section 5: Monitoring & Management (Questions 45-50)

**45. Answer: B** - To collect, analyze, and act on telemetry from Azure resources  
*Explanation:* Azure Monitor is the comprehensive monitoring platform that collects metrics, logs, and traces from Azure resources, enabling visibility and alerting.

**46. Answer: A, B, C, E** - Metrics, Logs, Traces, Application Insights data  
*Explanation:* Azure Monitor collects time-series metrics, log entries, distributed traces, and application performance data. Documents are stored in databases, not monitored by Azure Monitor.

**47. Answer: A** - To manage costs and provide recommendations for optimization  
*Explanation:* Azure Advisor analyzes your Azure resources and provides recommendations for cost optimization, security, reliability, and performance improvements.

**48. Answer: A** - True  
*Explanation:* Azure Backup can back up on-premises servers, VMs, databases, and file shares using the Microsoft Azure Recovery Services Agent or Azure Backup Server.

**49. Answer: A** - Backup backs up data; Site Recovery provides disaster recovery with replication  
*Explanation:* Backup creates point-in-time copies of data. Site Recovery continuously replicates VMs to enable rapid recovery in case of disaster.

**50. Answer: A, B, C, E** - PowerShell scripts, Python code, Graphical workflows, Webhooks for triggering  
*Explanation:* Automation runbooks can use PowerShell, Python, or graphical workflows for automation tasks and can be triggered by webhooks. HTML templates are not used in runbooks.

---

## 📊 Scoring Guide

Calculate your score:
- **45-50 correct (90-100%):** Excellent! You're ready for the exam
- **40-44 correct (80-89%):** Very good! Review missed topics
- **35-39 correct (70-78%):** Good! You're near passing - focus on weak areas
- **30-34 correct (60-69%):** Need more study - review all domains
- **Below 30 (< 60%):** Significant study needed - start with Microsoft Learn modules

---

## 📚 Study Resources

If you scored below 70%, focus on these areas:

### Identity & Governance
- [Azure Identity and Access Management](https://learn.microsoft.com/en-us/training/modules/describe-azure-identity-access-security/)
- [Azure Policy and Blueprints](https://learn.microsoft.com/en-us/training/modules/build-cloud-governance-strategy-azure/)

### Azure Compute
- [Azure Virtual Machines](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/)
- [Azure Container Services](https://learn.microsoft.com/en-us/training/modules/describe-azure-containers-services/)

### Azure Storage
- [Azure Storage Services](https://learn.microsoft.com/en-us/training/modules/describe-azure-storage-services/)
- [Storage Redundancy and Replication](https://learn.microsoft.com/en-us/training/modules/describe-azure-storage-services/)

### Azure Networking
- [Azure Networking Services](https://learn.microsoft.com/en-us/training/modules/describe-azure-compute-networking-services/)
- [Network Security and Connectivity](https://learn.microsoft.com/en-us/training/modules/describe-azure-network-security/)

### Monitoring & Management
- [Azure Monitoring and Management](https://learn.microsoft.com/en-us/training/modules/describe-features-tools-manage-deploy-azure-resources/)
- [Azure Backup and Recovery](https://learn.microsoft.com/en-us/training/modules/describe-features-tools-manage-deploy-azure-resources/)

---

## 💡 Exam Tips

1. **Understand hands-on concepts** — AZ-104 emphasizes practical administration skills
2. **Know RBAC thoroughly** — It's foundational to Azure administration
3. **Study networking scenarios** — NSGs, VNets, and peering are frequently tested
4. **Master storage account options** — Know when to use each replication type and access tier
5. **Understand VM scaling** — Know VMSS, availability options, and sizing
6. **Time management** — Spend about 1-2 minutes per question
7. **Read scenario questions carefully** — Many questions describe real-world situations
8. **Hands-on lab experience** — Practice creating and configuring resources in Azure

---

## 🎯 Next Steps

1. ✅ Review any questions you got wrong
2. 📖 Study the corresponding Microsoft Learn modules
3. 🔄 Retake this practice test until you consistently score 90%+
4. 🧪 Complete hands-on labs in your own Azure subscription
5. 📝 Take the official Microsoft practice test
6. 📅 Schedule your AZ-104 exam when ready

---

<p align="right"><a href="../README.md">Back to Student Resources</a></p>
