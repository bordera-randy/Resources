# 🧪 AZ-104 Hands-On Labs

## Azure Administrator Practical Experience

---

## Table of Contents

1. [Lab 1: Identity & Access Management](#lab-1-identity--access-management)
2. [Lab 2: Azure Storage & Backups](#lab-2-azure-storage--backups)
3. [Lab 3: Virtual Machines & Scaling](#lab-3-virtual-machines--scaling)
4. [Lab 4: Networking & Load Balancing](#lab-4-networking--load-balancing)
5. [Lab 5: Monitoring & Compliance](#lab-5-monitoring--compliance)
6. [Lab 6: Azure App Services & Containers](#lab-6-azure-app-services--containers)
7. [Lab 7: Azure DNS & Traffic Manager](#lab-7-azure-dns--traffic-manager)
8. [Lab 8: Azure Site Recovery & High Availability](#lab-8-azure-site-recovery--high-availability)
9. [Lab 9: Azure Key Vault & Managed Identities](#lab-9-azure-key-vault--managed-identities)
10. [Lab 10: Cost Management & Governance](#lab-10-cost-management--governance)

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

#### Query 1: CPU Usage Over Time

```kusto
Perf
| where ObjectName == "Processor"
| where CounterName == "% Processor Time"
| summarize AvgCPU = avg(CounterValue) by bin(TimeGenerated, 5m)
| render timechart
```

#### Query 2: Memory Usage

```kusto
Perf
| where ObjectName == "Memory"
| where CounterName == "% Committed Bytes In Use"
| summarize AvgMemory = avg(CounterValue) by Computer
| render barchart
```

#### Query 3: Failed Events

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

## Lab 6: Azure App Services & Containers

**Objective:** Deploy web applications using Azure App Service and Azure Container Instances

**Estimated Duration:** 50 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Basic understanding of web applications

### Step-by-Step Instructions

#### Task 1: Create Azure App Service Plan

1. Navigate to **App Service plans** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az104-appservice-lab"
   - Name: `asp-az104-lab`
   - Operating System: Linux
   - Region: East US
   - Pricing Tier: Basic B1
4. Click **Review + create**, then **Create**

#### Task 2: Deploy Web App

1. Navigate to **App Services** in Azure Portal
2. Click **Create** > **Web App**
3. Configure:
   - Resource Group: az104-appservice-lab
   - Name: `webapp-az104-[yourname]` (must be globally unique)
   - Publish: Code
   - Runtime stack: Node 18 LTS
   - App Service Plan: asp-az104-lab
4. Click **Review + create**, then **Create**
5. Once deployed, click **Go to resource**
6. Click **Browse** to view the default page

#### Task 3: Deploy Sample Application

1. In your web app, go to **Deployment Center**
2. Select source: **Local Git**
3. Click **Save**
4. Copy the Git Clone Uri
5. In local terminal, clone and deploy:

```bash
git clone [Git Clone Uri]
cd [repository-name]
echo "Hello from Azure App Service" > index.html
git add .
git commit -m "Initial deployment"
git push
```

6. Browse to your web app URL to verify deployment

#### Task 4: Configure Custom Domain and SSL

1. In web app, go to **Custom domains**
2. Click **Add custom domain**
3. Enter your domain name (if you own one)
4. Follow validation steps
5. Go to **TLS/SSL settings**
6. Click **Private Key Certificates (.pfx)**
7. Upload or create managed certificate
8. Go to **Bindings** and bind certificate to your domain

#### Task 5: Create Azure Container Instance

1. Navigate to **Container Instances** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az104-appservice-lab
   - Container name: `aci-nginx-lab`
   - Region: East US
   - Image source: Quick start images
   - Image: nginx
   - OS type: Linux
   - Size: 1 vCPU, 1.5 GB memory
4. Click **Next: Networking**
5. Set DNS name label: `aci-nginx-[yourname]`
6. Ports: 80
7. Click **Review + create**, then **Create**
8. Once deployed, browse to the FQDN to view nginx

#### Task 6: Configure App Service Deployment Slots

1. Navigate back to your web app
2. Go to **Deployment slots**
3. Click **Add Slot**
4. Configure:
   - Name: `staging`
   - Clone settings from: (your production slot)
5. Click **Add**
6. Deploy different content to staging slot
7. Test staging slot
8. Click **Swap** to promote staging to production

**Key Takeaways:**

- App Service Plans define compute resources for web apps
- Deployment slots enable zero-downtime deployments
- Container Instances provide serverless container hosting
- App Service supports multiple languages and frameworks
- Custom domains and SSL certificates secure web applications

**Troubleshooting:**

- **Issue:** Web app deployment fails
  - **Solution:** Check deployment logs in Deployment Center; verify runtime stack compatibility

- **Issue:** Container fails to start
  - **Solution:** Check container logs; verify image name and registry credentials

- **Issue:** Custom domain verification fails
  - **Solution:** Ensure DNS records are correctly configured; wait for DNS propagation

### Cleanup

1. Delete Container Instances
2. Delete Web Apps
3. Delete App Service Plan
4. Delete the resource group "az104-appservice-lab"

---

## Lab 7: Azure DNS & Traffic Manager

**Objective:** Configure DNS zones and implement global traffic distribution with Traffic Manager

**Estimated Duration:** 45 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Domain name (optional, can use Azure-provided names)

### Step-by-Step Instructions

#### Task 1: Create Azure DNS Zone

1. Navigate to **DNS zones** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az104-dns-lab"
   - Name: `yourdomain.com` (use a test domain if available)
4. Click **Review + create**, then **Create**
5. Note the Azure DNS name servers

#### Task 2: Add DNS Records

1. In your DNS zone, click **+ Record set**
2. Create A record:
   - Name: `www`
   - Type: A
   - TTL: 3600
   - IP address: (use a public IP from previous labs or 1.2.3.4 for testing)
3. Click **OK**
4. Create CNAME record:
   - Name: `blog`
   - Type: CNAME
   - TTL: 3600
   - Alias: `www.yourdomain.com`
5. Click **OK**
6. Create MX record for email:
   - Name: `@`
   - Type: MX
   - TTL: 3600
   - Preference: 10
   - Mail exchange: `mail.yourdomain.com`
7. Click **OK**

#### Task 3: Create Traffic Manager Profile

1. Navigate to **Traffic Manager profiles** in Azure Portal
2. Click **Create**
3. Configure:
   - Name: `tm-az104-lab`
   - Routing method: Performance
   - Resource group: az104-dns-lab
4. Click **Create**

#### Task 4: Add Traffic Manager Endpoints

1. In Traffic Manager profile, go to **Endpoints**
2. Click **+ Add**
3. Configure first endpoint:
   - Type: Azure endpoint
   - Name: `endpoint-eastus`
   - Target resource type: App Service
   - Target resource: (select a web app from previous lab or create new)
4. Click **Add**
5. Repeat to add second endpoint:
   - Name: `endpoint-westus`
   - Target resource: (another web app in different region)
6. Monitor endpoint health in the overview page

#### Task 5: Configure Geographic Routing

1. Create new Traffic Manager profile with Geographic routing
2. Configure:
   - Name: `tm-geo-az104-lab`
   - Routing method: Geographic
3. Add endpoints with geographic mappings:
   - Endpoint 1: North America → East US web app
   - Endpoint 2: Europe → West Europe web app
4. Test routing by accessing from different locations

#### Task 6: Implement DNS Alias Records

1. Navigate back to your DNS zone
2. Click **+ Record set**
3. Create alias record:
   - Name: `app`
   - Type: A
   - Alias record set: Yes
   - Alias type: Traffic Manager profile
   - Traffic Manager profile: tm-az104-lab
4. Click **OK**
5. Test resolution: `nslookup app.yourdomain.com`

**Key Takeaways:**

- Azure DNS provides authoritative DNS hosting
- Traffic Manager distributes traffic globally based on routing methods
- Performance routing directs users to nearest endpoint
- Geographic routing routes based on user location
- DNS alias records simplify management of Azure resources

**Troubleshooting:**

- **Issue:** DNS records not resolving
  - **Solution:** Verify name servers at domain registrar match Azure DNS servers; allow time for propagation

- **Issue:** Traffic Manager endpoint shows degraded
  - **Solution:** Check endpoint health probe settings; verify target resource is running

- **Issue:** Geographic routing not working
  - **Solution:** Test from different geographic locations; verify endpoint mappings

### Cleanup

1. Delete Traffic Manager profiles
2. Delete DNS zones
3. Delete the resource group "az104-dns-lab"

---

## Lab 8: Azure Site Recovery & High Availability

**Objective:** Configure disaster recovery and implement high availability solutions

**Estimated Duration:** 60 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Lab 3 completed (VMs for replication)

### Step-by-Step Instructions

#### Task 1: Create Recovery Services Vault

1. Navigate to **Recovery Services vaults** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az104-recovery-lab"
   - Vault name: `rsv-az104-lab`
   - Region: West US (different from source VMs)
4. Click **Review + create**, then **Create**

#### Task 2: Configure Site Recovery for Virtual Machines

1. In Recovery Services vault, go to **Site Recovery**
2. Click **Prepare infrastructure** under Azure virtual machines
3. Configure:
   - Source region: East US
   - Source resource group: (select VM resource group)
   - Deployment model: Resource Manager
   - Disaster recovery between availability zones: No
4. Click **Next**
5. Target settings:
   - Target region: West US
   - Target resource group: Create new
6. Click **Next**
7. Select VMs to replicate
8. Review replication settings
9. Click **Enable replication**
10. Monitor replication progress

#### Task 3: Configure Availability Sets

1. Navigate to **Availability sets** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az104-recovery-lab
   - Name: `avset-lab`
   - Region: East US
   - Fault domains: 2
   - Update domains: 5
4. Click **Review + create**, then **Create**
5. Create new VMs and assign to availability set during creation

#### Task 4: Perform Test Failover

1. Navigate to Recovery Services vault
2. Go to **Replicated items**
3. Select a replicated VM
4. Click **Test Failover**
5. Configure:
   - Recovery point: Latest processed
   - Azure virtual network: Select or create test network
6. Click **OK**
7. Monitor failover progress in notifications
8. Once complete, verify test VM in target region
9. Click **Cleanup test failover** when testing is complete

#### Task 5: Create Backup Policy

1. In Recovery Services vault, go to **Backup policies**
2. Click **+ Add**
3. Configure:
   - Policy type: Azure Virtual Machine
   - Policy name: `daily-backup-policy`
   - Backup schedule: Daily at 2:00 AM
   - Retention: 30 days
4. Click **Create**

#### Task 6: Configure VM Backup

1. In Recovery Services vault, go to **Backup**
2. Select workload: **Azure**
3. Select what to backup: **Virtual Machine**
4. Click **Backup**
5. Select VMs to back up
6. Choose backup policy: daily-backup-policy
7. Click **Enable Backup**
8. Trigger backup manually: **Backup now**

**Key Takeaways:**

- Azure Site Recovery enables disaster recovery between regions
- Availability Sets distribute VMs across fault/update domains
- Test failovers validate disaster recovery without impacting production
- Backup policies automate VM protection
- Recovery points enable point-in-time restoration

**Troubleshooting:**

- **Issue:** Replication failing
  - **Solution:** Verify network connectivity; check firewall rules; ensure sufficient permissions

- **Issue:** Test failover fails
  - **Solution:** Verify target network exists; check for resource conflicts; review error logs

- **Issue:** Backup jobs failing
  - **Solution:** Check VM agent status; verify vault capacity; review backup policy settings

### Cleanup

1. Delete replicated items
2. Delete test failover resources
3. Delete backup items
4. Delete Recovery Services vault
5. Delete the resource group "az104-recovery-lab"

---

## Lab 9: Azure Key Vault & Managed Identities

**Objective:** Secure secrets, keys, and certificates using Azure Key Vault with managed identities

**Estimated Duration:** 45 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Lab 3 or Lab 6 completed (VM or App Service for testing)

### Step-by-Step Instructions

#### Task 1: Create Azure Key Vault

1. Navigate to **Key vaults** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az104-keyvault-lab"
   - Key vault name: `kv-az104-[yourname]` (must be globally unique)
   - Region: East US
   - Pricing tier: Standard
4. Click **Next: Access policy**
5. Add yourself with all permissions
6. Click **Review + create**, then **Create**

#### Task 2: Add Secrets to Key Vault

1. In Key Vault, go to **Secrets**
2. Click **+ Generate/Import**
3. Create first secret:
   - Name: `DatabasePassword`
   - Value: `P@ssw0rd123!`
4. Click **Create**
5. Create second secret:
   - Name: `ApiKey`
   - Value: `abcd1234efgh5678`
6. Click **Create**
7. View secret and copy Secret Identifier

#### Task 3: Create and Upload Certificates

1. In Key Vault, go to **Certificates**
2. Click **+ Generate/Import**
3. Configure:
   - Method of Certificate Creation: Generate
   - Certificate Name: `ssl-certificate`
   - Subject: `CN=yourdomain.com`
   - Validity Period: 12 months
4. Click **Create**
5. Monitor certificate creation
6. Download certificate once created

#### Task 4: Enable Managed Identity on Virtual Machine

1. Navigate to a VM from previous labs
2. Go to **Identity**
3. Under **System assigned** tab:
   - Status: On
4. Click **Save**
5. Note the Object (principal) ID

#### Task 5: Grant Key Vault Access to Managed Identity

1. Navigate back to Key Vault
2. Go to **Access policies**
3. Click **+ Add Access Policy**
4. Configure:
   - Secret permissions: Get, List
   - Select principal: (search for your VM name)
5. Click **Add**
6. Click **Save**

#### Task 6: Access Key Vault from VM

1. Connect to the VM via RDP or SSH
2. Install Azure CLI or use PowerShell
3. Authenticate using managed identity:

```powershell
# PowerShell example
$response = Invoke-RestMethod -Uri 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://vault.azure.net' -Method GET -Headers @{Metadata="true"}
$KeyVaultToken = $response.access_token

# Get secret
$secret = Invoke-RestMethod -Uri 'https://kv-az104-[yourname].vault.azure.net/secrets/DatabasePassword?api-version=7.2' -Method GET -Headers @{Authorization="Bearer $KeyVaultToken"}
Write-Host $secret.value
```

4. Verify secret retrieval succeeds

#### Task 7: Enable Key Vault Logging

1. In Key Vault, go to **Diagnostic settings**
2. Click **+ Add diagnostic setting**
3. Configure:
   - Diagnostic setting name: `kv-audit-logs`
   - Logs: Select all log categories
   - Destination: Send to Log Analytics workspace
   - Workspace: Create or select existing
4. Click **Save**
5. View logs in Log Analytics after some activity

**Key Takeaways:**

- Azure Key Vault centrally manages secrets, keys, and certificates
- Managed identities eliminate need for credentials in code
- Access policies control who can access vault contents
- Diagnostic logs provide audit trail of vault operations
- Key Vault integrates with Azure services for secure credential storage

**Troubleshooting:**

- **Issue:** Managed identity cannot access Key Vault
  - **Solution:** Verify access policy is configured; check managed identity is enabled; allow time for permissions to propagate

- **Issue:** Secret retrieval fails with 403 error
  - **Solution:** Verify correct permissions in access policy; ensure vault firewall allows access

- **Issue:** Certificate creation fails
  - **Solution:** Check certificate parameters; verify Key Vault permissions; review error details

### Cleanup

1. Delete secrets and certificates
2. Delete Key Vault
3. Disable managed identity on VM
4. Delete the resource group "az104-keyvault-lab"

---

## Lab 10: Cost Management & Governance

**Objective:** Implement cost controls, budgets, and governance policies

**Estimated Duration:** 40 minutes

**Prerequisites:**

- Azure subscription with owner or billing reader access
- Resources from previous labs (optional, for cost analysis)

### Step-by-Step Instructions

#### Task 1: Analyze Current Costs

1. Navigate to **Cost Management + Billing** in Azure Portal
2. Go to **Cost analysis**
3. Select scope: Your subscription
4. View current month costs
5. Group by:
   - Resource group
   - Service name
   - Location
6. Apply filters to analyze specific resources
7. Export cost data to CSV

#### Task 2: Create Budget

1. In Cost Management, go to **Budgets**
2. Click **+ Add**
3. Configure:
   - Name: `monthly-budget-lab`
   - Reset period: Monthly
   - Creation date: First day of current month
   - Expiration date: One year from now
   - Amount: $100
4. Click **Next**
5. Set alert conditions:
   - Alert 1: 80% of budget
   - Alert 2: 100% of budget
   - Alert 3: 120% of budget
6. Add email recipients
7. Click **Create**

#### Task 3: Configure Cost Alerts

1. In Cost Management, go to **Cost alerts**
2. Click **+ Add**
3. Configure anomaly alert:
   - Alert type: Anomaly
   - Threshold: Medium
   - Email recipients: Your email
4. Click **Create**

#### Task 4: Implement Resource Tags

1. Navigate to **Tags** in Azure Portal
2. Create tag policy:
   - Navigate to **Policy**
   - Search for "Require a tag on resources"
   - Click **Assign**
3. Configure:
   - Scope: Your subscription
   - Tag name: `Environment`
   - Effect: Deny
4. Click **Review + create**, then **Create**
5. Test by creating resource without Environment tag (should fail)
6. Create resource with Environment tag (should succeed)

#### Task 5: Create Management Groups

1. Navigate to **Management groups**
2. Click **+ Add management group**
3. Configure:
   - Management group ID: `mg-production`
   - Display name: `Production Environment`
4. Click **Submit**
5. Create another management group:
   - ID: `mg-development`
   - Display name: `Development Environment`
6. Move subscriptions to appropriate management groups

#### Task 6: Implement Azure Advisor Recommendations

1. Navigate to **Advisor** in Azure Portal
2. Review recommendations in categories:
   - Cost
   - Security
   - Reliability
   - Operational Excellence
   - Performance
3. Select a cost recommendation
4. Review details and potential savings
5. Click **Implement** or note manual steps
6. Postpone or dismiss non-applicable recommendations

#### Task 7: Configure Resource Locks

1. Navigate to a critical resource group
2. Go to **Locks**
3. Click **+ Add**
4. Configure:
   - Lock name: `prevent-deletion`
   - Lock type: Delete
   - Notes: Protects production resources
5. Click **OK**
6. Test by attempting to delete a resource (should fail)

**Key Takeaways:**

- Cost Management provides visibility into Azure spending
- Budgets and alerts prevent cost overruns
- Resource tags enable cost allocation and organization
- Management groups apply policies across subscriptions
- Azure Advisor provides proactive recommendations
- Resource locks prevent accidental deletion or modification

**Troubleshooting:**

- **Issue:** Budget alerts not received
  - **Solution:** Verify email addresses are correct; check spam folder; ensure budget threshold is exceeded

- **Issue:** Policy assignment not enforced
  - **Solution:** Wait 15-30 minutes for policy to take effect; verify policy scope is correct

- **Issue:** Cannot see cost data
  - **Solution:** Verify you have appropriate billing permissions; check date range selection

### Cleanup

1. Delete budgets and cost alerts
2. Remove policy assignments
3. Delete management groups
4. Remove resource locks
5. Remove resource tags if desired

---

## Summary

These ten labs cover comprehensive Azure Administrator skills tested on the AZ-104 exam:

| Lab | Focus Area | Key Skills |
| --- | --- | --- |
| Lab 1 | Identity & Access Management | RBAC, Azure AD, Users/Groups |
| Lab 2 | Azure Storage & Backups | Storage accounts, Replication, Backup/Recovery |
| Lab 3 | Virtual Machines & Scaling | VMs, Load Balancers, Auto-scaling |
| Lab 4 | Networking | VNets, NSGs, Route Tables, Application Gateway |
| Lab 5 | Monitoring & Compliance | Azure Monitor, Alerts, Policies, Defender |
| Lab 6 | App Services & Containers | Web Apps, Containers, Deployment Slots |
| Lab 7 | DNS & Traffic Manager | DNS Zones, Traffic Distribution, Routing |
| Lab 8 | Site Recovery & HA | Disaster Recovery, Backups, Availability |
| Lab 9 | Key Vault & Identities | Secrets Management, Managed Identities |
| Lab 10 | Cost & Governance | Budgets, Tags, Policies, Locks |

**Total Lab Time:** ~485 minutes (8+ hours)

---

## Additional Resources

- [AZ-104 Exam Skills](https://learn.microsoft.com/en-us/certifications/exams/az-104/)
- [Azure Administrator Learning Path](https://learn.microsoft.com/en-us/training/paths/azure-administrator/)
- [Azure Documentation](https://learn.microsoft.com/en-us/azure/)

---

**Last Updated:** February 1, 2026

**Related:** [← Back to Resources](../../../../README.md) | [AZ-104 Practice Test](../practice-tests/az104-practice-test.md) | [All Azure Labs](./)
