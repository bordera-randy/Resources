# 🔐 AZ-500 Hands-On Labs

## Azure Security Technologies Practical Experience

---

## Table of Contents

1. [Lab 1: Identity & Access Management](#lab-1-identity--access-management)
2. [Lab 2: Platform Protection](#lab-2-platform-protection)
3. [Lab 3: Data & Application Security](#lab-3-data--application-security)
4. [Lab 4: Security Operations](#lab-4-security-operations)
5. [Lab 5: Azure Policy & Compliance](#lab-5-azure-policy--compliance)
6. [Lab 6: Container Security](#lab-6-container-security)
7. [Lab 7: Backup & Disaster Recovery](#lab-7-backup--disaster-recovery)
8. [Lab 8: Identity Protection & Risk Management](#lab-8-identity-protection--risk-management)
9. [Lab 9: Application Gateway & WAF](#lab-9-application-gateway--waf)
10. [Lab 10: Security Center Automation](#lab-10-security-center-automation)

---

## Lab 1: Identity & Access Management

**Objective:** Configure Azure AD users, groups, MFA, and Privileged Identity Management

**Estimated Duration:** 60 minutes

**Prerequisites:**

- Azure subscription with Global Administrator role
- Access to Azure Portal

### Step-by-Step Instructions

#### Task 1: Configure Azure AD Users and Groups

1. Navigate to **Azure Active Directory** > **Users**
2. Click **New User**
3. Create a new user with:
    - User principal name: `securityadmin@yourdomain.onmicrosoft.com`
    - Name: Security Administrator
    - Password: Generate (save temporarily)
4. Repeat to create another user: `appuser@yourdomain.onmicrosoft.com` (Application User)
5. Navigate to **Azure AD** > **Groups**
6. Click **New Group**
7. Create group "Security Admins":
    - Group type: Security
    - Add securityadmin user as member
8. Navigate to **Azure AD** > **Administrative units**
9. Click **Add**
10. Create administrative unit:
    - Name: `IT-Department`
    - Add Security Admins group

#### Task 2: Implement Multi-Factor Authentication (MFA)

1. Navigate to **Azure Active Directory** > **Security**
2. Click **Multifactor authentication**
3. Select users to enable MFA
4. Click **Enable**
5. Navigate to **Conditional Access**
6. Click **New policy**
7. Configure:
    - Name: `Require-MFA-All-Users`
    - Users: All users
    - Cloud apps: All cloud apps
    - Grant: Require multi-factor authentication
8. Enable policy: **On**
9. Click **Create**

#### Task 3: Test MFA Functionality

1. Open a private/incognito browser window
2. Navigate to <https://portal.azure.com>
3. Sign in with the test user created earlier
4. Follow MFA setup prompts
5. Complete authentication using phone/app
6. Verify access to Azure Portal

#### Task 4: Configure Azure AD Privileged Identity Management (PIM)

1. Navigate to **Azure AD Privileged Identity Management**
2. Click **Azure AD roles**
3. Click **Settings**
4. Select **Global Administrator** role
5. Click **Edit**
6. Configure:
    - Activation maximum duration: 8 hours
    - Require justification on activation: Yes
    - Require approval to activate: Yes
7. Click **Update**
8. Click **Assignments** > **Add assignments**
9. Select role: **Security Administrator**
10. Select member: securityadmin user
11. Assignment type: **Eligible**
12. Click **Next** > **Assign**

#### Task 5: Activate PIM Roles and Review Audit History

1. Sign in as securityadmin user
2. Navigate to **PIM** > **My roles**
3. Click **Activate** for Security Administrator role
4. Provide justification
5. Submit request
6. As Global Admin, review and approve request
7. Navigate to **PIM** > **Audit history**
8. Review activation logs

**Key Takeaways:**

- MFA provides additional authentication factor beyond passwords
- Conditional Access policies enforce security requirements
- PIM enables just-in-time privileged access
- Audit history provides accountability trail
- Administrative units segment Azure AD management

**Troubleshooting:**

- **Issue:** MFA not prompting during sign-in
  - **Solution:** Clear browser cache, ensure conditional access policy is enabled and applied

- **Issue:** PIM role activation not appearing
  - **Solution:** Wait 5-10 minutes for role assignment propagation, refresh browser

### Cleanup

1. Remove PIM role assignments
2. Disable conditional access policies
3. Delete test users and groups
4. Delete administrative units

---

## Lab 2: Platform Protection

**Objective:** Configure Network Security Groups, Azure Firewall, and service endpoints

**Estimated Duration:** 55 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Lab 1 completed (optional)

### Step-by-Step Instructions

#### Task 1: Create Network Security Groups (NSGs)

1. Navigate to **Network security groups** in Azure Portal
2. Click **Create**
3. Configure:
    - Resource Group: Create new "az500-platform-lab"
    - Name: `nsg-web-tier`
    - Region: East US
4. Click **Review + create**, then **Create**
5. Once deployed, click **Go to resource**
6. Go to **Inbound security rules**
7. Click **+ Add**
8. Configure rule:
    - Source: Any
    - Source port ranges: *
    - Destination: Any
    - Service: HTTPS
    - Action: Allow
    - Priority: 100
    - Name: `allow-https`
9. Click **Add**
10. Add another rule to deny all other traffic:
    - Priority: 4096
    - Action: Deny
    - Name: `deny-all-inbound`

#### Task 2: Create Virtual Network and Associate NSGs with Subnets

1. Navigate to **Virtual networks**
2. Click **Create**
3. Configure:
    - Resource Group: az500-platform-lab
    - Name: `vnet-secure`
    - Region: East US
    - IPv4 address space: 10.1.0.0/16
4. Click **Next: IP Addresses**
5. Add subnet: `subnet-web` (10.1.1.0/24)
6. Add subnet: `subnet-app` (10.1.2.0/24)
7. Click **Review + create**, then **Create**
8. Navigate to created VNet > **Subnets**
9. Click `subnet-web`
10. Set Network security group to `nsg-web-tier`
11. Click **Save**

#### Task 3: Test Traffic Filtering

1. Create a test VM in `subnet-web`:
    - Name: `vm-web-test`
    - Image: Windows Server 2022
    - Public IP: Yes
2. After deployment, attempt to RDP (port 3389)
3. Verify connection is blocked by NSG
4. Add temporary NSG rule to allow your IP for RDP
5. Verify connection succeeds

#### Task 4: Implement Azure Firewall

1. Navigate to **Firewalls**
2. Click **Create**
3. Configure:
    - Resource Group: az500-platform-lab
    - Name: `fw-secure`
    - Region: East US
    - Firewall tier: Standard
    - Virtual network: `vnet-secure`
    - Subnet: Create `AzureFirewallSubnet` (10.1.0.0/26)
    - Public IP: Create new `fw-pip`
4. Click **Review + create**, then **Create**
5. Wait for deployment (takes 5-10 minutes)

#### Task 5: Configure Application and Network Rules

1. Navigate to created firewall > **Rules (classic)**
2. Click **Application rule collection**
3. Click **+ Add application rule collection**
4. Configure:
    - Name: `allow-web-access`
    - Priority: 100
    - Action: Allow
    - Rules:
      - Name: `allow-microsoft`
      - Source addresses: 10.1.0.0/16
      - Protocol:port: https:443
      - Target FQDNs: `*.microsoft.com`
5. Click **Add**
6. Click **Network rule collection**
7. Click **+ Add network rule collection**
8. Configure:
    - Name: `allow-dns`
    - Priority: 100
    - Action: Allow
    - Rules:
      - Name: `allow-dns-queries`
      - Protocol: UDP
      - Source addresses: 10.1.0.0/16
      - Destination addresses: *
      - Destination ports: 53
9. Click **Add**

#### Task 6: Monitor Firewall Logs

1. Navigate to **Diagnostic settings**
2. Click **+ Add diagnostic setting**
3. Configure:
    - Name: `fw-diagnostics`
    - Logs: Select all categories
    - Destination: Send to Log Analytics workspace (create if needed)
4. Click **Save**
5. Wait 10-15 minutes for logs to appear
6. Query logs in Log Analytics

#### Task 7: Configure Virtual Network Service Endpoints

1. Navigate to **Storage accounts**
2. Create new storage account:
    - Resource Group: az500-platform-lab
    - Name: `stsecure[random]`
    - Region: East US
3. After creation, navigate to **Networking**
4. Set **Public network access**: Enabled from selected virtual networks and IP addresses
5. Click **+ Add existing virtual network**
6. Select `vnet-secure` and `subnet-app`
7. Click **Add**
8. Click **Save**
9. Navigate to **Virtual networks** > `vnet-secure` > **Subnets**
10. Click `subnet-app`
11. Under **Service endpoints**, select **Microsoft.Storage**
12. Click **Save**

**Key Takeaways:**

- NSGs filter traffic at Layer 4 (network/transport)
- Azure Firewall provides stateful firewall with FQDN filtering
- Application rules filter based on domain names
- Network rules filter based on IP/protocol/port
- Service endpoints secure Azure services to specific VNets
- Diagnostic logs enable security monitoring and auditing

**Troubleshooting:**

- **Issue:** Firewall deployment fails
  - **Solution:** Ensure AzureFirewallSubnet is exactly /26 and named correctly

- **Issue:** Cannot access storage from subnet
  - **Solution:** Verify service endpoint is enabled on subnet and storage firewall allows the VNet

### Cleanup

1. Delete Azure Firewall
2. Delete Virtual Machines
3. Delete Network Security Groups
4. Delete Storage Account
5. Delete Virtual Network
6. Delete resource group "az500-platform-lab"

---

## Lab 3: Data & Application Security

**Objective:** Implement Azure Key Vault, SQL Database security, and Storage encryption

**Estimated Duration:** 60 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Familiarity with Azure SQL and Storage

### Step-by-Step Instructions

#### Task 1: Implement Azure Key Vault

1. Navigate to **Key vaults** in Azure Portal
2. Click **Create**
3. Configure:
    - Resource Group: Create new "az500-data-lab"
    - Name: `kv-secure-[random]`
    - Region: East US
    - Pricing tier: Standard
4. Click **Next: Access policy**
5. Click **+ Add Access Policy**
6. Configure:
    - Key permissions: Get, List, Create
    - Secret permissions: Get, List, Set
    - Certificate permissions: Get, List
    - Select principal: Your user account
7. Click **Add**
8. Click **Review + create**, then **Create**

#### Task 2: Store Secrets and Keys

1. Navigate to created Key Vault
2. Click **Secrets** (under Objects)
3. Click **+ Generate/Import**
4. Configure:
    - Name: `sql-connection-string`
    - Value: `Server=tcp:myserver.database.windows.net;Database=mydb;`
5. Click **Create**
6. Click **Keys** (under Objects)
7. Click **+ Generate/Import**
8. Configure:
    - Options: Generate
    - Name: `encryption-key`
    - Key type: RSA
    - RSA key size: 2048
9. Click **Create**

#### Task 3: Configure Access Policies

1. In Key Vault, go to **Access policies**
2. Click **+ Add Access Policy**
3. Configure for application access:
    - Secret permissions: Get, List
    - Select principal: Create new app registration
4. Navigate to **Azure Active Directory** > **App registrations**
5. Click **New registration**
6. Name: `app-keyvault-access`
7. Click **Register**
8. Copy Application (client) ID
9. Go to **Certificates & secrets**
10. Create new client secret (save value)
11. Return to Key Vault access policies
12. Add policy for the app registration
13. Click **Save**

#### Task 4: Configure Azure SQL Database Security

1. Navigate to **SQL databases**
2. Click **Create**
3. Configure:
    - Resource Group: az500-data-lab
    - Database name: `db-secure`
    - Server: Create new
      - Server name: `sql-secure-[random]`
      - Authentication: SQL authentication
      - Admin login: sqladmin
      - Password: (create strong password)
    - Compute + storage: Basic (for testing)
4. Click **Review + create**, then **Create**

#### Task 5: Enable Transparent Data Encryption (TDE)

1. Navigate to created SQL server
2. Click on the database `db-secure`
3. Go to **Transparent data encryption**
4. Verify TDE is **On** (enabled by default)
5. Note: Data is encrypted at rest automatically

#### Task 6: Configure Firewall Rules

1. Navigate to SQL server `sql-secure-[random]`
2. Go to **Networking** (under Security)
3. Set **Public network access**: Selected networks
4. Click **+ Add client IP**
5. Add your current IP address
6. Create virtual network rule:
    - Click **+ Add existing virtual network**
    - Select VNet from Lab 2 (if available)
7. Click **Save**

#### Task 7: Implement Advanced Threat Protection

1. In SQL server, go to **Microsoft Defender for Cloud**
2. Click **Enable Microsoft Defender for SQL**
3. Configure:
    - Enable on subscription level: Yes
    - Email notifications: Your email
4. Click **Save**
5. After enabling, go to **Security alerts**
6. Review any detected threats (simulated or real)

#### Task 8: Configure Storage Account Security

1. Navigate to **Storage accounts**
2. Click **Create**
3. Configure:
    - Resource Group: az500-data-lab
    - Name: `stsecdata[random]`
    - Region: East US
    - Redundancy: LRS
4. Click **Review + create**, then **Create**

#### Task 9: Enable Storage Service Encryption

1. Navigate to created storage account
2. Go to **Encryption** (under Security + networking)
3. Verify encryption is enabled with Microsoft-managed keys
4. Change to customer-managed keys:
    - Select **Customer-managed keys**
    - Key vault: Select Key Vault from Task 1
    - Key: Select `encryption-key` created earlier
5. Click **Save**

#### Task 10: Configure Shared Access Signatures (SAS)

1. In storage account, go to **Shared access signature**
2. Configure:
    - Allowed services: Blob
    - Allowed resource types: Object
    - Allowed permissions: Read
    - Start time: Current time
    - Expiry time: 1 hour from now
    - Allowed protocols: HTTPS only
3. Click **Generate SAS and connection string**
4. Copy SAS token (save for testing)
5. Test by accessing blob with SAS URL

#### Task 11: Implement Storage Account Firewalls

1. In storage account, go to **Networking**
2. Set **Public network access**: Enabled from selected virtual networks and IP addresses
3. Click **+ Add your client IP address**
4. Optionally add virtual network rule
5. Click **Save**
6. Test access from allowed/blocked locations

**Key Takeaways:**

- Azure Key Vault centralizes secrets, keys, and certificates
- TDE encrypts SQL databases at rest automatically
- SQL firewall rules control network access
- Microsoft Defender for SQL detects threats and vulnerabilities
- Storage encryption can use Microsoft or customer-managed keys
- SAS tokens provide delegated access to storage resources
- Storage firewalls restrict access by IP or VNet

**Troubleshooting:**

- **Issue:** Cannot access Key Vault secrets
  - **Solution:** Verify access policy grants necessary permissions; check RBAC roles

- **Issue:** SQL connection fails
  - **Solution:** Ensure firewall rule allows your IP; verify credentials

- **Issue:** Storage SAS token doesn't work
  - **Solution:** Check token hasn't expired; verify permissions and protocols match usage

### Cleanup

1. Delete SQL database and server
2. Delete Storage accounts
3. Delete Key Vault
4. Delete App registration
5. Delete resource group "az500-data-lab"

---

## Lab 4: Security Operations

**Objective:** Configure Microsoft Defender for Cloud, Azure Monitor, and Microsoft Sentinel

**Estimated Duration:** 55 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Resources from previous labs (optional, for monitoring)

### Step-by-Step Instructions

#### Task 1: Configure Microsoft Defender for Cloud

1. Navigate to **Microsoft Defender for Cloud**
2. Go to **Environment settings**
3. Expand subscription hierarchy
4. Click on your subscription
5. Go to **Defender plans**
6. Enable the following plans:
    - Servers: **On**
    - App Service: **On**
    - Databases: **On**
    - Storage: **On**
    - Key Vault: **On**
7. Click **Save**

#### Task 2: Review Security Recommendations

1. In Defender for Cloud, go to **Recommendations**
2. Review high-severity recommendations
3. Click on a recommendation (e.g., "MFA should be enabled on accounts with owner permissions")
4. Review affected resources
5. Click **Take action**
6. Follow remediation steps
7. Mark as resolved or implement fix

#### Task 3: Implement Security Controls

1. In Defender for Cloud, go to **Regulatory compliance**
2. Select **Azure Security Benchmark**
3. Review compliance score
4. Click on a control (e.g., "IM-1: Use centralized identity and authentication system")
5. Review associated recommendations
6. Implement recommendations to improve score

#### Task 4: Configure Security Alerts

1. In Defender for Cloud, go to **Security alerts**
2. Click **Configure email notifications**
3. Add email address for notifications
4. Set severity threshold: Medium or higher
5. Click **Save**
6. Review any existing alerts
7. Investigate and remediate as needed

#### Task 5: Configure Azure Monitor and Log Analytics

1. Navigate to **Log Analytics workspaces**
2. Click **Create**
3. Configure:
    - Resource Group: Create new "az500-security-ops"
    - Name: `law-secops`
    - Region: East US
4. Click **Review + create**, then **Create**

#### Task 6: Configure Data Collection

1. Navigate to **Monitor** > **Data Collection Rules**
2. Click **Create**
3. Configure:
    - Rule name: `dcr-security-logs`
    - Resource Group: az500-security-ops
    - Region: East US
4. Click **Next: Resources**
5. Add resources to monitor (VMs, if available)
6. Click **Next: Collect and deliver**
7. Add data source:
    - Data source type: Windows Event Logs
    - Configure: Security events
8. Add destination: Log Analytics workspace `law-secops`
9. Click **Review + create**, then **Create**

#### Task 7: Create Alert Rules

1. Navigate to **Monitor** > **Alerts**
2. Click **+ Create** > **Alert rule**
3. Select scope: Your subscription or specific resources
4. Click **Condition**
5. Select signal: **Activity Log - Delete Virtual Machine**
6. Configure:
    - Event level: All selected
    - Status: All selected
7. Click **Next: Actions**
8. Create action group:
    - Name: `ag-security-alerts`
    - Add notification: Email/SMS
9. Click **Next: Details**
10. Configure:
    - Alert rule name: `Alert-VM-Deletion`
    - Severity: High (Sev 1)
11. Click **Review + create**, then **Create**

#### Task 8: Create Custom Queries

1. Navigate to **Log Analytics workspace** > `law-secops`
2. Go to **Logs**
3. Create queries for security analysis:

**Query 1: Failed Sign-ins**

```kusto
SigninLogs
| where ResultType != 0
| summarize FailedAttempts = count() by UserPrincipalName, IPAddress
| where FailedAttempts > 5
| sort by FailedAttempts desc
```

**Query 2: Security Events**

```kusto
SecurityEvent
| where EventID in (4625, 4648, 4720, 4722, 4724)
| summarize EventCount = count() by EventID, Activity
| sort by EventCount desc
```

**Query 3: Resource Changes**

```kusto
AzureActivity
| where OperationNameValue contains "delete" or OperationNameValue contains "write"
| summarize Changes = count() by Caller, ResourceProviderValue
| sort by Changes desc
```

#### Task 9: Configure Microsoft Sentinel

1. Navigate to **Microsoft Sentinel**
2. Click **+ Create**
3. Select workspace: `law-secops`
4. Click **Add**
5. Wait for Sentinel to provision

#### Task 10: Connect Data Sources

1. In Sentinel, go to **Data connectors**
2. Search for **Azure Activity**
3. Click **Open connector page**
4. Click **Connect**
5. Repeat for additional connectors:
    - Azure Active Directory
    - Microsoft Defender for Cloud
    - Office 365 (if available)

#### Task 11: Create Analytics Rules

1. In Sentinel, go to **Analytics**
2. Click **+ Create** > **Scheduled query rule**
3. Configure:
    - Name: `Multiple-Failed-Logins`
    - Tactics: Credential Access
    - Severity: Medium
4. Set rule logic:

```kusto
SigninLogs
| where ResultType != 0
| summarize FailedAttempts = count() by UserPrincipalName, IPAddress
| where FailedAttempts > 10
```

5. Set query scheduling: Run every 5 hours
6. Configure alert grouping
7. Click **Next: Incident settings**
8. Enable incident creation
9. Click **Next: Automated response**
10. Optionally add automation rules
11. Click **Review and create**, then **Create**

#### Task 12: Investigate Incidents

1. In Sentinel, go to **Incidents**
2. Click on an incident (or create test incident)
3. Review incident details:
    - Entities involved
    - Timeline
    - Evidence
4. Click **Investigate**
5. Use investigation graph to visualize relationships
6. Add comments and update incident status
7. Close incident when resolved

**Key Takeaways:**

- Microsoft Defender for Cloud provides unified security management
- Security recommendations guide hardening efforts
- Azure Monitor collects telemetry from all resources
- Log Analytics enables advanced query and analysis
- Alert rules notify of critical security events
- Microsoft Sentinel provides SIEM and SOAR capabilities
- Data connectors centralize security logs
- Analytics rules detect threats automatically
- Investigation tools help understand attack scope

**Troubleshooting:**

- **Issue:** No data in Log Analytics
  - **Solution:** Verify data collection rules are configured; wait 10-15 minutes for initial data

- **Issue:** Sentinel alerts not triggering
  - **Solution:** Check analytics rule query logic; verify data connectors are active

- **Issue:** Cannot connect data source to Sentinel
  - **Solution:** Ensure necessary permissions; some connectors require specific licenses

### Cleanup

1. Delete Microsoft Sentinel workspace connection
2. Delete Log Analytics workspace
3. Disable Microsoft Defender plans
4. Delete alert rules and action groups
5. Delete data collection rules
6. Delete resource group "az500-security-ops"

---

## Lab 5: Azure Policy & Compliance

**Objective:** Implement Azure Policy, governance controls, and compliance monitoring

**Estimated Duration:** 50 minutes

**Prerequisites:**

- Azure subscription with contributor or owner access
- Basic understanding of Azure resources

### Step-by-Step Instructions

#### Task 1: Create Custom Azure Policy Definitions

1. Navigate to **Policy** in Azure Portal
2. Click **Definitions** under Authoring
3. Click **+ Policy definition**
4. Configure:
    - Definition location: Your subscription
    - Name: `require-tag-environment`
    - Category: Create new "Custom Policies"
5. Add policy rule:

```json
{
  "mode": "Indexed",
  "policyRule": {
    "if": {
      "field": "tags['Environment']",
      "exists": "false"
    },
    "then": {
      "effect": "deny"
    }
  }
}
```

6. Click **Save**

#### Task 2: Assign Built-in Policies

1. In **Policy**, go to **Assignments**
2. Click **Assign policy**
3. Configure:
    - Scope: Your subscription
    - Policy definition: Search "Allowed locations"
    - Assignment name: `Restrict-Resource-Locations`
4. Click **Next: Parameters**
5. Select allowed locations: East US, West US
6. Click **Review + create**, then **Create**

#### Task 3: Create Policy Initiative (Policy Set)

1. In **Policy**, go to **Definitions**
2. Click **+ Initiative definition**
3. Configure:
    - Definition location: Your subscription
    - Name: `security-baseline`
    - Category: Custom Policies
4. Add policies:
    - "Audit VMs without managed disks"
    - "Require a tag on resources"
    - "Allowed locations"
    - Your custom tag policy
5. Click **Save**

#### Task 4: Assign Policy Initiative to Subscription

1. Navigate to **Policy** > **Assignments**
2. Click **Assign initiative**
3. Configure:
    - Scope: Your subscription
    - Initiative definition: `security-baseline`
    - Assignment name: `Security-Baseline-Policy`
4. Configure parameters for each policy
5. Click **Review + create**, then **Create**

#### Task 5: Test Policy Enforcement

1. Navigate to **Virtual machines**
2. Click **Create**
3. Try to create VM in non-allowed region (e.g., North Europe)
4. Observe policy denial
5. Try to create VM without Environment tag
6. Observe policy denial
7. Create VM with proper location and tags
8. Verify creation succeeds

#### Task 6: Review Policy Compliance

1. Navigate to **Policy** > **Compliance**
2. Review overall compliance score
3. Click on `Security-Baseline-Policy` assignment
4. Review compliant and non-compliant resources
5. Click on non-compliant resource
6. Review compliance details and remediation options

#### Task 7: Create Remediation Tasks

1. In **Policy** > **Compliance**, select a non-compliant policy
2. Click **Create remediation task**
3. Configure:
    - Policy to remediate: Select non-compliant policy
    - Scope: Select specific resources or entire scope
4. Click **Remediate**
5. Monitor remediation progress in **Remediation** tab

#### Task 8: Configure Policy Exemptions

1. Navigate to **Policy** > **Remediation**
2. Click **Policy exemptions**
3. Click **+ Add exemption**
4. Configure:
    - Scope: Select specific resource group or resource
    - Policy assignment: Select assignment to exempt
    - Exemption category: Waiver
    - Expires on: Set expiration date
    - Justification: Provide reason
5. Click **Review + create**, then **Create**

#### Task 9: Create Azure Blueprints

1. Navigate to **Blueprints**
2. Click **+ Create blueprint**
3. Configure:
    - Blueprint name: `security-compliant-environment`
    - Blueprint location: Your subscription
4. Click **Next: Artifacts**
5. Add artifacts:
    - Add policy assignment: `security-baseline`
    - Add resource group: `rg-secure-baseline`
    - Add role assignment: Security Reader
6. Click **Save draft**

#### Task 10: Publish and Assign Blueprint

1. In **Blueprints**, select your blueprint
2. Click **Publish blueprint**
3. Enter version: `1.0`
4. Click **Publish**
5. Click **Assign blueprint**
6. Configure:
    - Assignment name: `security-environment-prod`
    - Location: East US
    - Parameters: Fill required values
7. Click **Assign**
8. Monitor assignment status

#### Task 11: Configure Resource Locks

1. Navigate to a critical resource (e.g., storage account)
2. Go to **Locks** under Settings
3. Click **+ Add**
4. Configure:
    - Lock name: `prevent-deletion`
    - Lock type: **Delete**
    - Notes: "Critical production resource"
5. Click **OK**
6. Test by attempting to delete resource
7. Verify deletion is blocked

#### Task 12: Monitor Compliance with Azure Policy Insights

1. Navigate to **Policy** > **Compliance**
2. Click **Download** to export compliance report
3. Review report in Excel/CSV
4. Navigate to **Monitor** > **Activity Log**
5. Filter by:
    - Category: Policy
    - Time range: Last 24 hours
6. Review policy evaluation events
7. Identify denied operations due to policies

**Key Takeaways:**

- Azure Policy enforces organizational standards
- Custom policies extend built-in capabilities
- Policy initiatives group related policies
- Compliance dashboard shows adherence status
- Remediation tasks fix non-compliant resources
- Exemptions provide controlled exceptions
- Blueprints deploy consistent environments
- Resource locks prevent accidental deletion
- Activity logs track policy enforcement

**Troubleshooting:**

- **Issue:** Policy not enforcing on existing resources
  - **Solution:** Policy only applies to new operations; create remediation task for existing resources

- **Issue:** Blueprint assignment fails
  - **Solution:** Verify necessary permissions; check for conflicting policies or locks

- **Issue:** Compliance data not updating
  - **Solution:** Wait 15-30 minutes for evaluation cycle; trigger manual evaluation

### Cleanup

1. Delete policy assignments
2. Delete custom policy definitions
3. Delete policy initiatives
4. Remove resource locks
5. Delete blueprint assignments
6. Delete blueprints

---

## Lab 6: Container Security

**Objective:** Secure Azure Kubernetes Service (AKS) and container images with Azure Container Registry

**Estimated Duration:** 60 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Basic knowledge of containers and Kubernetes
- Azure CLI or Cloud Shell access

### Step-by-Step Instructions

#### Task 1: Create Azure Container Registry (ACR)

1. Navigate to **Container registries**
2. Click **Create**
3. Configure:
    - Resource Group: Create new "az500-container-lab"
    - Registry name: `acrsecure[random]`
    - Location: East US
    - SKU: Standard
4. Click **Review + create**, then **Create**

#### Task 2: Enable Azure Defender for Container Registries

1. Navigate to created ACR
2. Go to **Microsoft Defender for Cloud**
3. Click **Enable Microsoft Defender for container registries**
4. Verify protection is active
5. Navigate to **Security** > **Vulnerability scanning**
6. Verify scanning is enabled

#### Task 3: Push Container Image to ACR

1. Open **Cloud Shell** or Azure CLI
2. Authenticate to ACR:

```bash
az acr login --name acrsecure[random]
```

3. Pull sample image:

```bash
docker pull nginx:latest
```

4. Tag image for ACR:

```bash
docker tag nginx:latest acrsecure[random].azurecr.io/nginx:v1
```

5. Push to ACR:

```bash
docker push acrsecure[random].azurecr.io/nginx:v1
```

6. Verify image in ACR portal

#### Task 4: Review Container Image Vulnerabilities

1. In ACR, go to **Repositories**
2. Click on **nginx** repository
3. Click on **v1** tag
4. Review **Security** tab
5. Examine detected vulnerabilities
6. Review severity levels and remediation guidance

#### Task 5: Create Azure Kubernetes Service (AKS) Cluster

1. Navigate to **Kubernetes services**
2. Click **Create**
3. Configure:
    - Resource Group: az500-container-lab
    - Cluster name: `aks-secure`
    - Region: East US
    - Kubernetes version: Latest stable
    - Node count: 2
4. Click **Next: Node pools**
5. Review settings (keep defaults)
6. Click **Next: Authentication**
7. Enable **Azure Active Directory** authentication
8. Enable **Azure RBAC** for Kubernetes authorization
9. Click **Next: Networking**
10. Select **Azure CNI** networking
11. Enable **Network policy**: Azure
12. Click **Review + create**, then **Create**
13. Wait for deployment (10-15 minutes)

#### Task 6: Integrate AKS with ACR

1. Navigate to created AKS cluster
2. Go to **Settings** > **Properties**
3. Note the cluster's managed identity
4. Navigate to your ACR
5. Go to **Access control (IAM)**
6. Click **+ Add role assignment**
7. Select role: **AcrPull**
8. Assign access to: **Managed identity**
9. Select AKS cluster's identity
10. Click **Save**

#### Task 7: Configure Azure Policy for AKS

1. Navigate to AKS cluster
2. Go to **Policies** under Settings
3. Click **Enable Azure Policy**
4. Wait for add-on installation
5. Navigate to **Policy** in Azure Portal
6. Search for "Kubernetes" policies
7. Assign policy: "Kubernetes cluster containers should not use forbidden images"
8. Configure parameters:
    - Forbidden image patterns: `*:latest`
9. Click **Review + create**, then **Create**

#### Task 8: Deploy Secured Application to AKS

1. Connect to AKS cluster:

```bash
az aks get-credentials --resource-group az500-container-lab --name aks-secure
```

2. Create namespace:

```bash
kubectl create namespace secure-apps
```

3. Create deployment YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-secure
  namespace: secure-apps
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: acrsecure[random].azurecr.io/nginx:v1
        ports:
        - containerPort: 80
        securityContext:
          runAsNonRoot: true
          readOnlyRootFilesystem: true
          allowPrivilegeEscalation: false
```

4. Apply deployment:

```bash
kubectl apply -f deployment.yaml
```

5. Verify pods are running:

```bash
kubectl get pods -n secure-apps
```

#### Task 9: Configure Pod Security Standards

1. Create Pod Security Policy:

```yaml
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: restricted
spec:
  privileged: false
  allowPrivilegeEscalation: false
  requiredDropCapabilities:
    - ALL
  volumes:
    - 'configMap'
    - 'emptyDir'
    - 'secret'
  runAsUser:
    rule: 'MustRunAsNonRoot'
  seLinux:
    rule: 'RunAsAny'
  fsGroup:
    rule: 'RunAsAny'
```

2. Apply policy:

```bash
kubectl apply -f pod-security-policy.yaml
```

3. Test by attempting to create privileged pod
4. Verify policy blocks privileged containers

#### Task 10: Enable AKS Monitoring and Logging

1. Navigate to AKS cluster
2. Go to **Insights** under Monitoring
3. Click **Configure monitoring**
4. Select or create Log Analytics workspace
5. Click **Configure**
6. Wait for Container Insights to deploy
7. Review cluster performance metrics
8. Navigate to **Logs**
9. Query container logs:

```kusto
ContainerLog
| where Namespace == "secure-apps"
| order by TimeGenerated desc
| take 100
```

#### Task 11: Configure Network Policies

1. Create network policy YAML:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all-ingress
  namespace: secure-apps
spec:
  podSelector: {}
  policyTypes:
  - Ingress
```

2. Apply policy:

```bash
kubectl apply -f network-policy.yaml
```

3. Create policy to allow specific traffic:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-nginx-ingress
  namespace: secure-apps
spec:
  podSelector:
    matchLabels:
      app: nginx
  policyTypes:
  - Ingress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: ingress-nginx
    ports:
    - protocol: TCP
      port: 80
```

4. Apply policy and test connectivity

#### Task 12: Configure Secret Management with Key Vault

1. Navigate to **Key vaults**
2. Create new Key Vault:
    - Resource Group: az500-container-lab
    - Name: `kv-aks-[random]`
3. Create secret:
    - Name: `db-password`
    - Value: `SecureP@ssw0rd123`
4. Enable AKS integration:

```bash
az aks enable-addons --addons azure-keyvault-secrets-provider --name aks-secure --resource-group az500-container-lab
```

5. Create pod with Key Vault secret:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: app-with-secret
  namespace: secure-apps
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - name: secrets-store
      mountPath: "/mnt/secrets-store"
      readOnly: true
  volumes:
  - name: secrets-store
    csi:
      driver: secrets-store.csi.k8s.io
      readOnly: true
      volumeAttributes:
        secretProviderClass: "azure-keyvault"
```

6. Apply and verify secret mounting

**Key Takeaways:**

- ACR provides secure container image storage
- Image scanning detects vulnerabilities automatically
- AKS integration with Azure AD enables RBAC
- Azure Policy enforces container security standards
- Pod Security Policies prevent privileged containers
- Network policies control pod-to-pod communication
- Container Insights monitors cluster health
- Key Vault integration secures application secrets
- Azure CNI provides advanced networking features

**Troubleshooting:**

- **Issue:** Cannot pull images from ACR
  - **Solution:** Verify AcrPull role assignment; check ACR authentication

- **Issue:** Azure Policy not blocking non-compliant pods
  - **Solution:** Wait 5-10 minutes for policy add-on sync; verify policy is enabled

- **Issue:** Container Insights not showing data
  - **Solution:** Verify Log Analytics workspace connection; wait 10-15 minutes for initial data

### Cleanup

1. Delete AKS cluster
2. Delete Container Registry
3. Delete Key Vault
4. Delete resource group "az500-container-lab"

---

## Lab 7: Backup & Disaster Recovery

**Objective:** Implement Azure Backup, Site Recovery, and business continuity strategies

**Estimated Duration:** 55 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Virtual machines from previous labs (or create new ones)

### Step-by-Step Instructions

#### Task 1: Create Recovery Services Vault

1. Navigate to **Recovery Services vaults**
2. Click **Create**
3. Configure:
    - Resource Group: Create new "az500-bcdr-lab"
    - Vault name: `rsv-backup`
    - Region: East US
4. Click **Review + create**, then **Create**

#### Task 2: Configure Backup for Virtual Machines

1. Navigate to created Recovery Services vault
2. Go to **Backup** under Getting Started
3. Configure:
    - Where is your workload running: **Azure**
    - What do you want to backup: **Virtual machine**
4. Click **Backup**
5. Create backup policy:
    - Policy name: `daily-vm-backup`
    - Backup schedule: Daily at 10:00 PM
    - Retention: 30 days
6. Click **Enable Backup**
7. Select VMs to backup
8. Click **OK**

#### Task 3: Perform On-Demand Backup

1. In Recovery Services vault, go to **Backup items**
2. Click **Azure Virtual Machine**
3. Select a VM
4. Click **Backup now**
5. Specify retention: Until (30 days from today)
6. Click **OK**
7. Monitor backup job in **Backup jobs**

#### Task 4: Test VM Restore

1. In Recovery Services vault, go to **Backup items** > **Azure Virtual Machine**
2. Select backed up VM
3. Click **Restore VM**
4. Select restore point
5. Configure restore:
    - Restore Type: **Create new virtual machine**
    - Virtual machine name: `vm-restored`
    - Resource group: az500-bcdr-lab
    - Virtual network: Select existing or create new
    - Staging Location: Create new storage account
6. Click **Restore**
7. Monitor restore operation
8. Verify restored VM functionality

#### Task 5: Configure File-Level Recovery

1. In Recovery Services vault, go to **Backup items** > **Azure Virtual Machine**
2. Select VM
3. Click **File Recovery**
4. Select recovery point
5. Click **Download Executable** (for Windows) or **Download Script** (for Linux)
6. Run on target machine to mount backup
7. Browse and copy files as needed
8. Unmount when complete

#### Task 6: Configure Azure Site Recovery

1. In Recovery Services vault, go to **Site Recovery**
2. Click **Prepare infrastructure**
3. Configure:
    - Protection goal: **To Azure**
    - Are your machines virtualized: **Not virtualized/Other**
4. Click **OK**
5. Set up target region: West US
6. Click **Review + Start replication**

#### Task 7: Enable Replication for VMs

1. In Site Recovery, click **Replicate**
2. Configure:
    - Source location: East US
    - Azure virtual machine deployment model: Resource Manager
3. Click **Next: Virtual machines**
4. Select VMs to replicate
5. Click **Next: Replication settings**
6. Configure:
    - Target location: West US
    - Target resource group: Create new
    - Target virtual network: Create new
    - Cache storage account: Create new
    - Replication policy: Create new "24-hour-retention-policy"
7. Click **Enable replication**
8. Monitor replication status

#### Task 8: Test Disaster Recovery Failover

1. In Site Recovery, go to **Replicated items**
2. Select replicated VM
3. Verify replication health is healthy
4. Click **Test failover**
5. Configure:
    - Recovery point: Latest processed
    - Azure virtual network: Select test network
6. Click **OK**
7. Monitor failover progress
8. After completion, validate failover VM
9. Click **Cleanup test failover**
10. Confirm cleanup

#### Task 9: Create Recovery Plan

1. In Site Recovery, go to **Recovery Plans**
2. Click **+ Recovery plan**
3. Configure:
    - Name: `app-tier-recovery`
    - Source: East US
    - Target: West US
4. Click **Select items**
5. Add VMs in order of dependency:
    - Database VMs
    - Application VMs
    - Web VMs
6. Click **OK**
7. Click **Customize** to add pre/post actions
8. Save recovery plan

#### Task 10: Configure Backup for SQL Databases

1. Create Azure SQL Database (if not exists)
2. Navigate to SQL server
3. Go to **Automated backups**
4. Verify automatic backups are enabled
5. Configure retention:
    - Point-in-time retention: 35 days
    - Long-term retention: Monthly backups for 12 months
6. Click **Apply**

#### Task 11: Test SQL Database Restore

1. Navigate to SQL database
2. Click **Restore**
3. Select restore point
4. Configure:
    - Source: Point-in-time restore
    - Restore point: Select specific time
    - Database name: `db-restored`
5. Click **Review + create**, then **Create**
6. Verify restored database

#### Task 12: Configure Geo-Replication for SQL

1. Navigate to SQL database
2. Go to **Replicas** under Data management
3. Click **Create replica**
4. Configure:
    - Server: Create new in West US
    - Server name: `sql-replica-[random]`
    - Compute + storage: Match primary
5. Click **Review + create**, then **Create**
6. Monitor geo-replication status
7. Test failover:
    - Click on replica
    - Click **Forced failover**
    - Confirm failover
8. Verify application connectivity

**Key Takeaways:**

- Recovery Services vault centralizes backup and disaster recovery
- Azure Backup protects VMs, files, and databases
- File-level recovery enables granular restores
- Site Recovery provides automated disaster recovery
- Test failovers validate DR plans without impact
- Recovery plans orchestrate multi-tier failovers
- SQL automatic backups provide point-in-time restore
- Geo-replication provides regional redundancy
- Regular testing ensures recovery objectives are met

**Troubleshooting:**

- **Issue:** Backup job fails
  - **Solution:** Check VM agent status; verify network connectivity; review backup job logs

- **Issue:** Replication not starting
  - **Solution:** Verify required permissions; check network connectivity; ensure sufficient resources in target region

- **Issue:** SQL geo-replication lag
  - **Solution:** Check network latency; verify compute tier matches workload; monitor replication metrics

### Cleanup

1. Stop replication for VMs
2. Delete replicated items
3. Delete recovery plans
4. Delete SQL geo-replicas
5. Delete restored VMs and databases
6. Delete Recovery Services vault
7. Delete resource group "az500-bcdr-lab"

---

## Lab 8: Identity Protection & Risk Management

**Objective:** Configure Azure AD Identity Protection, risk policies, and conditional access scenarios

**Estimated Duration:** 50 minutes

**Prerequisites:**

- Azure AD Premium P2 license
- Global Administrator or Security Administrator role
- Test user accounts

### Step-by-Step Instructions

#### Task 1: Enable Azure AD Identity Protection

1. Navigate to **Azure Active Directory**
2. Go to **Security** > **Identity Protection**
3. Verify Identity Protection is available
4. Review dashboard showing risk detections

#### Task 2: Configure User Risk Policy

1. In Identity Protection, go to **User risk policy**
2. Click **Configure policy** or edit existing
3. Configure:
    - Assignments:
      - Users: All users (exclude break-glass accounts)
      - User risk: Medium and above
    - Controls:
      - Access: Require password change
4. Enforce policy: **On**
5. Click **Save**

#### Task 3: Configure Sign-in Risk Policy

1. In Identity Protection, go to **Sign-in risk policy**
2. Configure:
    - Assignments:
      - Users: All users
      - Sign-in risk: Medium and above
    - Controls:
      - Access: Require multi-factor authentication
4. Enforce policy: **On**
5. Click **Save**

#### Task 4: Review Risk Detections

1. In Identity Protection, go to **Risk detections**
2. Review detected risks:
    - Atypical travel
    - Anonymous IP address
    - Unfamiliar sign-in properties
    - Leaked credentials
3. Click on a detection to view details
4. Review user, location, IP, and risk level

#### Task 5: Investigate Risky Users

1. In Identity Protection, go to **Risky users**
2. Review users flagged as risky
3. Click on a user
4. Review risk history and detections
5. Take action:
    - **Confirm user compromised** (if confirmed)
    - **Dismiss user risk** (if false positive)
    - **Require password reset**

#### Task 6: Simulate Risky Sign-in

1. Download Tor Browser (anonymous browsing)
2. Navigate to <https://portal.azure.com>
3. Sign in with test user account
4. Complete MFA if prompted
5. Wait 5-10 minutes
6. Check Identity Protection for anonymous IP detection

#### Task 7: Configure Conditional Access with Risk

1. Navigate to **Azure AD** > **Security** > **Conditional Access**
2. Click **+ New policy**
3. Configure:
    - Name: `Block-High-Risk-Signins`
    - Users: All users
    - Cloud apps: All cloud apps
    - Conditions:
      - Sign-in risk: High
    - Access controls:
      - Block access
4. Enable policy: **Report-only** (test first)
5. Click **Create**

#### Task 8: Test Risk-Based Conditional Access

1. Use Tor Browser to sign in as test user
2. Observe sign-in risk evaluation
3. Verify MFA is required (medium risk)
4. Attempt sign-in from suspicious location
5. If high risk, observe blocked access
6. Review sign-in logs in Azure AD

#### Task 9: Configure MFA Registration Policy

1. In Identity Protection, go to **MFA registration policy**
2. Configure:
    - Assignments: All users
    - Require: Azure AD Multi-Factor Authentication registration
3. Enforce policy: **On**
4. Click **Save**
5. Test with new user account
6. Verify MFA registration is required on first sign-in

#### Task 10: Implement Location-Based Access

1. Navigate to **Conditional Access**
2. Click **Named locations**
3. Click **+ Countries location**
4. Configure:
    - Name: `Blocked-Countries`
    - Select countries to block (e.g., high-risk regions)
5. Click **Create**
6. Create new conditional access policy:
    - Name: `Block-Untrusted-Locations`
    - Conditions > Locations: Any location, exclude trusted
    - Access controls: Block access
7. Enable policy: **On**

#### Task 11: Configure Device-Based Conditional Access

1. In Conditional Access, create new policy
2. Configure:
    - Name: `Require-Compliant-Device`
    - Users: All users
    - Cloud apps: Office 365
    - Conditions > Device platforms: All
    - Grant: Require device to be marked as compliant
3. Enable policy: **Report-only**
4. Click **Create**
5. Monitor impact in **What If** tool

#### Task 12: Create Risk Event Remediation Workflow

1. Navigate to **Azure AD** > **Security** > **Risky users**
2. Configure notification:
    - Go to **Settings** > **Alerts**
    - Add email recipients for risk alerts
    - Set threshold: High risk
3. Create remediation playbook:
    - Document steps for investigating risky users
    - Define approval process for risk dismissal
    - Establish timeline for password reset
4. Test workflow with simulated risk event

**Key Takeaways:**

- Identity Protection detects identity-based risks automatically
- Risk policies enforce adaptive authentication
- User risk indicates compromised credentials
- Sign-in risk indicates suspicious authentication attempts
- Conditional access integrates with risk detection
- Location-based policies restrict access by geography
- Device compliance enforces security baselines
- Risk remediation requires investigation process
- Report-only mode tests policies before enforcement

**Troubleshooting:**

- **Issue:** Risk detections not appearing
  - **Solution:** Wait 24 hours for learning period; ensure Azure AD Premium P2 license

- **Issue:** Policy not triggering for risky sign-in
  - **Solution:** Verify policy assignment scope; check policy is enabled not report-only

- **Issue:** Cannot dismiss user risk
  - **Solution:** Verify Security Administrator role; check if risk is manually confirmed

### Cleanup

1. Disable user risk policy
2. Disable sign-in risk policy
3. Dismiss all test user risks
4. Delete test conditional access policies
5. Delete named locations
6. Remove test user accounts

---

## Lab 9: Application Gateway & WAF

**Objective:** Deploy Application Gateway with Web Application Firewall for application security

**Estimated Duration:** 60 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Web application or test VMs to protect

### Step-by-Step Instructions

#### Task 1: Create Virtual Network for Application Gateway

1. Navigate to **Virtual networks**
2. Click **Create**
3. Configure:
    - Resource Group: Create new "az500-appgw-lab"
    - Name: `vnet-appgw`
    - Region: East US
    - IPv4 address space: 10.2.0.0/16
4. Click **Next: IP Addresses**
5. Add subnets:
    - `subnet-appgw` (10.2.0.0/24) - for Application Gateway
    - `subnet-backend` (10.2.1.0/24) - for backend servers
6. Click **Review + create**, then **Create**

#### Task 2: Create Backend Web Servers

1. Navigate to **Virtual machines**
2. Click **Create** > **Azure virtual machine**
3. Configure VM 1:
    - Resource Group: az500-appgw-lab
    - Name: `vm-web1`
    - Region: East US
    - Image: Windows Server 2022
    - Size: Standard B2s
    - Administrator account: Create username/password
    - Networking: `vnet-appgw`, `subnet-backend`
    - Public IP: None
4. Click **Review + create**, then **Create**
5. Repeat to create `vm-web2` in same subnet

#### Task 3: Install IIS on Backend Servers

1. After VM deployment, connect to `vm-web1` via Bastion or RDP
2. Open PowerShell as Administrator
3. Install IIS:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

4. Create custom page:

```powershell
Set-Content -Path C:\inetpub\wwwroot\index.html -Value "<h1>Server 1 - $(hostname)</h1>"
```

5. Repeat steps for `vm-web2`
6. Verify IIS responds on both servers

#### Task 4: Create Application Gateway with WAF

1. Navigate to **Application gateways**
2. Click **Create**
3. Configure basics:
    - Resource Group: az500-appgw-lab
    - Name: `appgw-waf`
    - Region: East US
    - Tier: **WAF V2**
    - Enable autoscaling: Yes (min 2, max 10)
    - Availability zone: Zones 1, 2, 3
4. Click **Next: Frontends**
5. Configure frontend:
    - IP address type: Public
    - Public IP: Create new `appgw-pip`
6. Click **Next: Backends**
7. Add backend pool:
    - Name: `backend-pool-web`
    - Add target: Select `vm-web1` and `vm-web2` by IP
8. Click **Next: Configuration**
9. Add routing rule:
    - Rule name: `http-rule`
    - Priority: 100
    - Listener:
      - Name: `http-listener`
      - Frontend IP: Public
      - Protocol: HTTP
      - Port: 80
    - Backend targets:
      - Target type: Backend pool
      - Backend pool: `backend-pool-web`
      - HTTP settings: Create new
        - Name: `http-settings`
        - Protocol: HTTP
        - Port: 80
10. Click **Review + create**, then **Create**
11. Wait for deployment (10-15 minutes)

#### Task 5: Configure WAF Policy

1. Navigate to **Web Application Firewall policies**
2. Click **Create**
3. Configure:
    - Resource Group: az500-appgw-lab
    - Policy name: `waf-policy-production`
    - Region: East US
4. Click **Next: Policy settings**
5. Configure:
    - Mode: **Prevention**
    - Request body inspection: Enabled
    - Max request body size: 128 KB
6. Click **Next: Managed rules**
7. Enable rule sets:
    - OWASP 3.2 (or latest)
    - Microsoft_BotManagerRuleSet_1.0
8. Click **Next: Custom rules**
9. Add custom rule:
    - Name: `block-suspicious-ua`
    - Priority: 1
    - Match type: String
    - Match variable: RequestHeaders (User-Agent)
    - Operator: Contains
    - Match values: `badbot`, `scanner`
    - Action: Block
10. Click **Review + create**, then **Create**

#### Task 6: Associate WAF Policy with Application Gateway

1. Navigate to created Application Gateway
2. Go to **Web application firewall**
3. Click **Associate policy**
4. Select `waf-policy-production`
5. Click **Save**
6. Wait for association to complete

#### Task 7: Test Application Gateway Functionality

1. Navigate to Application Gateway
2. Copy frontend public IP address
3. Open browser and navigate to `http://[public-ip]`
4. Verify backend servers respond
5. Refresh multiple times to see load balancing
6. Verify both servers are serving traffic

#### Task 8: Test WAF Protection

1. Test SQL injection:

```bash
http://[public-ip]/?id=1' OR '1'='1
```

2. Observe WAF blocks request (403 Forbidden)
3. Test XSS attack:

```bash
http://[public-ip]/?search=<script>alert('xss')</script>
```

4. Verify request is blocked
5. Test path traversal:

```bash
http://[public-ip]/../../../etc/passwd
```

6. Confirm WAF protection

#### Task 9: Configure WAF Exclusions

1. Navigate to WAF policy
2. Go to **Exclusions**
3. Add exclusion:
    - Match variable: Request header
    - Selector: User-Agent
    - Exclusion rule set: Select specific rules to exclude
4. Click **Save**
5. Test that legitimate traffic with excluded pattern passes

#### Task 10: Review WAF Logs and Metrics

1. Navigate to Application Gateway
2. Go to **Diagnostic settings**
3. Click **+ Add diagnostic setting**
4. Configure:
    - Name: `waf-diagnostics`
    - Logs: ApplicationGatewayFirewallLog, ApplicationGatewayAccessLog
    - Destination: Send to Log Analytics workspace
5. Click **Save**
6. Wait 10-15 minutes for logs
7. Query WAF logs:

```kusto
AzureDiagnostics
| where ResourceType == "APPLICATIONGATEWAYS"
| where Category == "ApplicationGatewayFirewallLog"
| order by TimeGenerated desc
```

8. Review blocked requests

#### Task 11: Configure Health Probes

1. Navigate to Application Gateway
2. Go to **Health probes**
3. Click **+ Add**
4. Configure:
    - Name: `health-probe-http`
    - Protocol: HTTP
    - Host: Leave empty (use backend address)
    - Path: `/`
    - Interval: 30 seconds
    - Timeout: 30 seconds
    - Unhealthy threshold: 3
5. Click **Add**
6. Associate with backend HTTP settings
7. Monitor backend health in **Backend health**

#### Task 12: Implement SSL/TLS Termination

1. Obtain SSL certificate (self-signed for testing):

```powershell
$cert = New-SelfSignedCertificate -DnsName "appgw.contoso.com" -CertStoreLocation "cert:\LocalMachine\My"
Export-PfxCertificate -Cert $cert -FilePath "appgw-cert.pfx" -Password (ConvertTo-SecureString -String "P@ssw0rd123" -Force -AsPlainText)
```

2. Navigate to Application Gateway > **Listeners**
3. Add new listener:
    - Name: `https-listener`
    - Protocol: HTTPS
    - Port: 443
    - Certificate: Upload `appgw-cert.pfx`
4. Create routing rule for HTTPS listener
5. Test HTTPS access: `https://[public-ip]`

**Key Takeaways:**

- Application Gateway provides layer 7 load balancing
- WAF protects against OWASP Top 10 vulnerabilities
- Prevention mode actively blocks malicious requests
- Custom rules extend default protection
- Exclusions reduce false positives
- Health probes monitor backend availability
- SSL termination offloads encryption from backend
- Diagnostic logs enable security monitoring
- Autoscaling handles variable traffic loads

**Troubleshooting:**

- **Issue:** Backend servers marked unhealthy
  - **Solution:** Verify NSG allows traffic from Application Gateway subnet; check health probe path

- **Issue:** Legitimate requests blocked by WAF
  - **Solution:** Review logs to identify triggered rules; add exclusions or tune rule sensitivity

- **Issue:** SSL handshake fails
  - **Solution:** Verify certificate is valid and properly formatted; check certificate password

### Cleanup

1. Delete Application Gateway
2. Delete WAF policy
3. Delete backend VMs
4. Delete public IP addresses
5. Delete virtual network
6. Delete resource group "az500-appgw-lab"

---

## Lab 10: Security Center Automation

**Objective:** Implement automated security responses using Logic Apps and Azure Automation

**Estimated Duration:** 55 minutes

**Prerequisites:**

- Azure subscription with contributor access
- Microsoft Defender for Cloud enabled
- Previous labs completed (for resources to monitor)

### Step-by-Step Instructions

#### Task 1: Create Log Analytics Workspace for Automation

1. Navigate to **Log Analytics workspaces**
2. Click **Create**
3. Configure:
    - Resource Group: Create new "az500-automation-lab"
    - Name: `law-automation`
    - Region: East US
4. Click **Review + create**, then **Create**

#### Task 2: Create Automation Account

1. Navigate to **Automation Accounts**
2. Click **Create**
3. Configure:
    - Resource Group: az500-automation-lab
    - Name: `aa-security-automation`
    - Region: East US
4. Click **Review + create**, then **Create**
5. After creation, navigate to account
6. Go to **Identity** under Account Settings
7. Enable **System assigned** managed identity
8. Click **Save**

#### Task 3: Create Runbook for Security Remediation

1. In Automation Account, go to **Runbooks**
2. Click **+ Create a runbook**
3. Configure:
    - Name: `Remediate-OpenPorts`
    - Runbook type: PowerShell
    - Runtime version: 7.1
4. Click **Create**
5. Add runbook code:

```powershell
param(
    [Parameter(Mandatory=$true)]
    [string]$ResourceGroupName,
    [Parameter(Mandatory=$true)]
    [string]$NSGName
)

# Authenticate using managed identity
Connect-AzAccount -Identity

# Get NSG
$nsg = Get-AzNetworkSecurityGroup -ResourceGroupName $ResourceGroupName -Name $NSGName

# Remove rules allowing RDP/SSH from internet
$nsg.SecurityRules | Where-Object {
    $_.Access -eq 'Allow' -and
    $_.Direction -eq 'Inbound' -and
    $_.SourceAddressPrefix -eq '*' -and
    ($_.DestinationPortRange -contains '22' -or $_.DestinationPortRange -contains '3389')
} | ForEach-Object {
    Write-Output "Removing rule: $($_.Name)"
    Remove-AzNetworkSecurityRuleConfig -Name $_.Name -NetworkSecurityGroup $nsg
}

# Apply changes
$nsg | Set-AzNetworkSecurityGroup

Write-Output "Remediation complete for NSG: $NSGName"
```

6. Click **Save**
7. Click **Publish**

#### Task 4: Assign Permissions to Automation Account

1. Navigate to subscription or resource group
2. Go to **Access control (IAM)**
3. Click **+ Add role assignment**
4. Select role: **Network Contributor**
5. Assign access to: **Managed identity**
6. Select Automation Account's managed identity
7. Click **Save**

#### Task 5: Create Logic App for Alert Response

1. Navigate to **Logic Apps**
2. Click **Add**
3. Configure:
    - Resource Group: az500-automation-lab
    - Type: **Consumption**
    - Name: `logic-security-alert-response`
    - Region: East US
4. Click **Review + create**, then **Create**
5. After creation, click **Go to resource**
6. Click **Logic app designer**

#### Task 6: Configure Logic App Trigger

1. In designer, search for "Microsoft Defender for Cloud"
2. Select trigger: **When a Microsoft Defender for Cloud Alert is created or triggered**
3. Sign in with credentials
4. Configure trigger:
    - Severity: Select "High"
5. Click **+ New step**

#### Task 7: Add Logic App Actions

1. Add action: **Azure Automation - Create job**
2. Configure:
    - Subscription: Your subscription
    - Resource Group: az500-automation-lab
    - Automation Account: aa-security-automation
    - Runbook: Remediate-OpenPorts
    - Parameters:
      - ResourceGroupName: Extract from alert (use expressions)
      - NSGName: Extract from alert
3. Click **+ New step**
4. Add action: **Send an email (V2)**
5. Configure:
    - To: Your email
    - Subject: `Security Alert Remediated: @{triggerBody()?['AlertDisplayName']}`
    - Body: Include alert details and remediation status
6. Click **Save**

#### Task 8: Test Logic App with Simulated Alert

1. Create NSG with open port for testing
2. Wait for Defender for Cloud to detect
3. Navigate to Defender for Cloud > **Security alerts**
4. Trigger alert or wait for automatic detection
5. Monitor Logic App execution:
    - Go to Logic App > **Runs history**
    - Click on run to see execution details
6. Verify runbook executed successfully
7. Confirm email notification received

#### Task 9: Create Workflow Automation in Defender for Cloud

1. Navigate to **Microsoft Defender for Cloud**
2. Go to **Workflow automation** under Management
3. Click **+ Add workflow automation**
4. Configure:
    - Name: `Auto-Remediate-High-Severity`
    - Resource Group: az500-automation-lab
    - Trigger conditions:
      - Alert severity: High
      - Alert type: Select specific types
    - Actions:
      - Select Logic App: `logic-security-alert-response`
5. Click **Create**

#### Task 10: Create Automation for Resource Compliance

1. In Automation Account, create new runbook:
    - Name: `Enforce-TagCompliance`
    - Type: PowerShell
2. Add code:

```powershell
param(
    [Parameter(Mandatory=$true)]
    [string]$ResourceGroupName
)

Connect-AzAccount -Identity

# Get all resources without required tags
$resources = Get-AzResource -ResourceGroupName $ResourceGroupName | Where-Object {
    -not $_.Tags -or -not $_.Tags.ContainsKey('Environment')
}

foreach ($resource in $resources) {
    Write-Output "Adding tag to resource: $($resource.Name)"
    $tags = if ($resource.Tags) { $resource.Tags } else { @{} }
    $tags['Environment'] = 'Untagged'
    Set-AzResource -ResourceId $resource.ResourceId -Tag $tags -Force
}

Write-Output "Tag enforcement complete"
```

3. Publish runbook
4. Create schedule:
    - Navigate to runbook > **Schedules**
    - Click **+ Add a schedule**
    - Create schedule: Daily at 2:00 AM
    - Link to runbook

#### Task 11: Configure Alert Processing Rules

1. Navigate to **Monitor** > **Alerts**
2. Click **Alert processing rules**
3. Click **+ Create**
4. Configure:
    - Name: `Suppress-NonBusiness-Hours`
    - Scope: Your subscription
    - Filter:
      - Severity: Low, Informational
      - Time: Apply during non-business hours
    - Action: Suppress notifications
5. Click **Create**

#### Task 12: Create Custom Alert Query

1. Navigate to Log Analytics workspace
2. Go to **Logs**
3. Create custom query:

```kusto
SecurityAlert
| where TimeGenerated > ago(24h)
| where AlertSeverity == "High"
| summarize Count=count() by AlertName, CompromisedEntity
| order by Count desc
```

4. Click **+ New alert rule**
5. Configure:
    - Measurement: Table rows
    - Aggregation type: Count
    - Aggregation granularity: 5 minutes
    - Threshold: Greater than 0
6. Configure action group:
    - Create new action group
    - Add actions: Email, Logic App, Runbook
7. Click **Create alert rule**
8. Test by generating security events

**Key Takeaways:**

- Logic Apps enable automated response to security alerts
- Automation runbooks remediate security issues automatically
- Managed identity provides secure authentication for automation
- Workflow automation connects Defender alerts to Logic Apps
- Scheduled runbooks enforce continuous compliance
- Alert processing rules reduce alert fatigue
- Custom queries detect specific security conditions
- Email notifications keep security team informed
- Automated remediation reduces response time

**Troubleshooting:**

- **Issue:** Logic App fails to trigger
  - **Solution:** Verify workflow automation is enabled; check alert severity matches trigger

- **Issue:** Runbook authentication fails
  - **Solution:** Ensure managed identity is enabled and has necessary permissions

- **Issue:** Email notifications not received
  - **Solution:** Check email address in action group; verify email isn't in spam folder

### Cleanup

1. Delete workflow automation
2. Delete Logic Apps
3. Delete Automation Account and runbooks
4. Delete alert processing rules
5. Delete custom alert rules
6. Delete Log Analytics workspace
7. Delete resource group "az500-automation-lab"

---

## Summary

These ten comprehensive labs cover all Azure Security Engineer skills tested on the AZ-500 exam:

| Lab | Focus Area | Key Skills |
|-----|------------|------------|
| Lab 1 | Identity & Access Management | Azure AD, MFA, Conditional Access, PIM |
| Lab 2 | Platform Protection | NSGs, Azure Firewall, Service Endpoints |
| Lab 3 | Data & Application Security | Key Vault, SQL Security, Storage Encryption |
| Lab 4 | Security Operations | Defender for Cloud, Monitor, Sentinel |
| Lab 5 | Azure Policy & Compliance | Policy, Initiatives, Blueprints, Governance |
| Lab 6 | Container Security | AKS, ACR, Container Security |
| Lab 7 | Backup & Disaster Recovery | Azure Backup, Site Recovery, BCDR |
| Lab 8 | Identity Protection & Risk | Identity Protection, Risk Policies, Conditional Access |
| Lab 9 | Application Gateway & WAF | Application Gateway, WAF, Layer 7 Security |
| Lab 10 | Security Automation | Logic Apps, Automation, Workflow Orchestration |

**Total Lab Time:** ~550 minutes (9+ hours)

---

## Additional Resources

- [AZ-500 Exam Skills](https://learn.microsoft.com/en-us/certifications/exams/az-500/)
- [Azure Security Learning Path](https://learn.microsoft.com/en-us/training/paths/azure-security-engineer/)
- [Azure Security Documentation](https://learn.microsoft.com/en-us/azure/security/)

---

**Last Updated:** February 1, 2026

**Related:** [← Back to Student Resources](/README.md) | [AZ-500 Practice Test](../az500-practice-test.md) | [All Labs](../labs/)
