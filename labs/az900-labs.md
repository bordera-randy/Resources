# 🔬 AZ-900 Hands-On Labs

<p align="right"><sub>Last updated: February 1, 2026</sub></p>

**Practical Azure Fundamentals Labs** — Get hands-on experience with core Azure services and concepts required for the AZ-900 exam.

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#lab1">Lab 1: Create a VM</a> •
  <a href="#lab2">Lab 2: Storage</a> •
  <a href="#lab3">Lab 3: Networking</a> •
  <a href="#lab4">Lab 4: App Service</a> •
  <a href="#lab5">Lab 5: Security</a> •
  <a href="#requirements">Requirements</a>
</p>

---

## 📋 Overview
<a id="overview"></a>

These labs provide hands-on experience with Azure fundamentals. Each lab should take 30-45 minutes to complete.

**Prerequisites:**
- Azure subscription (free tier available)
- Web browser
- Basic understanding of cloud computing concepts

**Lab Summary:**

| Lab | Topic | Time | Difficulty |
|-----|-------|------|-----------|
| Lab 1 | Create an Azure Virtual Machine | 30 min | Beginner |
| Lab 2 | Work with Azure Storage | 35 min | Beginner |
| Lab 3 | Explore Azure Networking | 40 min | Beginner |
| Lab 4 | Deploy an App Service | 35 min | Intermediate |
| Lab 5 | Implement Azure Security | 40 min | Intermediate |

---

## 🖥️ Lab 1: Create an Azure Virtual Machine
<a id="lab1"></a>

**Duration:** 30 minutes  
**Difficulty:** Beginner  
**Skills Covered:** VMs, Resource Groups, Regions, Compute

### Objectives
- Create a resource group
- Deploy a Windows VM
- Connect to the VM using RDP
- Verify the VM is running

### Prerequisites
- Azure subscription
- RDP client (Windows: built-in, Mac: Microsoft Remote Desktop app)

### Step 1: Create a Resource Group

1. Go to [Azure Portal](https://portal.azure.com)
2. Search for "Resource groups" in the search bar
3. Click **+ Create**
4. Fill in the details:
   - **Subscription:** Select your subscription
   - **Resource group name:** `rg-az900-lab`
   - **Region:** East US (or your preferred region)
5. Click **Review + create** → **Create**
6. Wait for the deployment to complete

### Step 2: Create a Virtual Machine

1. Search for "Virtual machines" in the portal
2. Click **+ Create** → **Azure virtual machine**
3. **Basics tab:**
   - **Resource group:** Select `rg-az900-lab`
   - **Virtual machine name:** `vm-az900-lab`
   - **Region:** East US (match resource group)
   - **Image:** Windows Server 2022 Datacenter
   - **Size:** Standard_B2s (or a free tier option if available)
   - **Username:** `azureuser`
   - **Password:** Create a strong password (remember it!)
4. Click **Next: Disks**
5. Leave defaults, click **Next: Networking**
6. **Networking tab:**
   - **Virtual network:** Keep default or create new
   - **Subnet:** Keep default
   - **Public IP:** Create new (should be set to auto)
   - **Allow public access:** Select RDP (3389)
7. Click **Review + create**
8. Review the settings and click **Create**
9. Wait for deployment (5-10 minutes)

### Step 3: Connect to the VM

1. Once deployed, go to the VM resource
2. Click **Connect** → **RDP**
3. Click **Download RDP file**
4. Open the RDP file
5. Enter your username (`azureuser`) and password
6. Accept the certificate warning
7. You should now be connected to the VM desktop

### Step 4: Verify VM Setup

1. Open a command prompt on the VM
2. Run `ipconfig` to see the network configuration
3. Notice the private IP address assigned to your VM
4. Take a screenshot for verification

### Step 5: Clean Up

1. Return to the Azure Portal
2. Go to the resource group `rg-az900-lab`
3. Click **Delete resource group**
4. Type the resource group name to confirm
5. Click **Delete**

### Key Takeaways
- ✅ You created an Azure resource group (logical container)
- ✅ You deployed a Windows VM with specific configuration
- ✅ You connected to the VM using RDP
- ✅ You learned how to clean up resources

---

## 💾 Lab 2: Work with Azure Storage
<a id="lab2"></a>

**Duration:** 35 minutes  
**Difficulty:** Beginner  
**Skills Covered:** Storage Accounts, Blob Storage, Access Tiers

### Objectives
- Create a storage account
- Create a blob container
- Upload and download files
- Explore access tiers

### Prerequisites
- Azure subscription
- A text file or image to upload (or create one)

### Step 1: Create a Storage Account

1. In the Azure Portal, search for "Storage accounts"
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** Create new: `rg-storage-lab`
   - **Storage account name:** `staz900lab<randomnumber>` (must be globally unique, lowercase)
   - **Region:** East US
   - **Performance:** Standard
   - **Redundancy:** Locally-redundant storage (LRS)
4. Click **Next: Advanced**
5. Leave defaults, click **Review + create**
6. Click **Create**
7. Wait for deployment (1-2 minutes)

### Step 2: Create a Blob Container

1. Go to the storage account resource
2. In the left menu, click **Containers** (under Data storage)
3. Click **+ Container**
4. **Name:** `myfiles`
5. **Public access level:** Container (allow public read)
6. Click **Create**

### Step 3: Upload a File

1. Click on the `myfiles` container
2. Click **Upload**
3. Select a file from your computer (or create a simple text file)
4. Click **Upload**
5. Wait for the upload to complete

### Step 4: Download the File

1. Click on the uploaded file
2. You'll see a **Download** button in the properties
3. Click the "..." menu and select **Download**
4. Verify the file downloads to your computer

### Step 5: Explore File Properties

1. Click on the file name
2. Observe the properties:
   - URL (this is the public access link)
   - Size
   - Last modified
   - Content type
3. Copy the URL and open it in a browser to verify public access works

### Step 6: Understand Access Tiers (Theory)

While in the storage account, explore these concepts:
- **Hot tier:** For frequent access (highest cost, lowest access time)
- **Cool tier:** For infrequent access (lower cost, higher access time)
- **Archive tier:** For rare access or compliance (lowest cost, highest access time)

### Step 7: Clean Up

1. Go to the resource group `rg-storage-lab`
2. Click **Delete resource group**
3. Confirm deletion

### Key Takeaways
- ✅ You created a storage account (unstructured data storage)
- ✅ You created a blob container (like a folder)
- ✅ You uploaded and downloaded files
- ✅ You learned about access tiers and public access

---

## 🌐 Lab 3: Explore Azure Networking
<a id="lab3"></a>

**Duration:** 40 minutes  
**Difficulty:** Beginner  
**Skills Covered:** VNets, Subnets, NSGs, Network Isolation

### Objectives
- Create a Virtual Network and subnets
- Create Network Security Groups
- Create and configure NSG rules
- Understand network isolation

### Prerequisites
- Azure subscription

### Step 1: Create a Virtual Network

1. Search for "Virtual networks" in the portal
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** Create new: `rg-network-lab`
   - **Name:** `vnet-az900`
   - **Region:** East US
4. Click **Next: IP Addresses**
5. **IP Addresses tab:**
   - **IPv4 address space:** Keep default or `10.0.0.0/16`
6. Click **+ Add subnet** to create a subnet:
   - **Subnet name:** `subnet-web`
   - **Subnet address range:** `10.0.1.0/24`
7. Click **Add**
8. Click **Review + create** → **Create**

### Step 2: Create Network Security Groups

1. Search for "Network security groups"
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** `rg-network-lab`
   - **Name:** `nsg-web`
   - **Region:** East US
4. Click **Review + create** → **Create**

### Step 3: Add NSG Rules

1. Go to the NSG resource
2. Click **Inbound security rules** in the left menu
3. Click **+ Add**
4. Create a rule to allow HTTP:
   - **Source:** Any
   - **Source port ranges:** *
   - **Destination:** Any
   - **Service:** HTTP
   - **Action:** Allow
   - **Priority:** 100
   - **Name:** `AllowHTTP`
5. Click **Add**

5. Repeat to add HTTPS rule:
   - **Service:** HTTPS
   - **Priority:** 110
   - **Name:** `AllowHTTPS`

6. Review the **Outbound security rules** (notice RDP/SSH are allowed by default)

### Step 4: Associate NSG with Subnet

1. Click **Subnets** in the NSG menu
2. Click **+ Associate**
3. Select:
   - **Virtual network:** `vnet-az900`
   - **Subnet:** `subnet-web`
4. Click **OK**

### Step 5: Understand Network Flow

1. Go back to your VNet resource
2. Click **Subnets** in the left menu
3. Click on `subnet-web`
4. Observe the associated NSG: `nsg-web`

### Step 6: Add Another Subnet

1. Click **Subnets** in the VNet menu
2. Click **+ Subnet**
3. Create a database subnet:
   - **Name:** `subnet-database`
   - **Address range:** `10.0.2.0/24`
4. Click **Save**

### Step 7: Clean Up

1. Go to resource group `rg-network-lab`
2. Click **Delete resource group**
3. Confirm deletion

### Key Takeaways
- ✅ You created a Virtual Network (VNet) with multiple subnets
- ✅ You created and configured Network Security Groups
- ✅ You learned how NSG rules filter traffic (inbound/outbound)
- ✅ You associated NSGs with subnets for network isolation

---

## 🌐 Lab 4: Deploy an App Service
<a id="lab4"></a>

**Duration:** 35 minutes  
**Difficulty:** Intermediate  
**Skills Covered:** PaaS, App Service, Deployment, Scaling

### Objectives
- Create an App Service plan
- Deploy a web application
- Access the deployed application
- Explore scaling options

### Prerequisites
- Azure subscription
- Web browser

### Step 1: Create an App Service Plan

1. Search for "App Services" in the portal
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** Create new: `rg-appservice-lab`
   - **Name:** `app-az900-<randomnumber>`
   - **Publish:** Code
   - **Runtime stack:** .NET 8 (or latest)
   - **Operating System:** Windows
4. Click **Next: Hosting**
5. **Hosting tab:**
   - **App Service Plan:** Create new plan
   - **Plan name:** `plan-az900`
   - **Sku and size:** Free tier (if available) or Basic
6. Click **Review + create** → **Create**
7. Wait for deployment (1-2 minutes)

### Step 2: Access the Deployed App

1. Go to the App Service resource
2. Click the **URL** (shown in the overview page)
3. You should see the default Azure App Service page
4. Copy and save this URL

### Step 3: Explore App Service Features

1. Go back to the App Service resource
2. In the left menu, explore:
   - **Deployment slots:** (for staging/production)
   - **Scale up (App Service plan):** View pricing tiers
   - **Scale out (App Service plan):** Manual vs auto-scaling
   - **Backup:** (available in paid tiers)

### Step 4: View Metrics

1. Click **Metrics** in the left menu
2. Select a metric (e.g., CPU Percentage, Memory Percentage)
3. View the last hour of data
4. Since it's a new app, metrics might show minimal data

### Step 5: Explore Deployment Options

1. Click **Deployment Center** in the left menu
2. Observe deployment options:
   - Local Git
   - GitHub
   - Azure DevOps
   - Bitbucket
3. (You don't need to set up deployment for this lab)

### Step 6: Clean Up

1. Go to resource group `rg-appservice-lab`
2. Click **Delete resource group**
3. Confirm deletion

### Key Takeaways
- ✅ You deployed a PaaS application (no VM management needed)
- ✅ You accessed the deployed application via a URL
- ✅ You explored scaling options for App Service
- ✅ You learned about deployment methods

---

## 🔐 Lab 5: Implement Azure Security
<a id="lab5"></a>

**Duration:** 40 minutes  
**Difficulty:** Intermediate  
**Skills Covered:** Identity, RBAC, Key Vault, Security Best Practices

### Objectives
- Create a Key Vault
- Store a secret
- Create a custom role (or assign built-in roles)
- Understand RBAC
- Explore security recommendations

### Prerequisites
- Azure subscription
- A user or service principal for role assignment

### Step 1: Create a Key Vault

1. Search for "Key Vaults" in the portal
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** Create new: `rg-security-lab`
   - **Key vault name:** `kv-az900-<randomnumber>` (must be unique)
   - **Region:** East US
   - **Pricing tier:** Standard
4. Click **Next: Access policy**
5. Leave defaults (you should have access), click **Review + create**
6. Click **Create**
7. Wait for deployment

### Step 2: Add a Secret

1. Go to the Key Vault resource
2. Click **Secrets** in the left menu
3. Click **+ Generate/Import**
4. Create a secret:
   - **Name:** `database-password`
   - **Value:** `MySecurePassword123!`
5. Click **Create**

### Step 3: Retrieve the Secret

1. Click on the `database-password` secret
2. Click the current version
3. Click **Show Secret Value**
4. Observe the secret is now visible
5. Note the secret identifier (URL)

### Step 4: Understand Access Policies

1. Go back to the Key Vault
2. Click **Access policies** in the left menu
3. Observe which users/identities have access
4. Note the permissions (Get, List, Set, Delete, etc.)

### Step 5: Create a Test User Assignment (Theory)

While you might not have permissions to add users in a free subscription, understand this process:

1. In **Access policies**, you would click **+ Create**
2. Select permissions (Get, List, Set, Delete)
3. Select a principal (user or service)
4. This grants role-based access to the vault

### Step 6: Explore Security Center Recommendations

1. Search for "Microsoft Defender for Cloud" in the portal
2. Click **Recommendations**
3. Review any recommendations for your subscription
4. This shows security best practices and compliance gaps

### Step 7: Enable Multi-Factor Authentication (Theory)

While you should have MFA enabled for your own account:
1. Search for "Multi-factor authentication"
2. Click **MFA settings**
3. Observe how to require MFA for users

### Step 8: Clean Up

1. Go to resource group `rg-security-lab`
2. Click **Delete resource group**
3. Confirm deletion

### Key Takeaways
- ✅ You created a Key Vault for secret management
- ✅ You stored and retrieved secrets securely
- ✅ You learned about access policies (RBAC for Key Vault)
- ✅ You explored security recommendations and best practices

---

## 📋 Requirements
<a id="requirements"></a>

### For All Labs

1. **Azure Subscription**
   - Free tier is sufficient for these labs
   - Sign up at [azure.microsoft.com](https://azure.microsoft.com/free/)
   - Get $200 in free credits for 30 days

2. **Web Browser**
   - Chrome, Edge, Firefox, or Safari
   - JavaScript enabled
   - Cookies enabled

3. **Internet Connection**
   - Stable connection required
   - ~10 Mbps recommended

### For Lab 1 (Virtual Machine)

- RDP client:
  - **Windows:** Built-in (mstsc.exe)
  - **Mac:** Microsoft Remote Desktop app (free from App Store)
  - **Linux:** Remmina or xfreerdp

### For Labs 2-5

- Only a web browser needed

---

## 💡 Lab Tips

1. **Start with Lab 1** — Provides foundational VM knowledge
2. **Use naming conventions** — Helps organize resources
3. **Clean up resources** — Delete resources after each lab to avoid charges
4. **Take screenshots** — Document your work for reference
5. **Read error messages** — They often indicate what went wrong
6. **Use free tier** — Most labs work with free tier resources
7. **Refer to Azure docs** — When stuck, search Microsoft Learn

---

## ❓ Troubleshooting

### "Deployment Failed" Error
- Check resource group region matches resource region
- Verify resource names are unique
- Check subscription quotas haven't been exceeded

### Can't Connect to VM (RDP)
- Verify NSG allows RDP (port 3389)
- Check VM is running (status shows "Running")
- Verify correct username and password

### Storage Upload Fails
- Check storage account isn't locked
- Verify you have write permissions
- Check file size (standard accounts have limits)

### App Service Won't Deploy
- Verify App Service plan tier is sufficient
- Check region availability
- Review deployment logs

---

## 🎯 Next Steps

After completing these labs:

1. **Review Lab Concepts** — Ensure you understand each service
2. **Take Practice Tests** — Use the AZ-900 practice test
3. **Study Weak Areas** — Review Microsoft Learn modules
4. **Create Personal Labs** — Combine services for real scenarios
5. **Schedule Exam** — Book your AZ-900 exam

---

## 📚 Additional Resources

- [Azure Free Account](https://azure.microsoft.com/en-us/free/)
- [Microsoft Learn - Azure Fundamentals](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals/)
- [Azure Documentation](https://learn.microsoft.com/en-us/azure/)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)

---

<p align="right"><a href="../README.md">Back to Student Resources</a></p>
