# 🔬 AZ-900 Hands-On Labs

**Last updated:** February 1, 2026

**Practical Azure Fundamentals Labs** — Get hands-on experience with core Azure services and concepts required for the AZ-900 exam.

**Quick Links:**
[Overview](#overview) •
[Lab 1](#lab1) •
[Lab 2](#lab2) •
[Lab 3](#lab3) •
[Lab 4](#lab4) •
[Lab 5](#lab5) •
[Lab 6](#lab6) •
[Lab 7](#lab7) •
[Lab 8](#lab8) •
[Lab 9](#lab9) •
[Lab 10](#lab10) •
[Requirements](#requirements)

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
| --- | --- | --- | --- |
| Lab 1 | Create an Azure Virtual Machine | 30 min | Beginner |
| Lab 2 | Work with Azure Storage | 35 min | Beginner |
| Lab 3 | Explore Azure Networking | 40 min | Beginner |
| Lab 4 | Deploy an App Service | 35 min | Intermediate |
| Lab 5 | Implement Azure Security | 40 min | Intermediate |
| Lab 6 | Azure SQL Database | 35 min | Intermediate |
| Lab 7 | Azure Monitor and Alerts | 40 min | Intermediate |
| Lab 8 | Azure Functions (Serverless) | 35 min | Intermediate |
| Lab 9 | Azure Cost Management | 30 min | Beginner |
| Lab 10 | Azure Governance and Policies | 40 min | Advanced |

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
6. Repeat to add HTTPS rule:
   - **Service:** HTTPS
   - **Priority:** 110
   - **Name:** `AllowHTTPS`
7. Review the **Outbound security rules** (notice RDP/SSH are allowed by default)

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

## 🗄️ Lab 6: Azure SQL Database

<a id="lab6"></a>

**Duration:** 35 minutes  
**Difficulty:** Intermediate  
**Skills Covered:** PaaS Database, SQL Server, Query Editor, Firewall Rules

### Objectives

- Create an Azure SQL Database
- Configure firewall rules
- Connect using Query Editor
- Run basic SQL queries
- Explore database metrics

### Prerequisites

- Azure subscription
- Basic SQL knowledge (optional but helpful)

### Step 1: Create an Azure SQL Database

1. Search for "SQL databases" in the portal
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** Create new: `rg-sqldb-lab`
   - **Database name:** `db-az900-demo`
   - **Server:** Click **Create new**
     - **Server name:** `sql-az900-<randomnumber>`
     - **Location:** East US
     - **Authentication method:** Use SQL authentication
     - **Server admin login:** `sqladmin`
     - **Password:** Create a strong password (remember it!)
     - Click **OK**
   - **Want to use SQL elastic pool:** No
   - **Compute + storage:** Click **Configure database**
     - Select **Basic** tier (cheapest option)
     - Click **Apply**
4. Click **Next: Networking**
5. **Networking tab:**
   - **Connectivity method:** Public endpoint
   - **Allow Azure services:** Yes
   - **Add current client IP address:** Yes
6. Click **Review + create** → **Create**
7. Wait for deployment (3-5 minutes)

### Step 2: Configure Firewall Rules

1. Go to the SQL server resource (not the database)
2. Click **Networking** in the left menu
3. Verify your client IP is listed
4. If not, click **Add your client IPv4 address**
5. Click **Save**

### Step 3: Connect Using Query Editor

1. Go to the SQL database resource `db-az900-demo`
2. Click **Query editor** in the left menu
3. Login with:
   - **Authorization type:** SQL server authentication
   - **Login:** `sqladmin`
   - **Password:** Your password
4. Click **OK**

### Step 4: Create a Sample Table

1. In the query editor, paste this SQL:

   ```sql
   CREATE TABLE Products (
       ProductID INT PRIMARY KEY,
       ProductName VARCHAR(50),
       Price DECIMAL(10,2)
   );
   ```

2. Click **Run**
3. You should see "Query succeeded"

### Step 5: Insert Sample Data

1. Paste this SQL:

   ```sql
   INSERT INTO Products (ProductID, ProductName, Price)
   VALUES 
       (1, 'Laptop', 999.99),
       (2, 'Mouse', 29.99),
       (3, 'Keyboard', 79.99);
   ```

2. Click **Run**

### Step 6: Query the Data

1. Paste this SQL:

   ```sql
   SELECT * FROM Products;
   ```

2. Click **Run**
3. You should see the three products displayed

### Step 7: Explore Database Metrics

1. Go back to the database overview
2. Click **Metrics** in the left menu
3. Add metrics:
   - DTU percentage
   - Storage percentage
   - CPU percentage
4. View the graphs

### Step 8: Clean Up

1. Go to resource group `rg-sqldb-lab`
2. Click **Delete resource group**
3. Confirm deletion

### Key Takeaways

- ✅ You created an Azure SQL Database (PaaS)
- ✅ You configured firewall rules for access
- ✅ You used Query Editor to run SQL commands
- ✅ You explored database monitoring metrics

---

## 📊 Lab 7: Azure Monitor and Alerts

<a id="lab7"></a>

**Duration:** 40 minutes  
**Difficulty:** Intermediate  
**Skills Covered:** Monitoring, Metrics, Alerts, Log Analytics

### Objectives

- Enable monitoring for a resource
- Create custom metrics
- Configure alerts
- View activity logs
- Understand diagnostic settings

### Prerequisites

- Azure subscription
- Existing resource (or create a storage account for this lab)

### Step 1: Create a Storage Account to Monitor

1. Search for "Storage accounts" in the portal
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** Create new: `rg-monitor-lab`
   - **Storage account name:** `stmonitor<randomnumber>`
   - **Region:** East US
   - **Performance:** Standard
   - **Redundancy:** LRS
4. Click **Review + create** → **Create**

### Step 2: Explore Metrics

1. Go to the storage account resource
2. Click **Metrics** in the left menu
3. Click **Add metric**
4. Select:
   - **Scope:** Your storage account
   - **Metric Namespace:** Account
   - **Metric:** Transactions
   - **Aggregation:** Count
5. Click **Apply**
6. View the metric graph

### Step 3: Create an Alert Rule

1. Click **Alerts** in the left menu
2. Click **+ Create** → **Alert rule**
3. **Scope:** Already selected (your storage account)
4. Click **Next: Condition**
5. Click **Add condition**
6. Search for "Transactions" and select it
7. Configure the condition:
   - **Threshold value:** 100
   - **Aggregation type:** Total
   - **Check every:** 5 minutes
8. Click **Next: Actions**
9. Click **Create action group**
10. **Basics tab:**
    - **Action group name:** `ag-storage-alerts`
    - **Display name:** `StorageAlerts`
11. Click **Next: Notifications**
12. Add notification:
    - **Notification type:** Email/SMS/Push/Voice
    - **Name:** `EmailAdmin`
    - **Email:** Your email address
13. Click **Review + create** → **Create**
14. Click **Next: Details**
15. **Alert rule name:** `alert-high-transactions`
16. Click **Review + create** → **Create**

### Step 4: View Activity Log

1. Go to the storage account
2. Click **Activity log** in the left menu
3. View recent operations (creation, updates, etc.)
4. Click on any activity to see details
5. Notice the JSON representation

### Step 5: Enable Diagnostic Settings

1. Click **Diagnostic settings** in the left menu
2. Click **+ Add diagnostic setting**
3. **Diagnostic setting name:** `diag-storage-logs`
4. Select log categories:
   - StorageRead
   - StorageWrite
   - StorageDelete
5. **Destination details:**
   - Select **Send to Log Analytics workspace**
   - Create new workspace if needed
6. Click **Save**

### Step 6: Create a Sample Log Query (Optional)

1. Search for "Log Analytics workspaces"
2. Click on your workspace
3. Click **Logs** in the left menu
4. Try a sample query:

   ```kusto
   AzureActivity
   | where TimeGenerated > ago(24h)
   | summarize count() by OperationName
   | order by count_ desc
   ```

5. Click **Run**

### Step 7: Clean Up

1. Go to resource group `rg-monitor-lab`
2. Click **Delete resource group**
3. Confirm deletion

### Key Takeaways

- ✅ You explored Azure metrics and monitoring
- ✅ You created alert rules for resource monitoring
- ✅ You configured action groups for notifications
- ✅ You explored activity logs and diagnostic settings

---

## ⚡ Lab 8: Azure Functions (Serverless)

<a id="lab8"></a>

**Duration:** 35 minutes  
**Difficulty:** Intermediate  
**Skills Covered:** Serverless Computing, Function Apps, HTTP Triggers, Consumption Plan

### Objectives

- Create an Azure Function App
- Create an HTTP-triggered function
- Test the function
- View function logs
- Understand serverless benefits

### Prerequisites

- Azure subscription
- Web browser

### Step 1: Create a Function App

1. Search for "Function App" in the portal
2. Click **+ Create**
3. **Basics tab:**
   - **Resource group:** Create new: `rg-functions-lab`
   - **Function App name:** `func-az900-<randomnumber>`
   - **Publish:** Code
   - **Runtime stack:** .NET
   - **Version:** 8 (or latest)
   - **Region:** East US
   - **Operating System:** Windows
   - **Plan type:** Consumption (Serverless)
4. Click **Next: Storage**
5. **Storage account:** Create new or use existing
6. Click **Review + create** → **Create**
7. Wait for deployment (2-3 minutes)

### Step 2: Create an HTTP Trigger Function

1. Go to the Function App resource
2. Click **Functions** in the left menu
3. Click **+ Create**
4. **Development environment:** Develop in portal
5. **Template:** HTTP trigger
6. **New Function:** Name it `HttpExample`
7. **Authorization level:** Anonymous (for testing)
8. Click **Create**

### Step 3: Test the Function

1. Click on the `HttpExample` function
2. Click **Code + Test** in the left menu
3. You'll see the default function code
4. Click **Test/Run** at the top
5. In the **Input** tab:
   - **HTTP method:** GET
   - **Query:** Add parameter `name` with value `Azure`
6. Click **Run**
7. View the output in the **Output** tab
8. You should see: "Hello, Azure"

### Step 4: Get the Function URL

1. Click **Get Function Url** at the top
2. Copy the URL
3. Open a new browser tab
4. Paste the URL and add `?name=YourName` at the end
5. Press Enter
6. You should see the response in the browser

### Step 5: Modify the Function Code

1. Go back to **Code + Test**
2. Modify the code to return JSON:

   ```csharp
   #r "Newtonsoft.Json"
   
   using System.Net;
   using Microsoft.AspNetCore.Mvc;
   using Microsoft.Extensions.Primitives;
   using Newtonsoft.Json;
   
   public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
   {
       log.LogInformation("C# HTTP trigger function processed a request.");
   
       string name = req.Query["name"];
   
       string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
       dynamic data = JsonConvert.DeserializeObject(requestBody);
       name = name ?? data?.name;
   
       var response = new {
           message = $"Hello, {name ?? "Guest"}!",
           timestamp = DateTime.UtcNow
       };
   
       return new OkObjectResult(response);
   }
   ```

3. Click **Save**
4. Test again using the Test/Run feature

### Step 6: View Logs and Metrics

1. Click **Monitor** in the left menu
2. View invocation logs
3. Click **Metrics** in the Function App menu
4. Add metric:
   - **Metric:** Function Execution Count
5. View the graph

### Step 7: Explore Function App Settings

1. Go to the Function App overview
2. Explore:
   - **Configuration:** Application settings
   - **Networking:** Outbound/Inbound rules
   - **Scale out:** Consumption plan auto-scales
   - **Deployment slots:** For staging (premium plans)

### Step 8: Clean Up

1. Go to resource group `rg-functions-lab`
2. Click **Delete resource group**
3. Confirm deletion

### Key Takeaways

- ✅ You created a serverless Function App
- ✅ You deployed an HTTP-triggered function
- ✅ You tested and modified function code
- ✅ You learned about consumption-based pricing

---

## 💰 Lab 9: Azure Cost Management

<a id="lab9"></a>

**Duration:** 30 minutes  
**Difficulty:** Beginner  
**Skills Covered:** Cost Analysis, Budgets, Cost Alerts, Pricing Calculator

### Objectives

- Analyze current costs
- Create a budget
- Set up cost alerts
- Use the pricing calculator
- Understand cost optimization

### Prerequisites

- Azure subscription
- Some existing resources (or use previous lab resources)

### Step 1: Access Cost Management

1. Search for "Cost Management + Billing" in the portal
2. Click on your subscription
3. Click **Cost analysis** in the left menu
4. View your current costs

### Step 2: Explore Cost Analysis

1. In Cost analysis, view:
   - **Accumulated costs:** Total spending
   - **Daily costs:** Day-by-day breakdown
   - **Forecast:** Projected spending
2. Change the view to:
   - **Group by:** Resource group
   - **Group by:** Service name
   - **Group by:** Location
3. Observe how costs are distributed

### Step 3: Create a Budget

1. Click **Budgets** in the left menu
2. Click **+ Add**
3. Configure budget:
   - **Name:** `monthly-budget-100`
   - **Reset period:** Monthly
   - **Budget amount:** $100
   - **Start date:** First day of current month
4. Click **Next**
5. **Alert conditions:**
   - Add alert at 80% of budget
   - Add alert at 100% of budget
6. **Alert recipients:**
   - Add your email address
7. Click **Create**

### Step 4: Set Up a Cost Alert

1. Stay in **Budgets**
2. Click on your created budget
3. Click **Edit**
4. Add another alert condition:
   - **Type:** Forecasted
   - **Threshold:** 90%
5. Click **Save**

### Step 5: Use the Pricing Calculator

1. Open a new browser tab
2. Go to [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
3. Add products:
   - Search for "Virtual Machines"
   - Select a VM size (e.g., B2s)
   - Configure:
     - Region: East US
     - OS: Windows
     - Hours: 730 (full month)
   - View estimated cost
4. Add another product:
   - Search for "Storage Accounts"
   - Configure storage needs
   - View estimated cost
5. Save or export the estimate

### Step 6: Explore Cost Optimization Recommendations

1. Go back to Cost Management
2. Click **Advisor recommendations**
3. View recommendations:
   - Resize or shutdown underutilized VMs
   - Delete unused resources
   - Use reserved instances
   - Change storage tiers
4. Review potential savings

### Step 7: Understand Tags for Cost Tracking

1. Go to any resource (e.g., a storage account)
2. Click **Tags** in the left menu
3. Add tags:
   - **Name:** `Environment` **Value:** `Dev`
   - **Name:** `CostCenter` **Value:** `IT`
   - **Name:** `Project` **Value:** `AZ900-Lab`
4. Click **Save**
5. Go back to Cost analysis
6. **Group by:** Tag
7. Select your tag name to filter costs

### Step 8: Review Cost Management Best Practices

Key strategies to reduce costs:

- Use **Azure Hybrid Benefit** for Windows licenses
- Purchase **Reserved Instances** for long-term workloads
- Use **Auto-shutdown** for dev/test VMs
- Implement **right-sizing** for VMs
- Delete **unused resources** regularly
- Use **cost-effective regions**
- Leverage **Azure DevTest subscriptions**

### Key Takeaways

- ✅ You analyzed your Azure spending
- ✅ You created budgets and cost alerts
- ✅ You used the pricing calculator for estimates
- ✅ You learned cost optimization strategies

---

## 🛡️ Lab 10: Azure Governance and Policies

<a id="lab10"></a>

**Duration:** 40 minutes  
**Difficulty:** Advanced  
**Skills Covered:** Azure Policy, Blueprints, Management Groups, Resource Locks, Compliance

### Objectives

- Create an Azure Policy
- Apply a policy to a resource group
- Test policy enforcement
- Create a resource lock
- Understand compliance reporting

### Prerequisites

- Azure subscription
- Owner or Contributor role at subscription level

### Step 1: Create a Resource Group

1. Search for "Resource groups" in the portal
2. Click **+ Create**
3. **Basics:**
   - **Resource group name:** `rg-governance-lab`
   - **Region:** East US
4. Click **Review + create** → **Create**

### Step 2: Explore Built-in Policies

1. Search for "Policy" in the portal
2. Click **Definitions** in the left menu
3. Browse built-in policies:
   - Filter by **Category:** Tags
   - Search for "Require a tag on resources"
4. Click on the policy to view details

### Step 3: Assign a Policy

1. Click **Assignments** in the left menu
2. Click **+ Assign policy**
3. **Basics:**
   - **Scope:** Select your subscription
   - Click **Select resource group** → Choose `rg-governance-lab`
   - **Policy definition:** Click **...**
     - Search for "Require a tag on resources"
     - Select the policy
     - Click **Select**
4. Click **Next**
5. **Parameters:**
   - **Tag Name:** `Environment`
6. Click **Next: Remediation**
7. Leave defaults
8. Click **Review + create** → **Create**

### Step 4: Test Policy Enforcement

1. Try to create a storage account in `rg-governance-lab`
2. Search for "Storage accounts"
3. Click **+ Create**
4. **Basics:**
   - **Resource group:** `rg-governance-lab`
   - **Storage account name:** `stpolicytest<randomnumber>`
5. Click **Review + create**
6. You should see a validation error about the missing tag
7. Cancel the creation

### Step 5: Create a Resource with the Required Tag

1. Try again to create the storage account
2. Before clicking Review + create, click **Next: Advanced**
3. Click **Next: Networking**
4. Click **Next: Data protection**
5. Click **Next: Encryption**
6. Click **Next: Tags**
7. Add tag:
   - **Name:** `Environment`
   - **Value:** `Dev`
8. Click **Review + create** → **Create**
9. This time it should succeed

### Step 6: Create a Resource Lock

1. Go to the storage account you just created
2. Click **Locks** in the left menu
3. Click **+ Add**
4. **Lock name:** `prevent-delete`
5. **Lock type:** Delete
6. **Notes:** "Prevent accidental deletion"
7. Click **OK**

### Step 7: Test the Resource Lock

1. Try to delete the storage account
2. Click **Delete** at the top
3. You should see an error message about the lock
4. Cancel the deletion

### Step 8: View Compliance Report

1. Go back to **Policy**
2. Click **Compliance** in the left menu
3. View compliance state:
   - Overall compliance percentage
   - Compliant vs non-compliant resources
4. Click on your policy assignment
5. View detailed compliance information

### Step 9: Create a Custom Policy (Theory)

While you may not have permissions to create custom policies, understand the process:

1. In **Policy**, click **Definitions**
2. Click **+ Policy definition**
3. You would define:
   - Policy rules (JSON format)
   - Parameters
   - Effect (Deny, Audit, Append, etc.)
4. Example policy rule to deny public storage accounts:

   ```json
   {
     "if": {
       "allOf": [
         {
           "field": "type",
           "equals": "Microsoft.Storage/storageAccounts"
         },
         {
           "field": "Microsoft.Storage/storageAccounts/networkAcls.defaultAction",
           "notEquals": "Deny"
         }
       ]
     },
     "then": {
       "effect": "deny"
     }
   }
   ```

### Step 10: Understand Management Groups (Theory)

Management groups provide governance hierarchy:

- **Structure:** Subscription → Management Group → Root Management Group
- **Benefits:**
  - Apply policies across multiple subscriptions
  - Organize subscriptions by department/project
  - Inherit policies and RBAC from parent groups

### Step 11: Clean Up

1. Remove the resource lock:
   - Go to storage account → Locks
   - Click the lock → Delete
2. Remove the policy assignment:
   - Go to Policy → Assignments
   - Click your assignment → Delete
3. Delete the resource group:
   - Go to `rg-governance-lab`
   - Click **Delete resource group**
   - Confirm deletion

### Key Takeaways

- ✅ You created and assigned Azure Policies
- ✅ You tested policy enforcement
- ✅ You created resource locks to prevent deletion
- ✅ You viewed compliance reports
- ✅ You learned about governance best practices

---

## 📋 Requirements

<a id="requirements"></a>

### For All Labs

1. **Azure Subscription**
   - Free tier is sufficient for these labs
   - Sign up at [Azure Free Account](https://azure.microsoft.com/free/)
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

### For Labs 2-10

- Only a web browser needed

---

## 💡 Lab Tips

1. **Start with Lab 1** — Provides foundational VM knowledge
2. **Follow the sequence** — Labs build on each other conceptually
3. **Use naming conventions** — Helps organize resources (e.g., `rg-<purpose>-lab`)
4. **Clean up resources** — Delete resources after each lab to avoid charges
5. **Take screenshots** — Document your work for reference
6. **Read error messages** — They often indicate what went wrong
7. **Use free tier** — Most labs work with free tier resources
8. **Refer to Azure docs** — When stuck, search Microsoft Learn
9. **Practice multiple times** — Repetition builds confidence
10. **Combine labs** — Create scenarios that use multiple services together

---

## ❓ Troubleshooting

### "Deployment Failed" Error

- Check resource group region matches resource region
- Verify resource names are unique (globally unique for some services)
- Check subscription quotas haven't been exceeded
- Review the error details in the notification panel

### Can't Connect to VM (RDP)

- Verify NSG allows RDP (port 3389)
- Check VM is running (status shows "Running")
- Verify correct username and password
- Ensure your public IP is allowed in firewall rules

### Storage Upload Fails

- Check storage account isn't locked
- Verify you have write permissions
- Check file size (standard accounts have limits)
- Ensure storage account is not soft-deleted

### App Service Won't Deploy

- Verify App Service plan tier is sufficient
- Check region availability for the chosen runtime
- Review deployment logs in Deployment Center
- Check for naming conflicts

### SQL Database Connection Issues

- Verify firewall rules include your client IP
- Check server name is correct (include `.database.windows.net`)
- Verify authentication credentials
- Ensure "Allow Azure services" is enabled

### Policy Not Enforcing

- Check policy scope includes the resource
- Verify policy effect is "Deny" not "Audit"
- Allow 5-10 minutes for policy to take effect
- Check for policy exemptions

### Cost Management Not Showing Data

- Wait 24-48 hours for initial cost data
- Verify you have cost management reader role
- Check subscription is active and not expired
- Some free tier usage may not show costs

---

## 🎯 Next Steps

After completing these labs:

1. **Review Lab Concepts** — Ensure you understand each service and its purpose
2. **Take Practice Tests** — Use official AZ-900 practice tests
3. **Study Weak Areas** — Review Microsoft Learn modules for topics you found challenging
4. **Create Personal Labs** — Combine services for real-world scenarios
5. **Explore Advanced Labs** — Try AZ-104 or AZ-305 labs for deeper knowledge
6. **Join Azure Community** — Participate in forums and Q&A sites
7. **Schedule Exam** — Book your AZ-900 exam when ready
8. **Keep Learning** — Azure updates constantly; stay current with new features

---

## 📚 Additional Resources

- [Azure Free Account](https://azure.microsoft.com/en-us/free/)
- [Microsoft Learn - Azure Fundamentals](https://learn.microsoft.com/en-us/training/paths/azure-fundamentals/)
- [Azure Documentation](https://learn.microsoft.com/en-us/azure/)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- [Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/)
- [Azure Updates](https://azure.microsoft.com/en-us/updates/)
- [Azure Blog](https://azure.microsoft.com/en-us/blog/)

---

**Back to:** [Student Resources](../README.md)

