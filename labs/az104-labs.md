# 🧪 AZ-104 Hands-On Labs

**Azure Administrator Practical Experience**

---

## Table of Contents

1. [Lab 1: Identity & Access Management](#lab-1-identity--access-management)
2. [Lab 2: Azure Storage & Backups](#lab-2-azure-storage--backups)
3. [Lab 3: Virtual Machines & Scaling](#lab-3-virtual-machines--scaling)
4. [Lab 4: Networking & Load Balancing](#lab-4-networking--load-balancing)
5. [Lab 5: Monitoring & Compliance](#lab-5-monitoring--compliance)

---

## Lab 1: Identity & Access Management

**Objective:** Configure Azure AD users, groups, and role-based access control (RBAC)

**Estimated Duration:** 45 minutes

**Prerequisites:**
- Azure subscription with Owner or User Access Administrator role
- Access to Azure Portal

### Step-by-Step Instructions

#### Task 1: Create Users and Groups in Azure AD

1. Navigate to **Azure Active Directory** > **Users**
2. Click **New User**
3. Create a new user with:
   - User principal name: `appdev@yourdomain.onmicrosoft.com`
   - Name: App Developer
   - Password: Generate (save temporarily)
4. Repeat to create another user: `storageadmin@yourdomain.onmicrosoft.com` (Storage Administrator)
5. Navigate to **Azure AD** > **Groups**
6. Click **New Group**
7. Create group "Developers":
   - Group type: Security
   - Add appdev user as member
8. Create group "Storage Admins":
   - Group type: Security
   - Add storageadmin user as member

#### Task 2: Implement RBAC

1. In your Azure subscription, go to **Access control (IAM)**
2. Click **Add** > **Add role assignment**
3. Assign "Contributor" role to "Developers" group
4. Click **Add** > **Add role assignment** again
5. Assign "Storage Account Contributor" role to "Storage Admins" group
6. Verify assignments in the **Role assignments** tab

#### Task 3: Test Role Assignments

1. Navigate to a storage account (create one if needed)
2. Go to **Access control (IAM)**
3. Verify the "Storage Admins" group has appropriate permissions
4. Note what each group can and cannot do based on their assigned roles

**Key Takeaways:**
- Azure AD is the identity provider for Azure resources
- RBAC provides fine-grained access control using built-in and custom roles
- Groups allow you to manage permissions for multiple users simultaneously
- Least privilege principle: assign only necessary permissions

**Troubleshooting:**
- **Issue:** User not appearing in Azure AD
  - **Solution:** Ensure the user has an Azure AD license and check that you're in the correct directory

- **Issue:** Role assignment not working
  - **Solution:** Wait 5-10 minutes for permissions to propagate, then refresh the browser

### Cleanup

1. Delete the created users and groups from Azure AD
2. Remove role assignments from the Resource Group or Subscription

---

## Lab 2: Azure Storage & Backups

**Objective:** Create and manage storage accounts, configure backup and disaster recovery

**Estimated Duration:** 50 minutes

**Prerequisites:**
- Azure subscription with contributor access
- Lab 1 completed (optional, for testing access)

### Step-by-Step Instructions

#### Task 1: Create and Configure Storage Account

1. Navigate to **Storage accounts** in Azure Portal
2. Click **Create**
3. Configure with:
   - Resource Group: Create new "az104-storage-lab"
   - Storage account name: `sa104lab[randomnumber]` (must be globally unique)
   - Region: East US
   - Performance: Standard
   - Redundancy: Geo-redundant storage (GRS)
4. Click **Review + create**, then **Create**
5. Once deployed, click **Go to resource**

#### Task 2: Create Blob Containers and Upload Data

1. In the storage account, go to **Containers** (under Data storage)
2. Click **+ Container**
3. Create container "backup-data"
4. Create another container "logs"
5. Click on "backup-data" container
6. Click **Upload**
7. Select any local file to upload (or create a test file)
8. Verify the file appears in the container

#### Task 3: Configure Storage Account Firewall

1. In storage account, go to **Networking** (under Security + networking)
2. Set firewall to **Enabled from selected virtual networks and IP addresses**
3. Add your current IP address under **Firewall** section
4. Click **Save**
5. Verify you can still access the storage account from your current location

#### Task 4: Enable Soft Delete for Blobs

1. In storage account, go to **Data protection** (under Data management)
2. Enable **Soft delete for blobs**: ON
3. Set retention days to 7
4. Enable **Soft delete for containers**: ON
5. Click **Save**
6. This allows recovery of deleted data within the retention period

#### Task 5: Create Backup

1. Navigate to **Backup center** in Azure Portal
2. Click **+ Backup**
3. Select Datasource type: **Azure Blobs**
4. Select your storage account
5. Choose vault: **Create new**
6. Configure:
   - Vault name: `vault-az104-lab`
   - Resource group: Use same as storage account
7. Complete backup configuration

**Key Takeaways:**
- Storage account replication options (LRS, GRS, RA-GRS) affect cost and availability
- Firewall rules restrict access to authorized networks/IPs
- Soft delete provides data protection without permanent deletion
- Backup center centralizes backup management across Azure resources

**Troubleshooting:**
- **Issue:** "Storage account name already exists"
  - **Solution:** Storage account names must be globally unique; add more random characters

- **Issue:** Cannot upload files to container
  - **Solution:** Check firewall rules; your IP might be blocked

### Cleanup

1. Delete the backup vault
2. Delete the storage account
3. Delete the resource group "az104-storage-lab"

---

## Lab 3: Virtual Machines & Scaling

**Objective:** Create VMs, configure auto-scaling, and implement load balancing

**Estimated Duration:** 55 minutes

**Prerequisites:**
- Azure subscription with contributor access
- Familiarity with networking concepts

### Step-by-Step Instructions

#### Task 1: Create Virtual Machines

1. Navigate to **Virtual machines** in Azure Portal
2. Click **Create** > **Virtual machine**
3. Configure:
   - Resource Group: Create new "az104-vm-lab"
   - VM name: `vm-lab-01`
   - Region: East US
   - Image: Windows Server 2022 Datacenter
   - Size: Standard_B2s
   - Username: azureuser
   - Password: Create strong password (save for later)
   - Public inbound ports: Allow RDP (3389)
4. Click **Next: Disks**
5. Review OS disk settings (keep defaults)
6. Click **Next: Networking**
7. Create new Virtual Network: `vnet-lab`
8. Create new Subnet: `subnet-lab`
9. Click **Review + create**, then **Create**
10. Wait for deployment to complete

#### Task 2: Create Additional VMs for Load Balancing

1. Repeat Task 1 to create second VM:
   - VM name: `vm-lab-02`
   - Use same Resource Group and Virtual Network
2. Repeat once more for third VM:
   - VM name: `vm-lab-03`

#### Task 3: Create Load Balancer

1. Navigate to **Load Balancers** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az104-vm-lab
   - Name: `lb-lab`
   - Type: Public
   - SKU: Standard
   - Region: East US
4. Click **Next: Frontend IP configuration**
5. Click **Add a frontend IP configuration**
6. Create: `frontend-ip`
7. Click **Next: Backend pools**
8. Click **Add a backend pool**
9. Name: `backend-pool`
10. Associated to: Virtual network (vnet-lab)
11. Click **+ Add target** and select all three VMs
12. Click **Next: Inbound rules**
13. Click **Add a load balancing rule**
14. Configure:
    - Name: `http-rule`
    - Protocol: TCP
    - Port: 80
    - Backend port: 80
    - Backend pool: backend-pool
15. Click **Review + create**, then **Create**

#### Task 4: Configure Virtual Machine Scale Set (Alternative to Manual Scaling)

1. Navigate to **Virtual Machine Scale Sets**
2. Click **Create**
3. Configure:
   - Resource Group: az104-vm-lab
   - Name: `vmss-lab`
   - Region: East US
   - Image: Windows Server 2022 Datacenter
   - Size: Standard_B2s
   - Username: azureuser
   - Password: (create new)
4. Click **Next: Networking**
5. Create new VNet or use existing vnet-lab
6. Click **Next: Management**
7. Enable autoscaling: **Yes**
8. Configure autoscaling:
    - Min instances: 2
    - Max instances: 5
    - Default instances: 2
9. Add scale rule: Scale out when CPU > 75%
10. Click **Review + create**, then **Create**

**Key Takeaways:**
- Virtual Machine Scale Sets automatically scale based on metrics
- Load Balancers distribute traffic across multiple VMs
- Backend pools group VMs for load balancing
- Inbound rules define how traffic reaches your VMs
- Health probes detect unhealthy instances automatically

**Troubleshooting:**
- **Issue:** Cannot connect to VM via RDP
  - **Solution:** Verify Network Security Group allows RDP (port 3389), check firewall rules

- **Issue:** Load Balancer shows unhealthy backends
  - **Solution:** Check if VMs are running and health probe port is accessible

### Cleanup

1. Delete the Virtual Machine Scale Set
2. Delete all Virtual Machines
3. Delete the Load Balancer
4. Delete the Virtual Network
5. Delete the resource group "az104-vm-lab"

---

## Lab 4: Networking & Load Balancing

**Objective:** Configure advanced networking with multiple subnets, NSGs, and traffic management

**Estimated Duration:** 50 minutes

**Prerequisites:**
- Azure subscription with contributor access
- Lab 3 completed (recommended for understanding VMs)

### Step-by-Step Instructions

#### Task 1: Create Advanced Virtual Network Architecture

1. Navigate to **Virtual networks** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az104-network-lab"
   - Name: `vnet-advanced`
   - Region: East US
   - IPv4 address space: 10.0.0.0/16
4. Click **Next: Subnets**
5. Create multiple subnets:
   - Subnet 1: `subnet-web` (10.0.1.0/24)
   - Subnet 2: `subnet-app` (10.0.2.0/24)
   - Subnet 3: `subnet-db` (10.0.3.0/24)
6. Click **Review + create**, then **Create**

#### Task 2: Create and Configure Network Security Groups

1. Navigate to **Network security groups** in Azure Portal
2. Click **Create**
3. Create first NSG: `nsg-web`
   - Resource Group: az104-network-lab
4. After creation, click on `nsg-web`
5. Go to **Inbound security rules**
6. Click **+ Add** and configure:
   - Source: Any
   - Source port ranges: *
   - Destination: Any
   - Destination port ranges: 80,443
   - Protocol: TCP
   - Action: Allow
   - Priority: 100
   - Name: `allow-http-https`
7. Click **Add**
8. Repeat to create `nsg-app` and `nsg-db`:
   - nsg-app: Allow traffic on port 8080 from vnet-web subnet
   - nsg-db: Allow port 3306 from vnet-app subnet only

#### Task 3: Associate NSGs with Subnets

1. Navigate to **Virtual networks** > `vnet-advanced`
2. Go to **Subnets**
3. Click `subnet-web`
4. Set Network security group to `nsg-web`
5. Click **Save**
6. Repeat for `subnet-app` (associate `nsg-app`)
7. Repeat for `subnet-db` (associate `nsg-db`)

#### Task 4: Create and Test Application Gateway

1. Navigate to **Application Gateways** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az104-network-lab
   - Name: `appgw-lab`
   - Region: East US
   - Virtual network: `vnet-advanced`
   - Subnet: Create new `subnet-gateway` (10.0.0.0/24)
4. Click **Next: Frontends**
5. Add public IP configuration (create new `appgw-ip`)
6. Click **Next: Backends**
7. Add backend pool and configure targets
8. Click **Next: Configuration**
9. Add routing rule:
    - Listener name: `http-listener`
    - Frontend IP: Public
    - Protocol: HTTP
    - Port: 80
    - Backend target: backend-pool
10. Click **Review + create**, then **Create**

#### Task 5: Configure User Defined Routes (UDR)

1. Navigate to **Route tables** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az104-network-lab
   - Name: `udr-lab`
   - Region: East US
4. After creation, click on `udr-lab`
5. Go to **Routes**
6. Click **+ Add**
7. Create route:
    - Route name: `route-to-firewall`
    - Address prefix: 192.168.0.0/16
    - Next hop type: Virtual appliance
    - Next hop address: 10.0.0.254
8. Click **Add**
9. Go back to route table > **Subnets**
10. Click **Associate**
11. Select `vnet-advanced` and `subnet-app`

**Key Takeaways:**
- Network Security Groups control traffic at the subnet/NIC level
- Application Gateway provides Layer 7 (application) load balancing
- User Defined Routes override default Azure routing behavior
- Subnet design follows security layering (web → app → db)
- Network segmentation provides defense-in-depth security

**Troubleshooting:**
- **Issue:** Cannot communicate between subnets
  - **Solution:** Verify NSG rules allow traffic; check route tables for custom routes blocking traffic

- **Issue:** Application Gateway shows unhealthy backends
  - **Solution:** Ensure backend VMs are running and health probe port responds correctly

### Cleanup

1. Delete Application Gateway
2. Delete Route tables
3. Delete Network Security Groups
4. Delete Virtual Network
5. Delete the resource group "az104-network-lab"

---

## Lab 5: Monitoring & Compliance

**Objective:** Configure Azure Monitor, create alerts, and implement compliance solutions

**Estimated Duration:** 45 minutes

**Prerequisites:**
- Azure subscription with contributor access
- Lab 3 completed (VMs for monitoring)

### Step-by-Step Instructions

#### Task 1: Create and Configure Log Analytics Workspace

1. Navigate to **Log Analytics workspaces** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az104-monitoring-lab"
   - Name: `law-az104-lab`
   - Region: East US
4. Click **Review + create**, then **Create**
5. Once deployed, click **Go to resource**

#### Task 2: Enable Azure Monitor on Virtual Machines

1. Navigate to **Virtual machines** (or create a new test VM)
2. Select a VM to monitor
3. Go to **Extensions + applications**
4. Click **Add**
5. Search for and select **Azure Monitor Agent**
6. Click **Create**
7. Configure:
   - Create new data collection rule: `dcr-lab`
   - Destination: Log Analytics workspace (law-az104-lab)
8. Click **Create and assign**
9. Wait for extension to install

#### Task 3: Create Custom Alerts

1. Navigate to **Monitor** > **Alerts**
2. Click **+ Create alert rule**
3. Select resource (VM from Task 2)
4. Click **Condition**
5. Select signal: **Percentage CPU**
6. Configure:
    - Operator: Greater than
    - Threshold value: 75
    - Aggregation granularity: 5 minutes
    - Check every: 1 minute
7. Click **Next**
8. Click **+ Create action group**
9. Configure:
    - Action group name: `ag-cpu-alerts`
    - Short name: `cpualerts`
10. Click **Notifications**
11. Select **Email/SMS/Push/Voice**
12. Add your email address
13. Click **OK** > **Review + create** > **Create**

#### Task 4: Create Log Analytics Queries

1. Go to **Log Analytics workspace** > `law-az104-lab`
2. Click **Logs**
3. Click **+ New Query**
4. Run predefined queries:

**Query 1: CPU Usage Over Time**
```kusto
Perf
| where ObjectName == "Processor"
| where CounterName == "% Processor Time"
| summarize AvgCPU = avg(CounterValue) by bin(TimeGenerated, 5m)
| render timechart
```

**Query 2: Memory Usage**
```kusto
Perf
| where ObjectName == "Memory"
| where CounterName == "% Committed Bytes In Use"
| summarize AvgMemory = avg(CounterValue) by Computer
| render barchart
```

**Query 3: Failed Events**
```kusto
Event
| where EventLevelName == "Error"
| summarize ErrorCount = count() by Computer, Source
| sort by ErrorCount desc
```

#### Task 5: Configure Azure Policy for Compliance

1. Navigate to **Policy** in Azure Portal
2. Click **Definitions** on the left
3. Search for a built-in policy: **Allowed locations**
4. Click on it, then **Assign**
5. Configure:
    - Scope: Your subscription or resource group
    - Allowed locations: Select East US, West US
6. Click **Review + create**, then **Create**
7. Navigate to **Compliance**
8. View compliance status of resources

#### Task 6: Enable Security Center Recommendations

1. Navigate to **Microsoft Defender for Cloud**
2. Go to **Recommendations**
3. Review high-priority recommendations
4. Click on a recommendation (e.g., "Virtual machines should have endpoint protection")
5. Review affected resources
6. Click **Fix** or implement the recommendation manually

**Key Takeaways:**
- Azure Monitor collects metrics and logs from all resources
- Log Analytics enables KQL queries for deep analysis
- Alerts notify you of critical conditions automatically
- Action Groups route alert notifications to appropriate channels
- Azure Policy enforces organizational compliance standards
- Microsoft Defender for Cloud provides security recommendations

**Troubleshooting:**
- **Issue:** No data appearing in Log Analytics
  - **Solution:** Ensure Azure Monitor Agent is installed and running; wait 5-10 minutes for data collection

- **Issue:** Alert not triggering even though condition is met
  - **Solution:** Verify alert rule is enabled; check action group configuration; ensure threshold is correct

- **Issue:** Policy assignments not showing compliance
  - **Solution:** Allow 5-10 minutes for compliance evaluation; manually trigger evaluation if available

### Cleanup

1. Delete alert rules
2. Delete action groups
3. Delete Azure Monitor Agent extensions from VMs
4. Delete Log Analytics workspace
5. Delete Policy assignments
6. Delete the resource group "az104-monitoring-lab"

---

## Summary

These five labs cover the core Azure Administrator skills tested on the AZ-104 exam:

| Lab | Focus Area | Key Skills |
|-----|-----------|-----------|
| Lab 1 | Identity & Access Management | RBAC, Azure AD, Users/Groups |
| Lab 2 | Azure Storage & Backups | Storage accounts, Replication, Backup/Recovery |
| Lab 3 | Virtual Machines & Scaling | VMs, Load Balancers, Auto-scaling |
| Lab 4 | Networking | VNets, NSGs, Route Tables, Application Gateway |
| Lab 5 | Monitoring & Compliance | Azure Monitor, Alerts, Policies, Defender |

**Total Lab Time:** ~245 minutes (4+ hours)

---

## Additional Resources

- [AZ-104 Exam Skills](https://learn.microsoft.com/en-us/certifications/exams/az-104/)
- [Azure Administrator Learning Path](https://learn.microsoft.com/en-us/training/paths/azure-administrator/)
- [Azure Documentation](https://learn.microsoft.com/en-us/azure/)

---

**Last Updated:** February 1, 2026

**Related:** [← Back to Student Resources](/README.md) | [AZ-104 Practice Test](../az104-practice-test.md) | [All Labs](../labs/)
