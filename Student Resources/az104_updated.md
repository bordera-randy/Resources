# AZ-104 Exam Resources

## Table of Contents
- [AZ-104 Exam Resources](#az-104-exam-resources)
  - [Table of Contents](#table-of-contents)
  - [Documentation](#documentation)
  - [Labs](#labs)
  - [Study Guides](#study-guides)
  - [Learning Modules](#learning-modules)
  - [Student Resources](#student-resources)

## Documentation
- [Microsoft Learn: AZ-104 Exam](https://learn.microsoft.com/en-us/certifications/exams/az-104)
- [Azure Administrator Documentation](https://learn.microsoft.com/en-us/training/courses/az-104t00)

## Labs
- [AZ-104 Labs](https://microsoftlearning.github.io/AZ-104-MicrosoftAzureAdministrator/)

## Study Guides
- [Exam AZ-104 Study Guide](https://learn.microsoft.com/en-us/certifications/resources/study-guides/az-104)
- [Whizlabs AZ-104 Study Guide](https://www.whizlabs.com/blog/az-104-exam-preparation-guide/)

## Learning Modules
- [Manage Azure identities and governance](https://learn.microsoft.com/en-us/training/modules/manage-azure-identities/)
- [Implement and manage storage](https://learn.microsoft.com/en-us/training/modules/implement-and-manage-storage/)
- [Deploy and manage Azure compute resources](https://learn.microsoft.com/en-us/training/modules/deploy-and-manage-azure-compute-resources/)
- [Configure and manage virtual networking](https://learn.microsoft.com/en-us/training/modules/configure-and-manage-virtual-networking/)
- [Monitor and back up Azure resources](https://learn.microsoft.com/en-us/training/modules/monitor-and-back-up-azure-resources/)

## Student Resources
- [Microsoft Learn: Student Hub](https://learn.microsoft.com/en-us/training/student-hub/)
- [Azure for Students](https://azure.microsoft.com/en-us/free/students/)



1.1. Management - Azure Cloud Shell
Azure Cloud Shell
 Browser-accessible shell for managing Azure resources
o Can provide Bash or PowerShell
 � In background it uses dockerized version of PowerShell / bash
 When you open it for the first time →
i. It creates a new storage account called azcloudshell and some numbers
ii. It then creates a file share that stores your user information.
1.2. Management - Resources & Costs.
Subscriptions
Resource tagging
 ��Always tag!
 Tags are additional metadata that can be assigned to resources/resource groups.
o ❗ Child resources do not inherit resource groups tags
o ❗ Max 15 tag name/value pairs.
 E.g. CostCenter = YHZ
 Why?
o Organize
o Search
o View
o Billing & cost managements
 On Portal
o You can search for Tags and see filtered lists.
o ❗ Resources are tagged after resource is created as opposed to PowerShell/CLI.
Resource Tagging and Cost Center Spending Limits
Spending Limits
 Applies to free trial subscriptions, MSDN and Visual Studio subscriptions.
o If spending limit is exceeded:
a. Email message is sent
pg. 2
SKILLCERTPRO
b. Deployed resources are disabled in next billing cycle.
c. Databases and storage accounts become read-only
o Free trials can be upgraded to Pay-as-you-go
 Do not apply to support plans, pay-as-you-go, Enterprise Dev/Test
ARM Consumption API
 Returns usage details
 ❗ Supported only in Enterprise enrollments and Web Direct subscriptions
 Available through CLI and different SDKs.
 Consumption APIs
o Enterprise customers only: Price Sheet, Budgets, Balance
o Reserved VMs: Reservation Summaries API, Reservation Details API, Reservation 
recommendations API
o Others: Marketplace charges, usage details
Azure Pricing Calculator
 Estimates monthly costs
 See online
Azure Advisor Cost Recomendations
 Identifies wastage
 E.g. idle VMs, SQL DBs.
o Can configure automatic shutdown
o Auto-shutdown option in VM.
 Recommendations about:
o High availability
o Security
o Performance
o Cost recommendations, e.g.:
 Virtual machine reserved instances to reduce costs.
 VM resizing: Scale up / down
 Remove unprovisioned ExpressRoute circuits.
 Configure rule:
o E.g. Average CPU Utilization < 5%
pg. 3
SKILLCERTPRO
Subscription blade
 In Cost analysis you can filter by Tags.
 Invoices
 Manage in Subscription blade
o Manage payment methods
 �� Adding one allows you to remove subscription limits.
o Download usage details
o Transfer/cancel subscription
o Set-up billing alerts
 E.g. e-mail if billing total is $150
Optimizing VM costs
 �� Use VM Reserved Instances
o You can create one in Reservations blade
 �� Set-up auto shutdown in VMs
o Auto-shutdown blade in VM.
Microsoft Azure Resource Providers
 Enables Azure features.
 Many are registered automatically
o E.g. Microsoft.Compute that handles 
VMs, Microsoft.Network, Microsoft.Sql, Microsoft.Storage
 Some are not registered automatically
o E.g. Microsoft.PolicyInsights, Microsoft.AzureActiveDirectory, Microsoft.Az
ureStack, Microsoft.Botservice
o Custom providers can be registered with subscription.
 Requires the Contributor or Owner roles.
 In most cases providers are registered automatically when you deploy 
resources that uses the providers.
 You can register, unregister, re-register through Subscription → Resource providers in 
Portal
1.3. Management - Resource Groups
pg. 4
SKILLCERTPRO
Resource groups
 Logical grouping of resources that shares the same lifecycles.
o Resource group holds different unique resources.
o Resource groups can contain resources that reside in different regions.
 Location of resource group is just the meta data for the resource group.
Tags
 Categorization / organization of resource groups for e.g. billing, management
 E.g. Dept: IT
 �� Tags are not inherited
 ❗ Max 15 tag name/value pairs.
Locks
 For accidental deletion or accidental changes to resources within a resource group.
 Consists of two locks:
o CanNotDelete
 Authorized users can still read and modify a resource, but they can't 
delete the resource.
o ReadOnly
 Authorized users can read a resource, but they can't delete or update the 
resource.
 Same as giving everyone a Reader role.
 Locks are inherited from resources within the resource group.
IAM
 Access control, RBAC
 Roles are inherited
 Role assignment: Role definition role (role, e.g. Reader) + Person/Scope/Service 
Principal + Scope
Policies
 Azure entity that controls behaviors within a resource group
o Allow you to keep compliant with corporate standards and SLAs.
o Set in a scope with a name and definition.
pg. 5
SKILLCERTPRO
 Scope: E.g. resource group, subscription.
 Definition: E.g. "Allow resource types"
 Name, description, Policy (e.g. azurepolicy.rules.json), 
Parameters (e.g. azurepolicy.parameters.json)
Events
 Create event subscriptions triggered by the resources group in Event Grid.
Automation Script
 Can be added to library to be redeployed later on.
o ❗ All resources cannot be redeployed
o �� Must change the name to avoid duplicates.
 ARM templates for resource groups can also be found on GitHub.
 You can Add to library, or click on Deploy to deploy directly.
Moving Resources
 You can move resources to another resource group or subscription.
 ❗ All resources cannot be moved.
 Ways of moving
o Using CLI: az resource move --destination-group new-rg --id resourceid
o In portal: Overview → Move
Alerts
1. Target: What resource and where
2. Criteria: What specific action
3. Details: Who, when, where, how
4. Action Group: Who to inform and how to inform them
Metrics
1. Resource group: Where to look at the metric
2. Resource type: The type of resource to look at
3. Available metrics: What specifics about the metrics
pg. 6
SKILLCERTPRO
4. Chart: Graphic display of the metric
2.1. Governance - Roles
Roles
Role assignments
 Delegated resource administration
 Roles organize related resource permissions together
o Depends on resource type
 E.g. different for VM and storage.
 Scope
o Roles are applied to a scope.
o They're inherited in following order:
 Management groups
 Subscription
 Resource groups
 Individual resources
 Role can be assigned to:
o Users
o Groups
o Service principal
 Application
 System Assigned Managed Identity: App Service, Function App, Virtual 
Machine, Virtual Machine Scale Set
 User Assigned Managed Identity
Role types
Built-in roles
 60+
 Common roles:
o Owner: Manage resources and resource access
o Contributor: Manage resources but not resource access.
pg. 7
SKILLCERTPRO
o Reader: Read-only access
o Storage Blob Data Reader: Specific to storage accounts
o SQL DB Contributor: Manage, but not access, SQL databases
o VM Contributor: Manage, but not access, virtual machines.
Custom roles
 ❗ Built using only PowerShell / CLI or REST API.
o New-AzureRmRoleDefinitation -Role $customRole
 Shows in same drop-down lists with built-in roles
 JSON file looks like this:
 {
 "Name": "Network Resource Viewer",
 "IsCustom": true,
 "Description": "Allows reading Azure network resources.",
 "Actions": [ "Microsoft.Network/*/read" ],
 "NotActions": [ ],
 "AssignableScopes": [ "/subscriptions/048.." ]
 }
Classic Administrator Roles
 The account that is used to sign up for Azure is automatically set as both the Account 
Administrator and Service Administrator.
o Roles are properties that can be changed in Subscription blade
 �� Azure recommends using RBAC roles
 Account Administrator (1 per Azure account)
o Conceptually, the billing owner of the subscription.
o The Account Administrator has no access to the Azure portal.
 Service Administrator (1 per Azure subscription)
o By default, for a new subscription, the Account Administrator is also the Service 
Administrator.
o The Service Administrator has the equivalent access of a user who is assigned the 
Owner role at the subscription scope.
o The Service Administrator has full access to the Azure portal.
 Co-Administrator (200 per subscription)
o The Co-Administrator has the equivalent access of a user who is assigned the 
Owner role at the subscription scope.
pg. 8
SKILLCERTPRO
2.2. Governance - Azure AD
Azure AD
Introduction to Active Directory
 Characteristics
o AD is cloud-based and geo-distributed
 Your tenant is distributed amongst many servers in Azure.
 Provides high level of availability and scalability.
o AD is multi-tenant.
 You're running a shared platform.
 Each tenant is segmented off on its own.
 Provides ability to give permissions from one tenant to another for certain 
accounts.
o Identity & Access
 Can be identity/access provider for Microsoft accounts for e.g. Office 365.
 In-house & third party developed applications can also leverage this 
service.
o Integrates with local AD
o Provides SSO
 For third party or in-house applications.
 Global administrator = Root
 Can be managed by Azure Portal, PowerShell/CLI, Microsoft Graph and API
o Microsoft Graph: API product trying to creating single way of interacting with all 
Microsoft APIs.
Role Based Access Control
 Roles defines actions that role is capable of doing.
 �� Roles are assigned to users and users only.
 ❗ Pre-built roles only.
o No custom roles.
o You can create custom that are application specific and are outside of the direct 
administration of Azure AD
 Roles are assigned at tenant level.
pg. 9
SKILLCERTPRO
o If you need separation of roles, you can create a new tenant and assign roles and 
permissions on that account.
Custom Domains
 You initially get tenantname.onmicrosoft.com
 Custom names must be fully qualified: Not a local name but an online name.
 Ownership must be verified
o Microsoft gives text records (TXT or MX)
o You put text record in DNS to get verified
 You can verify multiple domains
 Possible to register subdomains but you register parent domain.
 In Portal: Active Directory → Custom domain names → Add custom domain
Multiple Directories
 Resource independence
o Resource in one directory does not have access to resource in other directory
o No forests, trusts etc.
 Administrative independencies
o ❗ If you're global admin in one directory doesn't mean you have any access in 
other directory.
 Synchronization independence
o You can synchronize to specific directory and it does not impact other directories.
 Switch directory
o In Portal → Active Directory → Overview → Switch directory
Conditional Access
 Can be applied on users, locations, devices, applications.
 Policies allow you to have
o One application with multiple rules
o One rule with multiple applications
 ❗ Only available in Azure AD Premium
 Condition (if something) → Control (do something)
o Conditions
 Users and groups
 • Groups • User ID • Locations (IP)
pg. 10
SKILLCERTPRO
 Cloud apps
 Device platform and state
 • Domain Joined • Compliant • Lost or Stolen
 Locations (IP)
 Client apps
o Control: Allow, Deny, MFA
 Multi-factor authentication
 Compliant device
 Approved client app
 Terms of use
 Custom and session controls
 Manage in AD - Conditional Access
 Example policy: "Marketing app from US only"
o Assignments
 Users and groups: All users
 Cloud apps: Marketing app (registered in Azure AD)
 Conditions
 Locations: Include any location but exclude Contoso location
 Contoso locations is a named location
 Set US locations in portal: Active Directory → 
Conditional Access → Named locations
 Client apps: Apply policy with access from Browser but not from 
mobile apps and desktop clients.
o Access controls: Block access
Access Reviews
 Access review is created for an identified reviewer.
o Duration can be set
o Usually created by administrators.
o Reviewers can approve or deny.
 Access review can be a member of programs.
o A program groups reviews together.
 Managed in Access Reviews (separate view, not included in AD)
Administrative Units
 Container of resources
pg. 11
SKILLCERTPRO
 Used for
o Delegating administrative permissions over subsets of users
o Applying policies to a subset of users
 Useful in organizations with independent (autonomous) divisions
 An administrative unit is a directory object that can be created and populated with 
resources/users.
 AD Premium feature
 E.g. a central administrator can
o Create an administrative unit for a particular school (Business school)
o Populate it with only the Business school users
o Central administrator can add the Business school IT staff to a scoped role
 Grants the IT staff of Business school administrative permissions only over 
the Business school administrative unit
Identity Protection
 Detection
o Vulnerabilities
 E.g. MFA not configured, Unmanaged cloud apps, privileged identity 
management (only grant identity to user for a set period of time).
o Risk events (e.g. user sign in in from unknown detection)
 E.g. leaked credentials on internet, anonymous IP addresses (VPNs etc.), 
suspicious IP addresses, impossible travel (superman event, user logs in 
from NY and after 5 minutes logs in from Hong Kong), Unknown 
locations, infected devices.
 Investigations
o Receive notifications
o Workflows (when, who, what happened)
o Analysis: How can you apply policies to prevent future events?
 Policies
o User risk policy: E.g. if user risk event is high, allow access but require password 
change
o Sign-in risk: E.g. if sign-in risk is medium, allow access but require MFA.
Auditing and Monitoring
 Active Directory → Activity
o Sign-in: See, filter, search log-on statuses
o Audit logs: See, filter, search activity logs for Azure AD
pg. 12
SKILLCERTPRO
 Active Directory → Users and groups
o You can see user sign-in risks
 Active Directory → Azure AD Connect
o Install Azure AD Connect health from here
o Shows how health your Azure AD Connections
2.2.1. Governance - Azure AD - Entities
Azure AD Entities
Users
Types of users
 Cloud or Synced (from local AD through AD Connect)
 Member or Guest
o Members are created within AD directory
o Guests are invited by administrator or one of other users of Azure AD.
Common settings
 Usual attributes (e.g. department, phone number, contact, email)
 Setup password policy, expiration policy, flag users needing to reset their password
Usage Location
 Location is required if you want to assign license to a user within AD.
 Set usage location
o In portal: Active Directory → Users → Select User → Profile → Settings
 You can then assign license
o In Portal: Active Directory → Users → Select User → Licenses
 User Principal Name: Combination of a user name + domain.
Create new user
 AD → User → new User
pg. 13
SKILLCERTPRO
 User name
o Required, e.g. test@contoso.onmicrosoft.com
 Properties: Optional information e.g. first name, last name, job title.
External access
 You can add a user as an External User
 Good for B2B scenarios
o AD is not required on other business side.
Self-service password reset
 Scenarios
o Allows users to change their passwords
o If you cannot log in somehow
o Helps with account lockout
 Authentication methods
o Types:
 Text message/Phone call
 Secondary email
 Security questions
o Administrator requires one or more.
 Manage in portal
o Steps: Active Directory → Password Reset
o Configurations
 Enable
 You can enable for all users or selected users.
 �� Good to first enable for a pilot group to see how it works.
 Registration
 Require users to register when signin in
 Prompts user to fill information for authentication 
methods.
 After how long user will be prompted to confirm authentication 
method information
 Notifications
 Notify users on password resets
 Notify all admins when other admins reset their password
pg. 14
SKILLCERTPRO
User settings
 Enterprise applications
o Users can consent to apps accessing company data on their behalf (yes/no)
 Yes; users can consent to allow third party and multi-tenant applications 
to consent on their own behalf.
o Users can add gallery apps to their Access Panel
 No; as an administrator you have to manually integrate the applications
through Access Panel
 App registrations
o Users can register applications (yes/no)
 Yes; non administrations can register applications to be used within the 
directory, no; only administrators can do it
Groups
 Types of groups
o Assigned or Dynamic
 Assigned: You assign users to groups manually
 Dynamic: You select various attributes to make users member of a group
 Dynamic query e.g. department Equals marketing
o Security or Office 365
 Security groups are for assigning permissions.
 Owners and members
o Owners: Can add/remove users from the group.
o Members: cannot manage the group, normal permissions
 Expiration of groups
o Groups can automatically expire.
 You manage in "Azure Directory → Groups"
o You can assign licenses to a group where each member will get a license.
 Good for performing bulk user updates
 Self-service group management
o Owners manage groups instead of administrator that manage the group for the 
owners.
o Users can request to join in group with providing some business justification.
o Audits & alerts
 Everything is logged
 You can e.g. trigger alert on frequent activities in a group
 Company Branding
o In portal: Active Directory → Users and groups → Company branding
pg. 15
SKILLCERTPRO
o Allows you to customize the pages with e.g. banner, sign-in page text, user name 
hint
Devices
 Enables more management
 Device settings show overview in Portal
o Intune + MDM offer much more control
 You can add work or school account to integrate
Registration types
Register Device
 Basic registration
 Bring your own device (BYOD) scenario
 For mobile devices and Windows 10
o Enable/disable and additional management (MDM) for mobile devices like intune.
 Enterprise State Roaming
o Users synchronizes their user settings and application settings data to the cloud.
o Supported in Windows 10
o Enhanced security, management and monitoring.
o Separation of corporate and consumer data in cloud.
Join Device
 Corporate owned assets that you want to manage
 E.g. Windows 7 or Windows 10
 You get some benefits e.g. single sign on.
Hybrid Join
 You can enable automatic registration for your AD joined computers
 Join device in both local AD and Azure AD
 Grant device user access to apps that need traditional local AD (=on-prem AD) 
authentication.
 You get service principal for the device
 Actual management is done through Group Policy or System Center Configuration 
Manager.
pg. 16
SKILLCERTPRO
o They're tied in to Azure AD but not part of core AD.
 Relies on AD Connect for synchronization
o If they're already joined to local AD, they're also registered in Azure AD 
automatically.
 Configuration
o Ensure access to external Azure AD URLs.
o Configure SCP (service connection point) internally.
o Configure ADFS if required
Manage in Portal
 Active Directory → Devices
 Configurations
o Users may join devices to Azure AD
o Additional administrators on Azure AD joined devices
 Default is none, you can select users
o Users may register their devices with Azure AD
o Require Multi-Factor Auth to join devices
o Maximum number of devices per device
o Users may sync settings and enterprise app data
 All, selected, None
o For more you need PowerShell.
Azure AD Device Settings/Policies
 Control permissions
o Who's allowed to access join devices?
 Control sync
o Enabled/disabled
 Device management through Intune or other MDM
 Conditional access
o Whether or not device has access to resources within your organization
Applications
 Azure AD IDaaS (Identity Directory as a Service)
 Application types
o Third party or internal
pg. 17
SKILLCERTPRO
o Pre-integrated or proxies
 Automated user provisioning through SCIM 2.0
o Use provisioning enables synchronization of user account.
o SCIM
 System for cross domain identity management.
 Defined by IETF
 Control users, groups and their relations
o Available on select SaaS apps
 In portal, you can assign access to applications
o AD → Applications → Select application → Users and groups
2.2.2. Governance - Azure AD - Hybrid Identities
Hybrid Identities
 Hybrid (common) identity = Cloud + On Premises identity
 Connection is done through Azure AD connect
Four Pillars
 Unified Development and DevOps
o A common approach to building applications, and full flexibility to deploy in the 
cloud or on-premises
 Integrated management and security
o Built-in management and security solutions across full operational lifecycle from 
cloud to on-premises
 Common Identity
o Enable end-user productivity with single sign on to cloud and on premises 
applications while protecting corporate data
o Single identity
 Create and manage a single identity for each user across your hybrid 
enterprise, keeping users, groups and devices in sync
o Single Sign-on
 Provide single sign-on access to your application including thousands of 
pre-integrated SaaS apps
o Conditional Access
 Protect identities by enforcing risk-based conditional access policies and 
multi-factor authentication for both on-premises and cloud applications
pg. 18
SKILLCERTPRO
o Remote Access
 Provide secure remote access to on-premises web applications through 
Azure AD Application Proxy
o Self Service
 Self-service password reset and application access requests for directories 
in the datacenter an the cloud
o High Availability
o Collaboration
 Enable vendors, contractors and partners to get risk-free access to inhouse resources
o Consistency
 Truly consistent capabilities
 Consistent Data Platform
o Seamlessly distribute data between cloud and on-premises
o Enrich with analysis and deep learning
Azure AD Connect
 Integrate your on-premises AD or LDAP directory to the cloud
 Establish a single identity for your users to access on-premises and cloud-based 
resources
 Connect your users to thousands of SaaS applications published through Azure
 Manage in Azure AD Connect → Synchronization Service
 Adjust to business changes after Azure AD Connect is installed.
 Change the service accounts
 Add the Managers OU to be included in the synchronization
Preparing for Azure AD Connect
 Create a new user in Azure AD as Global Administrator
 Download Azure AD Connect and install it.
o You need > Windows Server 2008
Install and configure Azure AD Connect
 Installation settings
o Initially
 Custom or Express installation
 Installation location
pg. 19
SKILLCERTPRO
 Create an express SQL or use an existing SQL instance
 Provide a service account or create a new one
 Service account for SQL server
 Custom sync groups
 Fill: Administrators group, operators group, browser group, 
password reset groups
 AD Connect groups not domain groups!
o Then
 How users will sign-in
 One of them: Password synchronization, Pass-through 
authentication, Federation with AD FS
 Enable sign on → Yes, No
 Forest and Azure credentials
 Global administration username password
 Select directory type (AD or LDAP)
 Then type Forest name
 Create new AD account or use existing AD account
 Type domain username and password
 �� Recommended to enter Enterprise Admin credentials
 Select UPN for sign-in
 E.g. azure-contoso.com
 Select user name: e.g. userPrincipalName, treeName, unicodePwd
o Then
 Choose what domains and OUs get synchronized to the cloud
 Sync all domains and OUs or sync selected domains and OUs
 How to uniquely identify users
 Identification:
a. Users are represented only once across all directories.
b. User identities exist across multiple directories.
 Match using: mail attribute, specific attribute, etc.
 Source anchor (ID)
. Let Azure manage the source anchor for me
a. Specific attribute: objectGUID, pager, objectSid etc.
 Filter users and devices by group
a. Synchronize all users and devices
b. Synchronize selected
 Optional features
 Exchange hybrid deployment
 Exchange mail public folders
 Azure AD app and attribute filtering
pg. 20
SKILLCERTPRO
 Password synchronization
 Password writeback
 Group writeback
 Device writeback
 Directory extension attribute sync.
 Enable single sign on
 ❗ Requires domain administrator account
 Choose staging mode or install it
 Staging mode: Synchronization won't synchronize any data to 
Azure AD
o Post installation
 Install AzureAD PowerShell module
 �� Then enable Azure AD recycle bin
Metaverse
 What'll be synced in the next synchronization
o Connectors to and from on-premises Active Directory
o Connectors to and from Azure Active Directory
 Controls what attributes from what objects from what location are available for 
synchronization
Hybrid Planning
Sign On
 Authentication and Authorization
o How do users typically login to their on-premises environment?
o How will users sign-on to the cloud?
o Will you be allowing workers from partner networks access to cl oud and onpremises resources?
 Multi Factor Authentication
o Do you currently implement multi-factor authentication?
o What are the key scenarios that you want to enable MFA for?
o Will you use MFA to secure Microsoft Apps?
o Will you use MFA to secure remote access to on-premises apps?
 Delegation and Administration
pg. 21
SKILLCERTPRO
o Does your company have more than one user with elevated privilege to manage 
your identity system?
o Does your company need to delegate access to users to manage specific resources?
o Does each delegated user need the same access?
Synchronization
 Directory synchronization
o Do you have a disaster recovery plan for the synchronization server?
o Where will the synchronization server be located?
 E.g. if it's behind a firewall, you'll need to open up some ports
o Do you have any other directory on-premises like LDAP or an HR database?
o Does your company use Microsoft Exchange?
 Multi Forest synchronization
o Are the UPNs unique in your organization?
 More than one forest → You can call people same thing as other people 
→ You won't be able to do that in single Azure AD as they need unique 
UPNs.
o Will the Azure AD Connect server be able to get to each forest?
o Do you have an account with the correct permissions for all forests you want to 
synchronize with?
 Password synchronization
o Do you have restrictions on storing passwords in the cloud?
o Will your employees be able to reset their own passwords?
o *What account lockout policy does your company require?
Applications
 Applications
o Will users be accessing on-premises applications? In the cloud? Or both?
o Are there plans to develop new applications that will use cloud authentications?
 If so, then make sure that authentication can use OAuth, certificates e.t.c.
o Will cloud users be accessing applications on-premises?
o Will on-premises users be accessing applications in the cloud?
 Access Control
o Does your company need to limit access to resources according to some conditions?
o Does your company have any application that needs custom control access to some 
resources?
pg. 22
SKILLCERTPRO
o Does your company need to integrate access control capabilities between onpremises and cloud resources?
o Does each user need the same access level?
Domain Structure
 Domain Name
o What name will your organization use for your domain in the cloud?
o Does your organization have a custom domain name?
o Is your domain public and easily verifiable via DNS?
 Directory Structure
o How many AD forests do you have?
o How many Azure AD directories?
o Will you filter what user accounts are synchronized with the Azure AD?
o Do you have multiple Azure AD Connect servers planned?
o Do you have different directory that users authenticate against?
 Federation
o Will you use the Azure Federation or on-premises AD FS?
 An option is moving on-premises AD FS to Azure Federation.
o More federation services for identities are provided now through Azure
o Does your organization use smart cards for Multi Factor Authentication
Forest to Azure AD Topology
 ❗ Restrictions
o One to one relation between Azure AD and AD Connect
 Multiple AD Connect cannot connect to Single azure AD
 Azure AD Connect cannot connect to multiple Azure AD directories
o The same user account cannot sync to multiple Azure AD directories
o Users in one Azure AD cannot appear as contacts in another Azure AD directory
 Single Forest to Single Azure AD
o Single Forest → Single AD Connect → One Multiple AD
o Most common topology
o �� Recommended by Microsoft
o Expected topology when using Azure AD Connect Express installation
o Supports multiple domains
 Single Forest to Multiple Azure AD
o Single Forest → Multiple AD Connects → One Multiple AD
pg. 23
SKILLCERTPRO
o Useful when e.g. some users passwords cannot be written back to the cloud but 
another department can do it.
o ❗ Azure AD Connect sync servers must be configured for mutually exclusive 
filtering.
o ❗ Users in one Azure AD will only be able to see users from their own Azure AD 
instance.
o ❗ A DNS domain can only be registered in a single Azure AD directory.
o ❗ Some write-back features not supported with this topology
 No group / device writeback
 Multiple Forest to Single Azure AD
o Multiple Forest → One AD Connect → One Azure AD
o ❗ Users must have only one identity across all forests
o The user authenticates to the forest in which their identity is located.
o All forests are accessible by Azure AD Connect
o ❗ Users have only one mailbox
 Multiple Forest to Multiple Azure AD
o Multiple Forest → Multiple AD Connects → Multiple Azure ADs
o Useful especially if you need isolation for different forests.
o For each instance of Azure AD, you'll need an installation of Azure AD Connect
o Users in one Azure AD will only be able to see users from their AAD instance.
Register domain name
 Add Azure AD Domain Name
o Create directory where organization name is contoso.local.
o Add domain name azure-contoso.com and verify through TXT DNS entry.
 Add UPN Suffix
o On-prem resources has name@contoso.local but you'll need name@azurecontoso.com to allow e.g. SSO.
o Flow:
a. Add azure-contoso.com as an alternative UPN Suffix through Active 
Directory Domains and Trusts
b. Add azure-contoso.com to all user accounts as the preferred UPN suffix.
Single Sign On
 Password synchronization
o A copy of password and usernames is synchronized to the cloud.
 Pass through authentication
pg. 24
SKILLCERTPRO
o You don't store passwords in cloud
o User is authenticated using pass through authentication agent that connects with 
on-premises AD
o Works seamlessly with Azure Multi-Factor authentication
 Seamless SSO
o Works with Azure AD Join or the desktop is previously joined to your AD domain
o Requires Azure service endpoints to be added to the client browser's Intranet 
zone.
 This way the browser can send the Kerberos ticket to the website.
o Flow:
a. Client from a joined device tries to access to a resource in cloud.
b. Local client goes to AD DC and gets an access token.
c. Client forwards access token to Azure AD.
 If MFA is enabled, it'll prompt user.
Making cloud apps available
 Azure AD → Enterprise Applications
 4 categories
i. Gallery applications
ii. Applications you're developing, integrated with Azure AD
iii. On-premises applications with Azure AD Application Proxy
 Azure AD Application Proxy
 Allows Azure to reach on-premises resources.
 Consistent access to private resources without a VPN.
 Install App Proxy & Connector on-premises
 ❗ Cannot be installed on a server with the Pass Through 
Authentication connector
 ❗ You need to configure a CNAME on DNS for the 
particular domain work for it to work.
 Set-up on Azure
 Add applications
 Assign to users
 Configure SSO
 Provision just like any SaaS app
 Flow for Azure user reaching on-premises resource:
a. Azure AD gives a token to user
b. User sends that token to Azure App Proxy
c. Proxy takes UPN and SPN and gives it to connector
pg. 25
SKILLCERTPRO
d. Connector goes to on-prem AD and gets Kerberos ticket.
e. It forwards it to actual on-prem application, it verifies the 
ticket and ticket is assigned to the cloud user.
iv. Non-gallery applications
 Manage permission
o Azure AD → Enterprise Applications → In application → Users and groups
 Configure SSO
. Configure SSO for the new application
 Manage permission
 Azure AD → Enterprise Applications → In application → Single 
sign-on
 Sign-on types:
 Password-based Sign-on
 Linked Sign-on
 SAML
 Provides step by step guide for federation between 
application and Azure AD manually
i. Click on the new application new in the Azure AD MyApps access panel
 Access panel is reached at myapps.microsoft.com
 It prompts you to install a browser extension
ii. Install Access Panel Extension
iii. Log into application so that password is stored for SSO
2.3. Governance - Azure Policies.
Microsoft Azure Policies
 Configures what kind of resources can be deployed and managed
 Ensures proper cloud governance by controlling resource deployment and usage.
o ❗ Publishing 
requires Microsoft.Authorization/policyassigments/write permission.
 The assigner is saved as assignedBy property.
 Apply to new and existing resources.
o Resources are scanned hourly for compliance with policies.
Policy types
 Built-in policies
pg. 26
SKILLCERTPRO
o E.g.: Require SQL Server 12.0, Allowed Storage Account SKU, Allowed Resource 
Types, Allowed Locations, Allowed Virtual Machine SKUs, Apply tag and its 
default value, Enforce tag and its value, Not allowed resource types
 Custom Policies
o JSON format
 Supports logical operations (or, allOf, noneOf) and if statements.
o Used for granular resource control
 E.g. limit load balancer creation to IT admins.
o Can be create manually or by copying existing policy from e.g. GitHub.
 E.g.
o {
o "policyRule": {
o "if": {
o "not": {
o "field": "location",
o "in": "[parameters('allowedLocations')]"
o }
o },
o "then": {
o "effect": "audit"
o },
o "parameters": {
o "allowedLocations": {
o "type": "Array",
o "metadata": {
o "description": "The list of allowed locations for resources",
o "displayName": "Allowed Locations",
o "strongType": "location"
o }
o }
o }
o }
}
Policy parameters
 Passed to policy
 Enable policy reuse
o Fewer policies are required.
 String or array
pg. 27
SKILLCERTPRO
Policy Effects
 Append: Resource policy additions, e.g. tags.
 Audit: Logging only, generates a warning.
 AuditIfNotExists: Enables audit if resource does not exists
 Deny: Denies deployment
o �� Existing non-compliant resources are marked but not deleted.
 DeployIfNotExists: If resource does not exists, deploy it.
Management Groups
 Organizes multiple subscriptions.
 Up to 6 hierarchical levels.
 Allows to assign policy groups
o �� Subscriptions inherit settings
 Facilitates RBAC
 Subscriptions can be moved to other parts of hierarchy.
Policy exclusions
 Called exclusion scopes
 Policies can have exclusions in different scopes
 Scopes can be e.g. resource groups in subscription, or VMs in resource groups.
Policy Initiative Definations
 Groups policies into a single unit.
 Used when a single Azure governance goal consists of multiple checks.
 Can be assigned to resources/groups/subscriptions
 E.g. Security Compliance
i. Check for endpoint protection
ii. Check for VM disk encryption
3. Monitoring
pg. 28
SKILLCERTPRO
Monitoring
Azure Monitor
 Centralized ways of getting insights from application to infrastructure
 You can diagnose, trace and debug issues
 Uses ML to detect anomalies and reveal hidden patterns
 Track how customers interact with the application
 Components
o • Alerts • Metrics • Action groups • Monitoring & reporting • Dashboard • Logs
High level view
 Collects data from
o • Application • Operating system • Resources • Subscription • Tenant
 Populates stores
o Metrics & logs
 Perform functions:
o Insights: • Application • Container • VM • Monitoring solutions
o Visualize: • Dashboards • Views • Power BI • Workbooks
o Analyze: • Metrics Explorer • Log Analytics
o Respond: • Alerts • Autoscale
o Integrate: • Event Hubs • Logic Apps • Ingest & Export APIs
Alerts
 Notifies when important conditions are found in the monitoring data
 Flow of alerts
o Alert Rule
 Target Resource (Signal) → Criteria (Logic Test)
 Action Group (Actions to do)
 Monitor condition (Alert State)
 Alert rules have single of each properties:
o Target resource
 Scope & signals for alerting.
 E.g. VM
o Signal
 Emitted by target resource
pg. 29
SKILLCERTPRO
 Can be metrics, activity log, application insights and log.
o Criteria
 Combination of signal and logic applied on target resources.
 E.g. less than X CPU usage.
o Logic
 User-defined logic to verify that signal is within expected range/values.
 E.g. less than 30% CPU usage.
o Alert name
o Alert description
o Severity
 Alert once the criteria specified in the alert.
 Can range from 0 to 4.
o Action
 Specific action taken when the alert is fired.
 You can alert on:
o Metric values
o Log search queries
o Health of underlying Azure platform
o More..
 State of alerts:
o New: Created or fired
o Acknowledged: Issue is reviewed.
o Closed: Issue has been resolved.
 Can be reopened by changing its state.
o User changes state from New.
Log types
 Diagnostic Logs
o Non-compute resources: Resource metrics
o Compute resources: Guest OS (e.g. syslog for Linux, event logs for Windows)
o Azure Monitoring Agents
 Azure Diagnostics Extension (cloud only)
 Windows Server and Linux
 useful for basic resource-level monitoring
 Deployed automatically to VM when you enable it.
 Boot diagnostics (serial console)
 Log Analytics Agent (hybrid solution)
pg. 30
SKILLCERTPRO
 Can collect logs from Azure & on-prem systems to same 
namespace.
 Application Logs
o Trace event streams
o Programmed in application itself.
o Application Insights
 Instrumentation tool
 HTTP requests
 Dependency Calls (to e.g. SQL, external services, background services)
 Activity Logs
o Azure infrastructure logs
o E.g.
 Who created VM?
 Who configured this VNet?
 Traffic stream from NSG?
o Can be sent to: Log Analytics, Event Hubs, Azure Storage
NSG (Network Security Group) Flow logging
 Flow logs handled by NSGs.
 Plot using
o In-built Azure plotting tool Network Watcher
o Power BI
Azure Cost Management
 In portal it can be eached through "Cost analysis" blade of desired scope.
 In "Cost analysis" you can filter by "Tag"s.
 Cost Management shows organizational cost and usage patterns with advanced analytics
 Reports show your internal and external costs for usage and Azure Marketplace charges
 You can automate periodically export of your costs
o �� You can also see daily usage data in Portal: Azure Account Center → Billing 
history → Current period → Download usage
 Data is consumed by other Azure resources
 Predictive analytics are also available.
Metrics
pg. 31
SKILLCERTPRO
 Collected one-minute frequency
 Uniquely identified in a namespace.
 �� Stored for 93 days
o Collected in Azure metrics database (time series database)
o �� Copy to Log Analytics for long term storage
 Holds value properties: Time, Type, Resource, Value, Multiple Dimensions
 Value:
o Health of application: can help to identify route cause.
o Valuable when combined with other metrics.
 Sources of metrics:
o Platform metrics
 Each resource provides
 Visibility into health and performance
o Application metrics
 Generated by application insights
 Detect performance issues & track trends
o Custom metrics
 ❗ Must be created in same region as the resource that has the metrics
 Use-cases: • Metrics explorer • Metric Alert Rule • Auto Scale • Route & Stream • Archive 
• Access
Third party tools
 ITSM
o IT as a Service
o Helps to design, plan, deliver, operate, and control information technology (IT) 
services
o Azure ITSM Connector
 Bi-directional connection layer between and your ITSM tool(s)
 Use cases:
 Create ITSM work items based on Azure alerts.
 Sync ITSM incident/change request data to Azure.
 SIEM
o Security information and event management
o E.g. Splunk (there's an open source add-on to send to Event Hubs)
 �� You could even use Azure Sentinel as a SIEM tool.
Action groups
pg. 32
SKILLCERTPRO
 Name: Unique identifier
 Action type
o Voice call or SMS
 ❗ Up to 10 SMS / voice call actions in an action group.
 ❗ No more than 1 SMS / Voice call every 5 minutes.
o Webhook
 ❗ Up to 10 webhook call actions in an action group.
 It'll retry 2 times: first after 10, then 100 seconds.
o Logic App
 ❗ Up to 10 logic app actions in an action group.
o Automation runbook
 ❗ Up to 10 Runbook actions in an action group.
o Azure Function
o ITSM
 ❗ Up to 10 ITSM actions in an action group.
o Email
 ❗ Up to 1000 e-mail actions in an action group.
 ❗ No more than 100 emails in an hour.
o Push notification
 Azure App Push
 ❗ Up to 10 Azure app actions in an action group.
 Details: corresponding phone number, email address, webhooks URI, or ITSM 
connection details.
Monitoring and reporting on spend
 Two ways to understand Azure bill to compare usage and costs (invoice):
i. Using usage file
 Detailed usage CSV file shows charges & daily usage in billing period
 Download:
a. Sign into the Azure account Center as the Account 
Administrator
b. Select the subscription for which you want the invoice and 
usage information
c. Select billing history → Download usage
 Select billing history
ii. Using Azure portal
 Subscription → Cost analysis → Filter by Timespan
 See estimated costs on Portal: Subscription → Usage and estimated costs
pg. 33
SKILLCERTPRO
Log Analytics
 Old: OMS, new: Embedded in Azure Monitor as Logs.
 It's a dataware house for telemetry
o It converts any schema to a table schema that allows you to query.
 Uses KQL (pipe-based) language to query.
 All monitoring roads lead t o Azure Log Analytics
o There's always an integration from an logging Azure component to Log Analytics.
 You can download agents in Workspace → Connect
o Agents do not require VPN
o System Center Operations Manager
 Can send data to Log Analytics from cloud/on-prem servers.
 Azure Data Explorer
o Query language is used & viewed
 Alert rule
o Based on each query that run on regular intervals, results are evaluated to trigger 
an alert.
o Target
 Specific Aure resource
o Criteria
 Specific logic to trigger an action
 Log Alerts
 Describes where signal is custom query based on Log Analytics
o Action
 Call to send a notification
o Set-up in Log Analytics → Alerts
 Export
o • Excel • PowerBI
 Application Insights data is used in a different partition in Log Analytics.
o E.g. requests, traces, usages
o Allows you to cross application queries
 Function
o Queries can be saved as functions to be used within another query.
 Requires log analytics workspace
Create performance baselines
 Baseline
o Configuration management term
pg. 34
SKILLCERTPRO
o Signifies an agreed-upon description of product attributes, per unit time, which 
serves as a basis for defining change.
o �� It's not only recommended but mandatory for team to develop a baseline.
 Gather diagnostics for long enough time.
 Capture all peaks and values over ordinary usage.
 Enable streams and create baseline
 Even analyze those and agree upon which performance ranges are 
acceptable to define SLAs.
 Helps to isolate problem
 Baselining in Azure
i. Continuous monitoring
ii. Normal operational parameters
iii. Alerts on deviations
iv. Take proactive corrective actions
 Baselines actions
o Enable diagnostics monitoring and telemetry, e.g.:
 Azure IaaS resources
 Azure App Service apps
o Creating performance baselines
 Analyze diagnostics output
 Plot metrics
4.1. Storage - Azure Storage
Storage
Storage services
 Storage account is top-level account for following services:
o Blob Storage
o File Storage
o Table Storage
o Queue Storage
Blob Storage
 Object and disk storage
pg. 35
SKILLCERTPRO
 Blob storage tiers
 Azure Search integration
 Blob Lease for exclusive write access
o Pass in lease id to API to modify
o E.g. IaaS VMs lease Page Blob disks to ensure its managed by single VM
 You can create snapshots on blob level and view snapshots.
Azure Data Lake Storage
 Uses blob storage to store data
 Big data analytics
 Analytics interface and APIs
 Blob storage APIs
 Hadoop compatible access to data
 ❗ GPv2 Storage accounts only
Blob Types
 Block Blob
o Composed of 100 MB blocks
o Optimized for efficient upload
o Insert, replace, delete, blocks
o ❗ Up to 4.77TB max file size
o ❗ 50.000 max blobs
 Append blob
o Can only append blocks
o Ideal for log and audit files
o ❗ 195GB max file size
 Page Blob
o Optimized for frequent read/write operations
o Good for VM disks and databases
 Foundation for IaaS disks
 Stores VHD files.
 Underlying storage for Azure SQL
o ❗ Standard (HDD) / Premium (SSD) storage
o ❗ 8 TB max file size
o ❗ Only offered in General Purpose account types
pg. 36
SKILLCERTPRO
Blob Storage Access Tiers
 Set on blob level.
 Three tiers:
i. Hot Tier: Frequent reads
 Lower data access costs
 Higher data storage costs
ii. Cool Tier: Accessed less frequently
 Higher data access costs
 Lower data storage costs
 Optimized for data that's stored 30 days
iii. Archive Tier: Take hours to get data available
 Highest data access cost
 Lowest data storage cost
 Optimized for data that's stored 180 days
 ❗ Only supported for Block Blobs
 Changing storage tiers incurs charges
 ❗ Can't change the Storage Tier of a Blob that has snapshots
 Azure Blob Storage Lifecycle Management Policies
o E.g. configure a policy to move a blob directly to the archive storage tier X days 
after it's uploaded
o In portal: Storage Account → Blob Service → Lifecycle Management
o Executed daily
WORM: Write Once Read Many
 Cannot be erased or modify for certain period of time.
 Set on container level
 Enable in portal
o Access Policy → Add Policy → Time-based retention (set retention period) / Legal 
hold (attach tags) → Lock policy
Soft Delete
 Saves deleted for a specified period of time
 In portal: Storage Account → Blob Services → Soft Delete
pg. 37
SKILLCERTPRO
Static Website Hosting
 When activated it creates $web container.
 You need to have default document and error page.
 You can integrate Azure CDN
o Azure Content Delivery Network (CDN)
 Distributed network of cache servers
 Provide data to user from closest source
 Offload traffic from origin servers to CDN
 Typically static data
 Pricing tiers are Microsoft, Akami, Verizon (Microsoft partners)
 Supports • HTTPS • large file download optimization• file compression • 
geo-filtering
 Azure CDN Core Analytics is collected and can be exported to blob 
storage, event hubs, Log Analytics.
o Azure Storage blob becomesorigin server.
o Azure CDN servers become edge servers
o CDN can authenticate to Blob Storage with SAS tokens to be able to read private 
data.
o Caching rules
 On blobs you can set CDN caching rules, such as CacheControl:maxage=86400 in blob properties.
o Two alternatives to set up:
a. Create CDN and configure against blob service.
b. Storage account → Blob service → CDN
 You can have custom domain
 You can have CORS policies
Azure Search
 Integrates with Blob Storage
 You can provide metadata in blobs, they'll be used as fields in search index which helps 
categorize documents and aid with features like faceted search.
o You can choose index content, content+metadata or just metadata.
 Searchable blobs can be • PDF • DOC/DOCs • XLS/XLSX • PPT/PPTx • MSG • HTML • XML 
• ZIP • EML • RTF • TXT • CSV • JSON
 Structure
o Index, Fields, Documents
 Data Load
o Push data in yourself
pg. 38
SKILLCERTPRO
o Pull data from Azure sources (SQL, Cosmos DB or blob storage)
 Data Access
o REST API, Simple Query, Lucene, .NET SDK
 Features:
o Fuzzy search handles misspelled words.
o Suggestions from partial input.
o Facets for categories.
o Highlighting search tags for the results.
o Tune and rank search results
o Paging
o Geo-spatial search if index data has latitude and longitude, user can get related 
data based on proximity
o Synonyms
 Lexical analysis done by Analyzers
 You can combine following cognitive skills in pipelines: OCR, language detection, key 
phrase extraction, NER, sentiment analysis, merger/split/image analysis/shaper.
File Storage
 SMB File Shares
 Attach to Virtual Machines as file shares
 Integrates with Azure File Sync
o On-prem to Azure sync with caching strategy
Table Storage
 NoSQL Data Store
 Scheme-less design
 Azure Cosmos DB
Queue Storage
 Message based
 For building synchronous applications
 URL format: e.g. http://storageaccount.blob.core.windows.net
Account Types
pg. 39
SKILLCERTPRO
Blob Storage Account
 Supported services: Blob storage
 Supported blob types: Block blobs, append blobs
 Supports blob storage access tiers (hot, cool, archive)
General Purpose V1
 Supported services: Blob storage
 ❗ Does not support blob storage access tiers (hot, cool, archive)
 ❗ Classic deployment & ARM
 ❗ Does not support ZRS (Zone Redundant Storage) replication
 Slightly cheaper storage transaction costs, can be converted to V2.
General Purpose V2
 Supports all latest features.
o Including anything in General Purpose V1 and blob storage access tiers.
 �� Recommended choice when creating storage account.
 Lower storage costs than V1
 ❗ Has a changing soft limit (as of now 500 TB)
o You can contact Azure support and request higher limits (as of now 5 PB). Same 
for ingress/egress limits to.
Account Replication
 Impacts SLA
 Locally Redundant Storage (LRS)
o Three copies of data in single data center.
o Data is spread across multiple hardware racks.
 Zone Redundant Storage (ZRS)
o Three copies of data in different availability zones in same region.
o ❗ Only available for GPv2 storage accounts
 Geo-redundant Storage (GRS)
o Three copies of data in two different data centers in two different regions.
o ❗ You don't get to choose second region, they're paired regions decided by 
Microsoft.
o ❗ Replication involves a delay.
pg. 40
SKILLCERTPRO
 RPO (recovery point objective) is typically lower than 15 minutes.
 Read-access Geo-redundant Storage (RA-GRS)
o Same as GRS, but you get read-only access to data in secondary region.
Azure Storage Explorer
 Cross-platform client application to administer/view storage and Cosmos DB accounts.
o Can be downloaded with Storage Account → Open in Explorer in Portal.
o Available in Azure portal as well (preview & simpler)
 Can manage accounts across multiple subscriptions
 Allows you to
o Run storage emulator in local environment.
o Manage SAS, CORS, access levels, meta data, files in File Share, stored procedures 
in Cosmos DB
o Manage soft delete:
 Enables recycle bin (retention period) for deleted items.
 Connecting and authentication
o Admin access with account log-in
o Limited access with account level SAS
Pricing
 Data storage cost (capacity)
 Data operations
 Outbound data transfer (bandwidth)
 Geo-replication data transfer
Import and export data to Azure
 You can use portal, PowerShell, REST API, Azure CLI, or .NET Storage SDKs.
 You can upload files/folders using Azure Storage Explorer.
 You can use physical drives
o ❗ 64 bit only operating systems: Windows 8+ and Windows Server 2008+
o Preparing the drive
 ❗ NSTF only.
 ❗ Drives must be encrypted using BitLocker
o WAImportExportTool
 Azure Import/Export tool
pg. 41
SKILLCERTPRO
 V1: Blob Storage, Export Jobs, V2: GP v1, GP v2
 Allows you to copy from on-prem.
AzCopy
 You can use AzCopy command-line utility tool.
 No limit to # of files in batch
 Pattern filters to select files
 Can continue batch after connection interruption
o Uses internal journal file to handle it
 Copy newer/older source files.
 Throttle # of concurrent connections
 Modify file name and metadata during upload.
 Generate log file
 Authenticate with storage account key or SAS.
Importing data
 Create import job
i. Create storage account
ii. Prepare the drives
 Connect disk drives to the Windows system via SATA connectors
 Create a single NTFS volume on each drive
 Prepare data using WAImportExportTool
 Modify dataset.csv to include files/folders
 Modify driveset.csv to include disks & encryption settings
 Copy access key from storage account
iii. In Azure → Create import/export job → Import into Azure → Select container RG 
→ Upload JRN (journal) file created from WAImportExportTool → Choose import 
destination to the storage account → Fill return shipping info
iv. Ship the drives to the Azure data center & update status with tracking number
 Costs
o Charged: fixed price per device, return shipping costs
o Free: for the data transfer in Azure
 ❗ No SLAs on shipping
o Estimated: 7-10 days after arrival
pg. 42
SKILLCERTPRO
Exporting data
1. In portal: Azure → Create Import/Export Job → Choose Export from Azure
2. Select storage account and optionally containers
3. Type shipping info
4. Ship blank drives to Azure
5. Azure encrypts & copies files
o Provides recovery key for encrypted drive.
Azure Data Box
 Microsoft ships Data Box storage device
o Each storage device has a maximum usable storage capacity of 80 TB.
 It lets you send terabytes of data into Azure in a quick, inexpensive, and reliable way
4.1.1. Storage - Azure Storage - Security
Azure Storage Account Security
Management vs Data Plane
 Handled with RBAC in Azure AD
o Can see storage keys: Owner, Contributor & Storage Account,Virtual Machine 
Contributor, Storage Account Key Operator Service
 Reader cannot see storage keys
Management Plane
 Administrative tasks e.g.
o Viewing properties of storage account.
o Deleting storage account.
o Assigning roles to other users.
o Modifying the configuration.
pg. 43
SKILLCERTPRO
Data Plane
 Requires access to storage account keys.
 On blobs you can set access level to public access.
Storage Account Keys**
 Provides full access to the storage
 �� Best practice: Give all admins and apps same key.
o Enables you to:
 Regenerate secondary key.
 Update apps to use secondary key
 Regenerate primary key
 Can be managed by Azure Key Vault using Powershell
o Storage account keys are stored as Key vault secrets.
o Azure Key Vault syncs keys with storage Account
o Storage account keys never returned to caller.
Shared Access Signatures (SAS tokens)
 �� Better as it follows principle of the least privilege.
 Contains permissions and start & end validity period.
o Set read and/or write permissions.
o Grant permissions to access only partition + row key ranges.
o You can restrict access to IP Address(es)
o Enforce HTTPS
 Two types:
o Service Level SAS: Only to a single blob/file/table or queue storage.
o Account Level SAS: Applies to multiple services
 ❗ It's generated by client and is not tracked by Microsoft.
o Signature is signed with account key and ensures none of the parameters are 
tempered.
o To invalidate, you'll need to regenerate storage account key used to sign SAS.
o �� Better way: Storage Access Policies
 Defined on container level.
pg. 44
SKILLCERTPRO
 In portal: Containers → Right click on container → Access policy
 Permissions + validity period is on server side.
 Service level SAS only.
 Easy to revoke by deleting the policy or changing its validity period.
 Example url:
URL part Description
https://myacount.blob.core.windows.net/container1/file1.
pdf
URL to endpoint
?sv=2017-07-29 Rest API version
&st=2018-04-30T19%3A19%3A19Z Validity start time
&se=2018-05-01T19%3A19%#A19Z Validity end time
&sr=b Type of resource
&sp=r Permissions
&sip=168.1.5.60-168.1.5.70
IP Address / 
range (optional)
&spr=https Protocol (optional
)
&sig=pk9oGEPqYyu0K4Gutfreq9n0CJqgnjYgkEwcIEL8I0%3D Signature
Azure AD authentication with RBAC
 Available for Blob and Queue services.
 Azure AD provides OAuth 2.0 token
 E.g. Storage Blob Data Contributor, Storage Blob Data Reader, Storage Queue Data 
Contributor, Storage Queue Data Reader
 Subscription level (for all Storage Accounts), Resource group level, Storage level or Blob 
container/queue level.
 For users, groups, applications, managed service identities.
 You register your application in AD (App Registrations)
pg. 45
SKILLCERTPRO
o You can then assign roles to your application.
o Roles can also be assigned to Managed Service Identity (MSI)
 Can set up with Azure VMs, Function Apps, VM Scale Sets
 Credentials are injected into service instance (e.g. client id and certificate)
 Code calls local MSI endpoint to authenticate to the resource (e.g. 
storage)
 Easier management, no need to handle SAS tokens or manage keys.
Encrypt data in transit
 Enforced by enabling Secure Transfer
o Requires HTTPS for REST API
o Requires SMB 3.0 for Azure file service
 When moving data e.g. between
o Azure regions
o On-prem to Azure storage
 You can use Site-to-Site VPN, Point-to-Site VPN or Azure ExpressRoute.
 The data is moved across internet.
 �� Vulnerable to Azure, good to encrypt data.
o Configuration from outside Storage Account always requires SMB 3.0
o SMB 2.1 does not have encryption so it's only allowed between different Azure 
regions.
o Secure transfer required option is disabled by default.
 SAS tokens can specify only HTTPS can be used.
 You can also use client side encryption
o Encrypt data within the application.
o Double encrypted as Azure storage encrypts data as default.
o Still good idea to enforce HTTPS
 HTTPS has built-in integrity checks to avoid network data loss
o There are SDKS for e.g. C#, JAVA.
o Can leverage Azure Key vault to generate and/or store keys.
Encrypt data in rest
 Every storage account has encryption enabled by default and cannot be disabled.
 Required for many compliances e.g. privacy.
pg. 46
SKILLCERTPRO
Storage Service Encryption (SSE)
 Encrypts data before it's written
 Decrypts data before it's read
 Allows you to get encryption without any code
 Applies to Standard and Premium.
 Uses 256 bit AES.
 Keys are managed by Microsoft by default.
 Allows you to use your own encryption keys.
o ❗ Blobs and files only.
o ❗ Can only enable after the account is created.
o ❗ Key vault and storage account must be in same region
 Can be in different subscriptions
Azure Disk Encryption
 Encrypts data disks (VHD) of VMs.
 Handles both managed & unmanaged disks.
 Windows VMs: BitLocker encryption
 Linux VMs: DM-crypt
 Integrates with Key Vault to manage keys.
o ❗ Key Vault must reside in same region and subscription
o When uploading encrypted VM, you can upload encryption keys to Azure Key 
Vault first.
 Good for migrating as you can use same keys as on-premises.
Configure network
 By default, storage accounts are accessible by all networks including internet
 Allows you to create trust boundaries
 Setting up networking/firewall rule
o ❗ Denies all traffic by default unless any connection are explicitly opened
 In portal: Settings → Firewalls and Virtual Networks →Select Network
 You can have VNets from the same region as storage account or in a paired region.
 Firewall allows you to choose IP addresses that can access VMs
o E.g. you can set up only ExpressRoute access.
 When you configure Azure Storage firewalls and virtual networks
pg. 47
SKILLCERTPRO
4.1.2. Storage - Azure Storage - Monitoring
Monitoring
Activity Log Monitoring
 Management logs:
o Role assignments
o Regenerating Storage Account keys
o Changing Storage Account settings
 Not data plane logs e.g. new blob added, they're diagnostic logs
Activitiy Log Events
 Types include: • Administrative events • Service health events • Autoscale events • 
Recommendations • Security alerts • Alerts
 ❗ Stored for 19 days
 Archival possible
o To Storage Account
o To Event Hub
Storage Analytics
 Type of diagnostic logs
o Enabled in Diagnostic settings
 ❗ Retention period up to 365 days.
 Contains
o Details of read, write, and delete operations
o Reasons for failed requests
 Issues can be found through monitoring or reported by users
 Data includes: • Type of Operation • Success or Failure • Object Key • HTTP Status Code • 
Start Time • Server and E2E Latency • Authentication Type • IP Address of Caller • 
Browser Information • Type of Client • Client Operation ID • Server Operation ID
 Write blobs to blocks immediately
o ❗ Can take an hour until available as flush is waited.
o Search +/- 15 minutes and based on log metadata
 ❗ 20 TB limit, independent of Storage Account total limit.
pg. 48
SKILLCERTPRO
 You can download Microsoft Message Analyzer and analyze logs in a good UI instead 
of text files.
Storage Analytics Metrics
 Enabled as default
 Integrates with Azure monitor
o ❗ Data is stored 30 days.
 Setting up alerts
 Sends
o Capacity metrics
 For both storage accounts and individual storage services
 Sent to Azure monitor every hour
 Values are refreshed daily
o Transaction metrics
 Successful, failed, errors
 Ingress/Egress of data
 Service availability
o Performance metrics: Server latency, E2E (end-to-end) latency
 Metric dimensions: Response type, API calls, authentication type, geotype
Monitoring costs
 Estimating costs
o Azure Pricing Calculator
o Azure Total Cost of Ownership (TCO) Calculator
 Calculate the cost savings by migrating from on-premises to Azure
 End of month bills
o Invoice, detailed usage CSV file
Azure Cost Management
 Detailed cost analysis
o Consumption, cost, performance
o In portal
 Open scope (e.g. subscription or resource) → Click on code analysis blade
 Or go to "Cost Management" → "Cost analysis" and change scope on top
 Resource optimizations
o Identify underutilized resources
pg. 49
SKILLCERTPRO
 Budgets, alerts, action groups
o Compare costs against budget
 Cross-cloud
o Manage Azure, Amazon and Google cloud resources in one tool.
 In portal can be found
 � Replaces Cloudyn that was a third party cost management service which was acquired 
by Microsoft in 2017 and integrated in Azure Cost Management, Cloudyn is deprecated 
since 2020 but existing users can still user.
Monitoring costs using portal
 In Subscription → Cost Analysis
o Filter, view consumptions per resource/tags etc.
 Subscription → Invoices
o Shows invoices
o ❗ It does not show individual resources.
 To see them go to: Subscription → Manage and download invoices
Monitoring costs using Azure Billing APIs
 Non-enterprise customers
o Azure Resource RateCard API
 Pricelist across different regions/currencies
o Azure Resource Usage API
 Enterprise customers
o Balance and Summary API
o Usage Details API
o Marketplace Store Charge API
o Price Sheet API
o Billing Periods API
4.2. Storage - Azure Files
Azure Files
 99.9% SLA with availability, redundancy and disaster recovery.
 Typical use cases:
o Lift and shift
pg. 50
SKILLCERTPRO
o Hybrid solutions
o Born-in-cloud applications that require shared storage are
o Storage for cross-platform solutions
o Any workload that currently uses a file server or NAS providing SMB access
 REST compatible
 SMB-compatible
o File protocol over port 445
o Can be mounted by Linux & windows & macOS compatible
o Versions
 SMB 1: Limited block sizes, chatty protocol
 SMB 2.1 (Supported by Azure)
 No encryption
 Better network performance than SMB 1.0
 Group file shares, software shares
 Supported >Windows 7, > Windows Server 2008
 SMB 3 (Supported by Azure)
 Active-active support: Clustering with nodes
 Transparent failover
 RDMA support, multi channel > Lower latency
 Enables usage of SQL and Hyper-V
 Encryption support
 Supported > Windows 8, > Windows Server 2012
o Talks through port 445 and outbound connection
 Create Azure File Share
o Multiple Azure File shares can be created under a storage account
o Each has a name and optional quota assigned
 Quota limits the size up to 5120 GB
o In portal: Storage → Files → File Share
 File access
o Access is via standard SMB client
o Dialect of SMB is negotiated between the client and Azure Files upon connection
o Encryption used if outside the Azure region or if required as part of the storage 
account configuration
o SMB access utilizes the storage account name (as user name) and access key (as 
password).
o REST access can utilize SAS tokens
Azure File Snapshots
pg. 51
SKILLCERTPRO
 Delta snapshot of a file share
 Read-only, you can download your snapshot or mount it.
 Azure Backup can schedule and manage snapshots
 ❗ 200 snapshots per file share
 If the file share is deleted all snapshots are also deleted
Replication options
 DFS-R (before it was File Replication Service)
 xcopy, robocopy
 Considerations: locking of files, data consistency, amount of data replicated and 
maintaining ACLs.
Azure File Sync
 Enables replication from a single Azure Files share to one or more Windows based file 
servers
o Windows service are in a synchronization group.
 Utilizes an agent deployed on each Windows Server instance that's then registered with 
the Storage Sync service then added to a sync group.
Cloud tiering
 Least used data is moved to the cloud
o Leaves a thumbprint on the server providing transparent access
o Data is pulled down when access is requested.
 Tiering is based on maintaining a certain percentage of free space.
o Ensures around 20% is always free in file server.
 Can be disabled
 Is scoped to a file sync namespace.
 ❗ File must be higher than 64 KB
Quality of Service (QoS)
 Default configuration: Server will consume maximum possible bandwidth for data 
transfer via the storage sync service.
 Supports network limits to be configured
 For a VM based file server, QoS of the hypervisor can be used.
pg. 52
SKILLCERTPRO
Considerations
 Avoid actions that'd cause data to be pulled down from the cloud
o E.g. anti-virus scans, backups on-premises
 ACL (Access Control Lists) are replicated to the cloud but are not enforced when 
accessed via Azure Files.
o �� Content should be restored to an IaaS VM file server to enable ACL 
enforcement.
 Data can be pre-seeded via Azure Databox with some caveats
o Enables pre-seeding instead of full copy over the network.
 Be careful when combining other data replication technologies.
Workflow for replication
1. Deploy a storage account
2. Deploy a Azure File Share
3. Deploy Storage Sync service
o Must be in same region as storage account
4. Create a sync group
o Sync group has:
 Storage account & file share
 Server endpoints
 Cloud endpoints
5. Register server
i. On portal: Sync Service → Registered Service → Download Azure File Sync 
Agent
ii. Install the service and register the server
6. Add file share into the sync group as server endpoint
o �� You can have only 1 cloud endpoint for the same sync group
o You can enable/disable cloud tiering
7. Install agent on file server
o Supported >Windows Server 2012
o Selected files can be skipped
8. Register server to the storage sync service as server endpoint
Scale and Limits
 15 storage sync services per subscription
 30 sync groups per storage service
 1 cloud endpoint and 50 server endpoints per sync group
pg. 53
SKILLCERTPRO
 4 TB maximum space
 100 GB maximum file size
 64 KB minimum file size to be tiered
Troubleshooting
 Check if TCP 445 is open for outbound traffic.
 In metrics you can monitor for problems.
 On portal
o In Sync Services → Sync Groups → Group → See health status and action 
recommendations for problems for cloud and server endpoints
 In Event Viewer you can check FileSync events
4.3. Storage - Azure Backup
Azure Backup
 Backs up to Recovery Services Vault
 Online storage entity in Azure used to hold data such as backup copies, recovery points 
and backup policies.
 Storage account is automatically created an configured
o Comes with LRS and GRS storage account
 Configure in Vault → Backup Infrastructure → Backup Configuration
 All backups are listed and globally controlled in Backup Jobs
o You can monitor status and get reports
o You can filter the jobs
 Backup policy
o Settings
 Policy type
 Azure VM
 Azure File Share
 SQL Server in Azure VM
 Backup frequency
 Retention range: daily, weekly, monthly, yearly
 You can set inbuilt RBAC roles to vault
o Backup Operator
 Manage backups but cannot remove backup, create vault, give any roles.
o Others e.g. • Backup Reader • Monitoring Reader
pg. 54
SKILLCERTPRO
 Backup Alerts
o Vault → Backup Alerts → Configure notifications → Enable e-mail notifications → 
Choose severities (critical, warning, information) → Select notification (per alert or 
hourly digest)
 Enable MFA
o Properties → Security settings → Enable
o ❗ Cannot be disabled when enabled once.
 You generate Security PIN for critical options and Azure Backup will prompt for the pin 
(Properties → Security settings)
 When creating a VM back-up you can enable back-ups and choose a vault and policy.
o ❗ VM must be in same location as recovery vault
 To delete a vault, ensure all backups are stopped, delete backup agents/servers
 Azure Backup Reports
o On portal: Vault → Backup Reports → Diagnostic Settings → Turn on diagnostics
o You can save reports in you can archive reports in storage accounts, stream to 
event hubs, send to Log Analytics
o After you configure a storage account for reports by using a Recovery Services 
vault, you can connect Azure Backup from Power BI and get a dashboard.
Benefits
 Automatic storage management
 Unlimited scaling
 Application-consistent backup
o Each and every recovery point it has information for what it needs to go back to 
recovery point
 Data encryption both in-rest and and in-transit
 Unlimited data transfer
 Long-term retention without any time limit
Pricing
 Pay as you go storage model
 You pay per Protected Instance
o Protected instance is an application server/workload or computer that's been 
configured to back up to Microsoft Azure
Components
pg. 55
SKILLCERTPRO
Microsoft Azure IaaS VM Backup
 Features
o Policy-driven backup and retention
 Scheduled and on-demand backups, multiple recovery points
 You can hwoever use to backup directly with Backup Now
o Application-consistent backup
 No impact on production environment and no shutdown of VMs
o Fabric level backup
 Multiple backups, centralized management, detailed tracking
 ❗ New VM created by backup won't have backup policy associated with it.
 Restoring and file-recovery manually
o Go to back-up blade for VM.
 Two alternatives:
a. Back-up items → Select backup → Restore VM → Select snapshot
b. VM → Back-up
o Different alternatives:
a. Restore VM
 Two alternatives:
a. Create new VM
b. Restore disks
b. File recovery
. Select recovery point
a. Download script and execute on VM
 Mounts disks from the selected recovery point
 �� If files are larger than 100 GB, restore whole VM instead
b. Unmount disks after recovery
Microsoft Azure Backup MARS Agent
 Called also Recovery Services Agent
 For backing up on-premises computers to Azure
o Install back-up agent on local machine
o Need connectivity to Microsoft Azure
 Same configuration and control
o Centralized management of all on-premises back-ups
 Secure backup and recovery
o Protected Instance is registered with Azure
 Flow
pg. 56
SKILLCERTPRO
i. In recovery services in portal
a. Back-up
 Where is your workload running: On-premises
 What do you want to back-up:
 • Files and folders • Hyper-V • VMware • Microsoft SQL 
Server • Sharepoint • Exchange • System State • Bare Metal 
Recovery
b. Backup files and folders and system state
c. Download Recovery Services Agent from link provided
d. Download credentials to enter in the workstation
e. Transfer credentials & agents to the workstation
ii. Install the Azure backup client
 Select a password for encryption
iii. Setup the backup
 Click on Schedule Backup in agent
 Select files/folders
 Specify retention settings and policy
iv. Backup and restore file
 Click on Backup Now in agent
 Click on Recover Now in agent
Microsoft Azure Backup Server
 Centralized installation
o Can be installed on a server in Azure or on-premises
 Free
 Similar functionality as Data Protection Manager (DPM)
 Backup a variety of instances
o Workloads, VMWare and Hyper-V VMs, hosts, files, application workloads and 
barebone backups
 Flow
i. Create Backup in Site Recovery Service
 Go to Vault → Backup
 Get link for Azure Backup Server
ii. Install Azure Backup Server
 Installs SQL server
iii. Configure Azure Backup Server
a. Select management
b. Protection Servers → Register a server
pg. 57
SKILLCERTPRO
c. Disk Servers → Add a disk for configuration files
d. Create protection group
 Add servers, workstations and workloads to the group
 Can back-up to online and/or locally
e. Enable disk for backup data
iv. Recover with Azure Backup Server
 Select server → Click on Recover Now
5. Compute - Virtual machines (VMs)
Virtual Machines (VMs)
Concepts
 Storage resource provider (SRP)
o Disks (blob)
o Storage account
 Compute resource provider (CRP)
o VMs
 Networking resource provider (NRP)
o NICs, IP addresses, subnets load balancers..
Common VM Operations
Moving a VM
 Helps for
o high availability
o reduce latency for serving from VMs closer to users
 �� You can move virtual machines with the managed disks & in Availability Zones across 
subscriptions and VMs.
o ❗ Not supported:
 Virtual Machine Scale Sets.
 Virtual machines created from Marketplace resources with plans attached
 ❗ To move a virtual machine with a network interface card, you must move all dependent 
resources.
pg. 58
SKILLCERTPRO
o E.g. • virtual network for the network interface card • all other network interface 
cards for the virtual network • VPN gateways
 Virtual networks (classic) can't be moved.
 Can move across regions using
o Azure Resource Mover
o Using Azure Site Recovery by copying the data
Stopping a VM
 Deallocation
o ❗ If you shut down a VM inside VM, Azure still keeps the resources
 �� Deallocate instead
 Auto shutdown
o VM blade in Portal
Removing a VM*
 Deleting VM doesn't remove dependencies such as NICs, storages, OS/data disks, IP 
addresses
 �� Delete resource group instead, or use taxonomic tags
 PowerShell or CLI allows you to keep OS and/or Data disks
Azure VM Extensions
 Extends VM capabilities
 Requires Azure VM Agent (different for Windows or Linux)
o Marketplace images already have it
o For lift & shift, install agent first before uploading to cloud
 VM Access
o Backdoor to reset VM password reset
o Allows to modify RDP/SSH configurations
 VM Backup
o Allows to back-up VMs and configurations to recovery vault
 Custom Script
o Allows Desired State Configuration (DSC)
 You can script in Linux (bash), Windows (PowerShell)
 Puppet, chef etc
 Microsoft Monitoring Agent
o Onboards VM in Log Analytics
pg. 59
SKILLCERTPRO
Sizing
 Allows vertical scaling, e.g. CPU, RAM and other resources
 ❗ Resizing requires rebooting VM.
 Azure Compute Unit (ACU)
o Standardization without any hardware details
o 100 ACU = Small (Standard A1) VM
 A = Family
 1 = Size (versioned)
o DS_V3 = 160-190 ACU
o Good for estimating for lift and shift.
o As you raise ACU, per minute runtime charges increases.
 Types
Type Sizes Description
General 
purpose
B, Dsv3, Dv3, 
DSv2, Dv2, 
DS, D, Av2, 
A0-7
Balanced CPU-to-memory ratio. Ideal for testing and 
development, small to medium databases, and low 
medium traffic web servers.
Compute 
optimized Fsv2, Fs, F
High CPU-to-memory ratio. Good for medium traffic 
web servers, network appliances, batch processes, 
and application servers.
Memory 
optimized
Esv3, Ev3, M, 
GS, G, DSv2, 
DS, Dv2, D
High memory-to-CPU ratio. Great for relational 
database servers, medium to large caches, and inmemory analytics.
Storage 
optimized Ls
High disk throughput and IO. Ideal for Big Data, SQL 
and NoSQL databases.
GPU
NV, NC, 
NCv2, NCv3, 
ND
Specialized virtual machines targeted for heavy 
graphic rendering and viedo editing, as well as model 
pg. 60
SKILLCERTPRO
Type Sizes Description
training and inferencing (ND) with deep learning. 
Available with single or multiple GPUs
High 
performance 
compute
H, A8-11
Our fastest and most powerful CPU virtual machines 
with high-throughput network interfaces (RDMA).
Disk Types
 OS Disk
o ❗ Generation 1. VHD only
 If you use Generation 2 Hyper-V you need to convert from .vhdx to .vhd.
o Registered as SATA drive
o ❗ Maximum capacity of 1 TB
 Data Disk
o Dependent # on VM instance size
o Registered as SCSI disk
o ❗ Max capacity 4 TB
 Temprorary Disk
o D: or /dev/sdb1
o Bound to the hardware host
o Do not store permanent data!
Storage
Standard vs. Premium Disk Storage
 Standard Disks
o Backed by cost-effective HDDs
o High availability: several replication options
o Stored in Azure storage account
o Standard SSD available for managed disks (dev/test/entry elvel production 
applications)
o Standard storage provides maximum IOPS values for each VHD
o On portal
pg. 61
SKILLCERTPRO
 You can see disks in Azure Disks.
 Azure names managed disks like dc1_data-disk1, dc1_OSDisk for a VM 
named dc.
 By clicking on it, you can manage the disk.
 You can e.g. export, create a snapshot
 Premium Disks
o Backed by high-speed SSDs
o IOPS values are predictable, expected performance levels
o Pre-pay for all storage used (fixed sized disk sizes)
 �� Predictable speed and IOPS
 P10, 128 GB, 500 IOPs, 50 MB/sec
o ❗ Supports only Generation 1 VHD
 If you use Generation 2 Hyper-V you need to convert from .vhdx to .vhd.
 �� Azure Site Recovery migration handles this automatically
 On portal
 You can see unmanaged disks in Blob Containers → VHDs → you 
see VHDs
 A security problem is that someone by mistake can give public 
access to the blobs in the storage account.
Managed vs. unmanaged Disk Storage
 Unmanaged Disks
o Original method to store VM VHDS
 Legacy
o VHDS are stored as page blobs in an Azure storage account
o ❗ Maximum 256 TB of storage per VM
o ❗ You need to manage storage account availability
o ❗ 20,000 IOPS limit across all VM disks in a standard storage account
o In storage account they're in Blob Containers → VHDS container.
 They're leased
 They a re locked
 You need to stop & deallocate VMs to delete them
 You can break lease in Storage Explorer by right clicking
 Managed Disks
o �� Always use
o Azure manages the disks, you don't have to worry about storage account-level 
IOPS restrictions.
o Pre-pay for disk size (no need for SA)
pg. 62
SKILLCERTPRO
 S10, 128 GB, 500 IOPS, 60 MB/sec
o Supports Standard and Premium SSD and Standard HDD
o ❗ LRS replication only for Premium managed disks
o ❗ You can resize only when they're unattached or owner VM is stopped & 
deallocated
Costs
 Use Azure Pricing Calculator
 Optimizing costs
o �� Reserved Virtual Instances are the cheapest option.
 You pay 1 to 3 year term for a particular VM instance size in aspecific 
region.
o �� Reuse on-prem Microsoft licensens, up to 49% discount
 VM Chooser (azurevmchooser.kvaes.be)
o Open source applications to get recommendations
a. Give total VCPUs, RAMs etc.
b. Select a recommended VM
c. VM optimizer: Choose usage patterns, region etc.
IP addressing
 You always have a private IP and you can optionally have a public IP
 Public IP addresses
o Best practice is to never have a public IP
 Consider a load balancer to map the private IP.
o First 5 public IPs are free then it costs
o You have to NSG with an public IP
o Public IPv4 addresses can be associated with:
 VM vNICs, public load balancers, VPN gateways, and application gateways
o Public IP Address SKUs
 Basic SKU
 Open by default
 Static or dynamic allocation
 Standard SKU
 Secure by default (NSG)
 Static allocation only
 HA: Availability zone aware, can span to different availability zones
 DNS Naming
pg. 63
SKILLCERTPRO
o For VMs you can configure & use host name
o VM -> Overview -> Configure DNS Name then you can have 
like somename.eastus2.cloudapp.azure.com
Monitoring
Boot Diagnostics
 Periodic screenshots of the console
 Enables serial console
o You can connect to VM when you can't SSH/RDP for fixing e.g. boot state
o Requires you to have VM Contributor or higher privileges.
o No need to open SSH/RDP ports
Guest OS diagnostics
 Requires storage account
 Event logs, performence counters etc.
 Lowest level IaaS monitoring extension
 For more diagnostics:
o Windows: AzurePerformanceDiagnostics
o Linux: Linux Diagnostic Extension (LAD) 3.0
Azure Log Analytics
 Enabled by deploying the Microsoft Management Extension
 Onboards VMs into Log Analytics workspace
System Center Operations Manager (SCOM)
 Hybrid cloud approach
 You can track your cloud VMs on on-premises or visa versa
5.1. Compute - Virtual machines (VMs) - High Availability
pg. 64
SKILLCERTPRO
High Availability
 High Availability = Redundancy
 Layers of availability
i. Hardware-level availability
 Handled by Azure
ii. Server-level availability
 Availability Sets
 Ensures 99.95% SLA for VMs in availability set
 Provides server level fault tolerance within a single data center 
within a single region.
 Availability sets are containers/racks that's called Fault Domains.
 2 VMs in same Availability Sets = Azure places those in different 
availability sets.
 Update domains are different domains in different availability sets 
(fault Domains) and your VMs are set in different update domains 
as well.
 Protects availability against VM shutdowns because of 
update failures / hardware shutdowns.
 ❗ Must assign availability set at VM deployment
 ❗ Scaling (resizing) requires stopping all VMs in the availability set.
 For single VM not in availability set you have 99.9% availability if 
you use premium storage.
iii. Datacenter-level
 Availability Zones
 Allows you to place redundant VMs in different regions.
 Provides data center level tolerance.
 Load balancers are availability zone aware on standard SKU
 ❗ You have to use managed disks
iv. Region-level
 You need recovery service vault (storage for back-ups/replications)
 VM backup
 Ad-hoc or scheduled
 Includes all disks and configurations
 Azure Site Recovery
 Failover recovery
 15 minute RPO (recovery point objective)
 Azure-to-Azure (A2A) ASR Architecture
 Directly available in VM blade
pg. 65
SKILLCERTPRO
 All storage data, VMs, disks (managed and 
unmanaged), subnets etc.
 Prepared and ready to go in another 
region.
 In sync
 ❗ May require configuration with IP 
addresses
 You can failover to it and/or failback
 Configure in VM blade -> Disaster recovery
 Allows you to configure disaster recovery 
for single VM
 For workloads including multiple 
VMs you should configure it directly 
from Site Recovery
 You can choose to automate what happens 
using Automation runbooks.
 You can then view recovery status in same 
blade
 Replication health
 Recovery points
 Crash-consistent:
 Least preferable
 As if VM is replicate 
while it was powered 
off, no guarantees
 App-consistent
 Preferable point to 
recover
 Data and OS back
 Commit -> Finalizes the failover
 Re-protected -> Creates new 
recovery environment from old 
recovery environment (which 
becomes source environment)
 Migration to Azure
 On-premises to Azure
 AWS to Azure
pg. 66
SKILLCERTPRO
Azure Advisor
 Gives recommendation regarding high availability
 E.g.:
o Add more virtual machines for improved fault tolerance (medium impact)
o Enable VM backup to protect your data from corruption and accidental 
deletion (medium impact)
o Create an Azure service health alert (low impact)
VM Events
 Planned maintenance events
 Unexpected downtime events
 Notification
o In Azure support webpage, status webpage, twitter account
o Administrators get e-mail notifications
5.2 Compute - Virtual machines (VMs) - Deployment
Deployment
 Deployment tools
o • Azure portal • Azure Cloud Shell • Azure PowerShell • Azure CLI • Azure SDKs • 
ARM templates
 You can create from
o User images
 Uses unmanaged disks
o Marketplace images
Create VM Image
Generalizing VM
 Should be the first step
 Generalization resets server-specific data: Computer name
o Security identifiers (SIDs)
pg. 67
SKILLCERTPRO
o Local administrator/root identity
o Device driver cache
o Event logs
 How to generalize
o On Windows use sysprep, "System Preparation Tool"
o On Linux run sudo waagent -deprovision+user
o Take a VM backup first, because generalization is destructive and permanent
Create VM image from Azure VM
 Managed Disk Concepts
o Disks
 No storage account (management) required
 Pay for pre-allocated storage (P10 =128 GB SSD VHD)
o Snapshots
 Read-only full copy of a managed disks
 You can create new VMs based on snapshots
o Images
 Generalized VM disk images
 Snapshots can be converted into images
 Flow
i. Get an image
 Get a snapshot image
a. Go to Disks → Select OS disk → Create snapshot
b. In snapshot → Click on Export → You will get SAS url → Download 
VHD
c. Generalize the image
 Or capture an image
 In portal: VM → Overview → Capture
 ❗ Not generalized
 It appears in images
ii. Go to Images in portal, select the image, from there click on Deploy and it'll 
navigate you
VM Connection
 You have different levels of security NSG, host firewall, options to have public IP or not
pg. 68
SKILLCERTPRO
Just-in-time VM Access
 Allowed by Azure Defender (formerly known as Azure Security Center Standard tier)
 Locks down all administrator ports as default, when admin requests admin session then 
session is bounded by time limit and IP address restriction while granting access.
 No need to have management port open all the time
 �� Recommended to enable
Deploying Linux Server VM
 Around 40% of workloads in Azure runs on Linux
 Endorsed in Azure: CentOS, CoreOS, Debian, Oracle Linux, Red Hat Enterprise Linux, SUSE 
Enterprise Linux, openSUSE, Ubuntu
 Connection
o Secure Shell (SSH)
 A popular client is PuTTy for SSH or you can install subsystem for 
Linux or git tools on Windows 10 to get SSH.
o Remote Desktop Protocol (RDP)
 You can install RDP on Linux.
 Some do not believe in graphical shell:
 Presents security vulnerability possible
 Needlessly consumes CPU
 Windows team ported RDP into linux.
o Serial Console
 COM1 serial port connection to VM
 Low-level access
 Helpful when e.g. your VM doesn't boot up
 Authentication
i. SSH Public Key
 You keep private key and share public key with Azure.
ii. Password
 You can reset those after deployment in portal: VM → Reset password
Deploying Windows Server VM
 Windows Server 2019, 2016, 2012, 2008, Windows 10 Pro or Enterprise (for e.g. load 
testing, client-side testing, jump-box)
 Connect
o Remote Desktop Protocol (RDP)
pg. 69
SKILLCERTPRO
 Uses TCP 3389
 You can connect directly from Portal: Overview → Connect
o WinRM (PowerShell) Remoting
 TCP 5985, 5986
o Serial Console
 Text console into VM
 Can get to VMs that can't boot
Prepare environment with Azure Policy
 RBAC vs Azure Policy
o RBAC
 Focuses on user actions at different scopes
 VM Contributor can manage only VM
 Built-in custom roles
o Azure Policy
 Focuses on resource properties during deployment for already existing 
resources
 Uses default allow and explicit deny access system
o Difference
 You're not going to be able to create VM unless you have read & write 
abilities by RBAC
 Azure Policy in contrast constrains what that RBAC can do when she/he 
attempts to create VM
 Some built-in Azure Policy definitions are e.g. allowed locations, VM SKU, ensure MMS 
extension is deployed
 You can create also own policies, or initiatives which are collections of policies.
 Examples
o Policy definition e.g. allowed locations
o Parameters e.g. select which regions are allowed
Deploy with ARM templates
 ARM templates are infrastructure as code foundation of automation and DevOps in 
Azure
 �� Visual Studio is a good ARM template editor
o Visual Studio Code can also be used.
 Different ways to work with templates
pg. 70
SKILLCERTPRO
i. You can go to Portal → Templates → Usage existing usages or add a new 
template
ii. In Visual Studio → Cloud → Azure Resource Group → You can select template 
location (e.g. GitHub) → Select a template
iii. Deploy a VM then in the last step click on "Download template and parameters"
 You can deploy with PowerShell, Cloud Shell, Azure CLI, or directly from Visual Studio
 You can automate deployment actions such as VM access
 Files
o azuredeploy.json
 Deployment template.
 Defines resources and property such as allowedValues, defaultValue
 You can refactor some values in variables and reuse in the file
 copy element block in deployment script allows you to create e.g. 3 
storages.
o azuredeploy.parameters.json
 Deployment parameters (required for deployment) to 
deploy azuredeploy.json
5.3 Compute - Virtual machines (VMs) - VM Scale Sets (VMMS)
VM Scale Sets (VMSS)
 Group that holds identically configured VMs
 Used for
o Need to create and manage multiple VMs
 Centrally create and manage multple VMs (Windows Server or Linux)
o Need for high availability and app resiliency
 Horizontal scaling, scaling up and down based on spikes
o Need for large (1000) scale
 E.g. Azure Batch uses scale sets under the hood
o Need for IaaS autoscale
 Scale out and in based on metrics based autoscale
PaaS Scaling vs IaaS Scaling
 Azure App Service
o High agility at the expense of administrative power
o The underlying Hyper-V Vms are almost totally abstracted from you
pg. 71
SKILLCERTPRO
o Easy manual, scheduled, or automatic scale out and scale back
 Virtual Machine Scale Set (VMSS)
o Maximum administrative power at the expense of agility
o VMSS represents Azure's approach to IaaS horizontal scaling
Deploying a VM Scale Set
 Create virtual machine scale set
o Availability zone
 Scale scale sets across one and more availability zones
 ❗ All regions do not support availability zone
o Instance count & instance set
o Low priority
 Take advantage of unutilized capacity
 Compute power that customers/Microsoft is not using
 Save costs
 Good for workloads that can handle interruption
 Stateless workloads
 VMs in the scale set may be evicted at any time
 You set eviction policy:
 Stop / Deallocate
 Delete
o Use manage/unmanaged disks
 ❗ Managed disks are not supported with availability zones
o Networking
 Application Gateway
 �� Useful if your scale sets are web servers
 ❗ Do not support RDP
 Load Balancer
 Supports RDP
 You set public IP address name and domain name label (domainname.region.cloudapp.azure.com)
 You can also use ARM template e.g. Deploy a Windows VM Scale Set with a Custom Script 
Extension that deploys VMs, load balancer and a powershell script to be executed after 
deployment.
Connecting to VMs
 In portal: Choose VM → Settings → Instances you can see all the instances
pg. 72
SKILLCERTPRO
 To connect to individual instances you need load balancer and NAT (network address 
translation)
o You can't RDP/SSH into individual instances directly
o You can connect to load balancer IPs
 In portal: Load Balancer → Inbound NAT rules
o NAT maps different VMs on different ports.
Configuring Autoscale
 Manual: Through Portal/SDK/CLI/PowerShell
 Autoscale
 Scheduled: If you know when the load will be high you can plan for that and scale with 
time triggers
 Metrics: Use various metrics from various sources to determine when to scale in/out
 Manage in VMSS → Scaling →
o Enable auto-scaling
o Select scale-mode
o Scale based on metric
 Add rule
 E.g. increase instance count by 1 when CPU percentage above 70%
 �� You should also create scale mode that bring down the scale count
 Properties
 Duration: Good to not be confused when scaling out/in, so set a 
duration to e.g. 10 minutes
 Cooldown: Waits after scale operation before new scale operation
o Scale to specific instance count
 Time-based scaling
 Set start and end date
5.4. Compute - Virtual machines (VMs) - Security
Security
Role based access control
 Provides fine-grained access to resources
 AAA
pg. 73
SKILLCERTPRO
o A: Authentication (identity)
o A: Authorization (abilities)
o A: Accounting (auditing)
 Higher to lower granularity
o Management groups → Subscription → Resource group → Resource
 Roles
o Reader: Observers
o Resource-specific or custom role, contributor: Users managing resources
o Owner: Admins
 Custom roles are defined in JSON
 RBAC focuses on user actions at different scopes.
o By contrast, Azure Policy focuses on resource properties during deployment
 Policies e.g. Allowed virtual machine SKUs, Enforce automatic OS 
upgrade with app health checks on VMSS
 You can manage in Access Control (IAM) blade.
Storage Security
Storage Service Encryption
 Protects data at rest in storage account
 128-bit AES encryption
 Azure manages encryption keys
o �� You can manage them yourself with Azure Key Vault
Azure Disk Encryption
 BitLocker for Windows Server VMs
 DM-Crypt library for Linux VMs
 Protects OS and data disks
 Azure- or customer- managed disks
 Manage:
o In VM blade -> Disks -> Add data disk
o Use PowerShell
a. Create key vault and vault key
b. Create security principal (identity in Azure AD) that can take the key from 
key vault
c. You run SetRmVMDiskEncryption to configure encryption
pg. 74
SKILLCERTPRO
Network-level security
Network Security Group (NSG)
 Stateful firewalls
 Augmented security rules: Have inbound/outbound rules
 Can be bound to public addresses, load balancers, subnets and VMs.
 Traffic streams are identified with 5-tuple hash: Source, destination, port, protocol, IP 
addresses.
 Source can be service tags
o In-built e.g. Internet
 Or custom (Application Security Group identifiers)
o Simplifies NSGs
o Logically groups VMs e.g. by role
 Association is done through NICs
o E.g. AppServers, DatabaseServers
o Flow:
a. Define ASGs
b. Include ASGs in NSGs
Host Firewalls
 E.g. Windows Defender Firewall on Windows Server VMs
 �� A range that's whitelisted in NSG can be blocked by host firewalls.
Jumpbox Architecture
 Jumpbox is a pivot point VM in a VNet
 Good for auditing every administrative action
o A shared jumpbox makes it easier to administrate the orchestration
 You can e.g. allow access to public IP and make sure it's locked down to that endpoint.
 Or you can e.g. point to Site-to-Site VPN or point-to-site VPN.
Azure Security Center (ACS)
 Two tiers: Azure Security Center Free Tier, Azure Defender
 See also pricing page
pg. 75
SKILLCERTPRO
Azure Security Center Free Tier
 Continuous security assessment
 Actionable recommendations
 Prioritized alerts and incidents
 Integrated security solutions
o E.g. recommends to deploy WAF
Azure Defender
 Just-in-time VM Access
 Threat protection for Azure VMs and non-Azure servers
 Threat protection for PaaS services
 Regulatory compliance dashboard and reports
Just-in-Time (JIT) VM Access
 Allowed by Azure Defender for servers (formerly known as Azure Security Center 
Standard tier)
 Normally to access a VM, you need 3389 for RDP protocol, or 22 to SSH for linux, you 
open those ports 7/24.
o Not so secure as they're publicly accessible if IP is public.
 JIT locks down inbound administrative port access
 Time-restricted access to specific IP address(es)
5.5. Compute - Virtual machines (VMs) - Backups
Backups
VM Disk Snapshots
 .VHD files (data + os disks in page blobs) are stored aas page blobs.
 Full and incremental point-in-time snapshots
 Faster than performing full back-ups
o �� The difference is that snapshots are deltas
 Supported in
pg. 76
SKILLCERTPRO
 Managed disks
 Unmanaged disks
o Use AzCopy command line tool to archive to another storage account
 ❗ Snapshots cannot outlive their sources blob
 If you delete VMs, snapshots become irrelevant
o �� Consider archiving them
 You can create new VM from a snapshot.
 In Portal -> VM -> Disks -> Select Disk -> Create Snapshot
 In Snaphots -> Find snapshot ->
o Export:
o You export with creating SAS URL (time limited)
o You get direct URL
Azure VM Backup
MARS, Microsoft Agent Recovery Services
 Supports on-prem to cloud
 Supports file/folders but not whole disk back-up
System Center DPM (Data Protection Manager)*
 Supports system image/whole VM back-ups from on-premises to Azure
Azure Backup Server (MABS, Microsoft Azure Backup Server)
 Azure specific version of System Center DPM
Azure Backup
 Azure IaaS VM Backup
 Require recovery services vault
o Don't need to worry about storage accounts
 Azure Backup service uses VMSnapshot and VMSnapshotLinux extensions
 VSS orchestrates consistent snapshots of OS and data disks.
pg. 77
SKILLCERTPRO
Consistency levels
 Application-consistent
o �� Preferred backup type
o Data is consistent with time of backup (VSS)
 File-system consistent
o Ensures the VM boots and there is neither corruption nor data loss
o You may need to take further action to bring data current
 Crash-consistent
o Least preferred backup type
o Used when you back up a powered down VM
Manage
 VM -> Backup ->
o Create/select recovery services vault
o Create back-up policy with backup frequency and retention range
 You can see/start/stop back-ups in Recovery Services vault -> Backup Items
o You can create policies in Backup Policies blade.
 In back-up/replication jobs blade you can list all jobs
Restore options
 Create a new VM
o Basic VM up and running from a restore point
 Restore disk
o Restores a VM disk which can then be used to create a new VM.
o Azure Backup provides a template to help you customize and create a VM.
o Useful if you want to customize the VM, add configuration settings that weren't 
there at the time of backup, or add settings that must be configured using the 
template or PowerShell.
 Replace existing
o You can restore a disk, and use it to replace a disk on the existing VM.
o Supported for unencrypted managed VMs
o ❗ Not supported for unmanaged disks, generalized VMs, or for VMs created using 
custom images.
Recovery Options
 Entire VM
pg. 78
SKILLCERTPRO
o OS and data disks
o Configuration
o Restore to original or alternate location
o Quick create option
o Flow: Recovery Services Vault -> Restore VM -> Restore type: Create VM
 Individual Disks
o Restore to storage account
o Includes ARM deployment template
o �� Use to control VM restore, gain full control over the VM environment
 Availability set
 vNIC
 IP addresses...
o Flow
a. Recovery Services Vault -> Restore VM -> Restore type: disks
b. Restore VHD(s) to storage account
c. Create VM configuration
d. Attach the OS and data disks
 Files and Folders
o Mount OS and data disks as network drives
o Azure VM File Recovery
 E.g. "We need to retrieve a few log files from 3 months ago. Time is of the 
essence"
 If it was a VM back-up, it'd be costly as it takes storage etc.
 With file recovery you can only recover log folders
 Workflow
 Select recovery point
 Download and run PowerShell script
 Recover file system
 Unmount the disks after recovery
 Manage in Recovery Service Vault -> File Recovery
Azure Site Recovery
 Replication/orchestration engine
 Failover recovery for VMs
 You can use cloud <=> cloud, on-prem <=> cloud, on-prem <=> on-prem
 Provides region level failover
 Physical and virtual (Hyper-V and/or VMware) machines are supported
pg. 79
SKILLCERTPRO
 Azure as a recovery site
 Migrate to Azure
 Manage in VM -> Disaster Recovery or Recovery Services vault -> Site 
Recovery (or Recovery Services vault -> Disaster Recovery especially for VMs)
o Select target region
o Select target resources (e.g. VNEt, availability set, RG) to new resources or 
existing
o You can set storage, replication and extension settings
o With a recovery plan you can set recovery order, inject code in-between VMs
 You need to do it Recovery services vault
 Failover/Failback
o In VM -> Disaster Recovery ->
 Select Test failover or Failover
 Click on "Commit"
 Re-protect -> Go back to the original location
o Flow:
a. Prerequisite check
b. Failover
c. Create recovery point
d. Start the VM
e. Clean-up resources
6.1. Networking - Virtual Network (VNet)
Virtual Network (VNet)
 Communications and security boundary
o Provides network isolation and segmentations
o Enables Azure resources to communicate with each other securely
 E.g. VMs, storage accounts, App Service apps, Azure SQL database 
instances
 Uses Azure network backbone
o Communications are internal by default unless you explicitly make it external
 Name resolution
o Azure-provided DNS
o DNS service
 Traffic filtering
o NSGs
pg. 80
SKILLCERTPRO
o Network Virtual Appliances
 ❗ 50-100 VNets allowed per subscription
 ❗ A resource can only be created in a virtual network that exists in the same region and 
subscription as the resource.
 Why multiple VNets?
o Saving money
 Service chaining: Share a network virtual appliance among several VNets
o Segmenting workloads
 NSGs and UDRs give you routing and traffic control
 E.g. hub and spokes
o Securing traffic
 Private connectivity that uses the Microsoft backbone network
 Moving a VNet
o ❗ When moving a virtual network, you must also move its dependent resources
 For VPN Gateways
 You must move IP addresses, virtual network gateways, and all 
associated connection resources.
 �� Local network gateways can be in a different resource group.
o To move a peered virtual network, you must first disable the virtual network 
peering
o ❗ You can't move a virtual network to a different subscription if the virtual 
network contains a subnet with resource navigation links
 For example, if an Azure Cache for Redis resource is deployed into a 
subnet, that subnet has a resource navigation link.
Role of VNet
 You can link app services, storage accounts, VMs
 Provides traffic isolation and segmentation
 Runs on Azure backbone network
 Configure communication with Internet
o �� Ensure only VMs that need public IP addresses get one.
 You need to link VNets together to allow communication
 Control traffic flows into the VNET, within the VNET, and between VNets.
 Have IPv4 address space
o Uses CIDR block of private RFC 1918 addresses that are not public/internet 
routable themselves
 VNets are divided into subnets
o E.g. in multi-tiered application, web-tier, business-tier, data-tier
pg. 81
SKILLCERTPRO
 Good for protecting access using NSGs
 Good for having jumpbox and protecting who can connect to jump-box
VNet Design Best Practices
 Create subnets based on workloads
o E.g. all of your web front-ends will have similar access requirements, then you can 
bind NSGs on subnet level.
 Bind NSGs at the subnet level
o Not good to bind at VNet level for better troubleshooting
 Deploy a network virtual appliance (NVA) and user-defined routes (UDRs) to further 
customize traffic.
o Virtual appliance (NVA)
 E.g. enterprise grade firewall appliance, load balancer appliance
 They exist in Azure marketplace
 They'll be installed in VNet as a VM
o User defined routes (UDRs)
 Customize and control routing in a VNet
 Implement site-to-site or point-to-site VPN tunnels with on-premises environment
Deploying a VNet
 You can use ARM templates e.g. from Github.
o Visual Studio is recommended for editing templates
 During deployment:
o Name: Must be unique
o Subnet: Default gives you one subnet, for more you can use ARM template or 
PowerShell/CLI
o DDoS protection
 Microsoft publishes their datacenter public IP address
 Bad actors run port-scanners on those IP addresses all the time
o Service endpoints
 Allows you to integrate Azure PaaS services
 After deployment:
o Address space
 You cannot edit
 You need to create new and delete old one.
o Subnets
pg. 82
SKILLCERTPRO
 You can always add new subnets & deploy gateway subnet that'll be used 
by an Azure gateway.
o DNS server
 Default is azure provided
 You can use custom by additional DNS servers
 Affect all VMs
 Still uses Azure DNS when necessary
 Used when e.g. site-to-site or point-to-site connections, it'll affect 
all VMs.
o Diagram
 You can enable network watcher here.
 You then load in subscription or RG and enable.
 It shows topology
Network Security Groups (NSG)
 Stateful firewall for inbound and outbound traffic
o Stateful = 5-tuple hash
 Source + destination IP and ports
 Protocol
 Has default rules
 Augmented rules
o Allow you specify list of IP-addresses
o No need to create several rules for same list
 Service tags
o Azure defined named IP address endpoints
o E.g. Internet, VirtualNetwork, AzureLoadBalancer, AzureTrafficManager, Storage, S
QL, AzureCosmosDB, AzureKeyVault.
o Allows you to use names instead of IP addresses
 Application Security Groups (ASGs)
o Custom (user-defined) logical identifiers
o You can associate IP ranges and then use it as source/destination in NSGs.
o E.g. WebServer, WappServers, DbServers
 Can be bound to VNets, subnets or NICs
o �� Bind to subnets
 Security rules
o Priority: Lower the number, higher the priority of the rules
pg. 83
SKILLCERTPRO
IP Addressing Best Practices
 If a VM doesn't need a public IP address (PIP), then don't assign one and use an Azure 
load balancer instead.
 Plan your VNet private address space to avoid overlap.
o Different from on-premises
o Different from other VNets in Azure
 Never configure networking from within the VM
o Do it on Azure instead using Azure abstractions
Network Interfaces
 Assigned to a single subnet.
 Have a public or private IP that's dynamic or static.
 IP forwarding
o E.g. if you have network appliance and you want to give it ability to forwar traffic 
that's not destined for itself
6.1.1. Networking - Virtual Network (VNet) - Connecting VNets
Connecting VNets
 You don't need to have a Layer 3 router to route traffic from subnet to subnet
 Azure system routes take care of the routing for you automatically
Options
VPN Gateway
 Creates IPsec/IKEv2 tunnel and always-on connection
 Used for connecting VPNs in cloud or hybrid scenario.
pg. 84
SKILLCERTPRO
Inside Azure
VNet-to-VNet VPN
 Create isolation or administrative boundaries
 Provide cross-region geo-redundancy and replication securely
 No traffic crosses the public internet
 Separate VPN gateways costs while VNet peering is free.
 �� Make sure your VNet address spaces do not overlap.
 Troubleshooting
o Verify connectivity through peering
 Set up Azure DNS
VNet peering
 ❗ Seamless connection between two Azure VNets.
o The peered networks appear as one, for connectivity purposes.
o Name resolution does not flow, requires own DNS zone
 Runs on Azure backbone
 �� You can peer across regions and subcriptions
 Peering can overcome misplaced VMs
 Save money with service chaining (e.g. services' communication are chained through a 
subnet)
 ❗ Peering must be done on both sites
o VNet1 <=> VNet2 and VNet2 <=> VNet1
 Configuration
o Allow forwarded traffic
 Am I peering from a hub VNet that'll have IP-forwarder?
 Allow peers (other VNets) to forward traffic to go through.
o Allow gateway transit
 Am I hosting a VPN gateway?
o Use remote gateways
 Is this network use peer’s gateway?
 ❗ VNets must be in same region
 Enables force tunnelling
o E.g. when all Internet traffic must go through on-premises firewall device.
o You can use user defined routes for all outbound traffic to go back through VPN 
gateway to on-premises.
 ❗ Peerings are not transitive
pg. 85
SKILLCERTPRO
o If you peer spoke1 <=> spoke2 and spoke2 <=> spoke3 then spoke1 cannot 
communicate with spoke3 automatically.
o Common solution is transiting VNet with Hub and Spoke topology.
 Topology is a segmentation
 When to segment with VNets and when with subnets?
 Depends on bureaucratic reasons
 E.g. different VNets when
 Different cost centers/groups need management 
autonomy
 You want to completely isolate different workloads
 Name resolution needs configurations
 You can't do with Azure provided DNS as all your hosts have 
then internal.cloudapp.net
 In peering azure provided DNS won't work
 Troubleshooting tips
o Azure blocks ICMP between Vnets and the Internet
 ICMP is used for ping
 Microsoft blocks it because of DDoS attacks.
o Simplify NSGs as much as possible to reduce troubleshooting friction
o Azure portal Diagnose and solve problems/Resource health blade is useful
o Network Watcher and Network Permormance Monitor make troubleshooting 
much easier
 Network Watcher
 Shows where's the traffic is captured/denied
 Suite of tools
 Topology: e.g. VNETs, subnets, VMs, NICs
 Variable Packet Capture: Captures TCP packages at NIC 
level as wireshark files.
 IP Flow Verify: Troubleshoots NSG
 Next hop: Troubleshoots route tables
 Connection troubleshoot: Why it does not connect?
 Diagnostics Logging
 Security Group View
 NSG Flow Logging
 VPN Gateway Troubleshooting
 Network Subscription Limits
 Role Based Access Control
 In Portal you can search for Network Watcher and enable it on 
VMs
pg. 86
SKILLCERTPRO
 Network Performance Monitor
 E.g. top network health events, ExpressRoute monitor, service 
endpoint monitor, performance monitor
 It ties in logs/metrics with Log Analytics.
 Part of Insights & Analytics Azure management solution.
 Works with installing Microsoft Monitoring Agent (MMA) in VM.
 Flow
a. Deploy Insight & Analytics and then select Network 
Performance Monitor
b. Choose VM and click on "Connect", it'll 
install MicrosoftMonitoringAgent
Hybrid Connections
Site-to-site VPN
 Two VPN devices connect to each other.
 Flow
i. Deploy a VPN Gateway resource in Azure
 Requires gateway subnet (or DMZ subnet).
 Different SKUs: Basic, VpnGw1, VpnGw2, VpnGw3
 You get more bandwidth, site-to-site and point-to-site points.
 Don't use basic for production
 You can see the deployed VPN Gateway in Connected Devices in subnet.
ii. Deploy a Local Network Gateway as well.
 For your on-prem gateway device, you need to set up one of the route 
table configurations:
 PolicyBased
 Handle route tables manually
 ❗ Does not work with BGP failover, active-to-active 
configurations
 RouteBased
 �� Always use if possible
 Some VPN devices do not support it
 What's compatible is documented on Microsoft 
docs.
iii. Create a connection between two gateways
 Create local-to-azure in Local Network Gateway
 Create azure-to-local in VPN Gateway
 In Shared Key in connection blade, specify a key.
pg. 87
SKILLCERTPRO
Point-to-site VPN
 Allows access to Azure resources through VPN tunnel from a client agent.
 More portable way
 Flow
i. On Azure deploy VPN gateway
ii. In Point-to-site configuration blade download VPN client
iii. Deploy agent (a VPN Client) from VPN gateway
iv. Install on individual endpoints (e.g. laptops)
 Allows connection outside network perimeter
Express route
 High speed secure connection between on-prem and cloud
Best practices for High Availability
 Combine ExpressRoute and VPN
o In gateway subnet
 Deploy ExpressRoute gateway
 Deploy VPN Gateway
o Both gateways gives access to front-end tier and a jumpbox in a management 
subnet
o If ExpressRoute goes down VPN gateway gets activated
 Deploy two VPNs
o Requires enabling BGP in gateway link
 Robust routing
 Enable active-to-active connection configuration
 ❗ Only allowed RouteBased routing configuration
o Two VPN gateways on-prem
 Allows redundant active-to-active connection to single gateway.
 You have one active and one stand-by gateway
System Routes vs. User-defined Routes
 Situations
o You need to move one VM to another VNet.
 It requires re-deploying
o Isolation & segmentations
pg. 88
SKILLCERTPRO
 E.g. development / production VNet
o Hub & Spoke Topology
 Hub: VNet have Virtual Network Appliance (e.g. firewall), or gateway
 You don't want to have Virtual Network Appliance as it costs both 
money and resources.
 Spokes
 Other VNets (e.g. front-end, back-end)
 You can force communicates with each other through Hub.
 Internet calls and calls from internet
o Handled by Azure using system routes
o You don't need to manipulate them
 If you want to override system routes (e.g. for Hub & Spoke topology)
o You need User Defined Routing
o For network appliance you need to configure IP forwarding
 Enables it to pass on traffic that it's not destined for itself.
6.1.2. Networking - Virtual Network (VNet) - DNS & Name Resolution
DNS & Name Resolution
Azure-provided name resolution
 No configuration required
 All VMs within a VNet can resolve each others' host names
 ❗ Limitations
o Cross-VNet name resolution
o Issue: No custom DNS suffix
 You can add custom DNS server IP addresses
o E.g. in hybrid cloud if you want Azure VMs to have IP addresses from onpremises DNS server or vice versa.
o E.g. stand up own DNS servers in VNet instead.
o E.g. configure DNS forwarding between one DNS server in one VNet to another 
DNS server in another VNet
Azure DNS
 Allows VNETs to resolve each others host names.
pg. 89
SKILLCERTPRO
 Host your public DNS domain in Azure
o Use Azure geo-distributed name servers for high speed name resolution
o Delegate a domain:
a. Create a DNS Zone
b. Copy an Azure DNS name server from the zone
c. In the registrar's DNS management page, edit the NS records and replace 
the NS records with the Azure DNS name servers.
 You manage in Portal -> DNS zone
o Each DNS zone has
 VNets of associated with it
 Record-sets: IP addresses and host names of VMs
 Create private DNS zones
o Allows you to not route names in public DNS
o Linked to VNets
 Lets you avoid setting up own DNS infrastructure
o Registration VNet
 You create private DNS zone and registration VNet
 Any VMs within that VNet will automatically have their names registered 
and DNS records created in Azure DNS
o Resolution VNet
 Allows you to have name resolution across VNets
 Other VNets will be resolution VNets
 Allows you to create records (hosts, alias) for VMs and it'll support name 
resolution across VNets
Hybrid Cloud
 ❗Azure provided DNS won't work with peering.
 A potential solution:
o On-prem: Configure own DNS server and configure forward queries to Azure.
o In Azure
 Connect VNets (peer or VPN)
 Deploy own DNS servers in VNets and configure forwarding there
o ❗ Too much overhead
 �� Use Azure DNS Private Zones instead
o Configure Azure DNS servers specifically for private zones.
o One network: Registration network
 Hosts will have their names auto-registered in private zones.
o Other networks: Resolution networks
pg. 90
SKILLCERTPRO
 You need to manually create hosts in CNAME/MX records.
o Set-up DNS name for peered Virtual Appliance and a VNet in a Hub & Spoke 
topology
 Existing VMs
 [Host (spoke) VM] in [Host (spoke) VNet]
 [Hub (virtual appliance, hybrid)] VM in [Hub (virtual appliance, 
hybrid) VNet]
b. Create & set-up route table
a. Create a route table -> Routes -> Add ->
 Name: E.g. subnet1-nva
 Address prefix: If destination IP of a packet matches this 
then it matches the rules. E.g. 192.168.8.0/24
 Next hop type: Virtual network gateway, virtual network, 
internet, virtual appliance, none.
 Choose [Hub (virtual appliance, hybrid) VM]
 Set next-hop address to IP of [Hub (virtual appliance, 
hybrid) VM]
b. Associate route table to related subnets
 Route-table -> Subnets -> Associate subnet
c. Set-up peering
 You can ping to VNets as name resolution does not work across 
VNets
 Set-up without any allow forwarded traffic, allow gateway 
transit, use remote gateways configuration
 [Hub (virtual appliance, hybrid) VNet] <=> [Host (spoke) 
VNet]
d. Create DNS Zone
 In portal -> DNS zone -> Add DNS zone
 Create private DNS zone in VA (hybrid) VNet
 Create DNS zone
 Register record set with IP and name of each VM
 Register two VNets
 Registration VNET for [Hub (virtual appliance, 
hybrid) VM]
 Resolution VNET for [Host (spoke) VM]
6.2. Networking - Load Balancers
pg. 91
SKILLCERTPRO
Load Balancer Options
 All load balancers are software appliances (software defined networking: SDN)
 �� Only Standard (not Basic) SKU allows availability zones in Load balancer
Public Load Balancer
 OSI Layer 4 TCP and UDP
 Internet-facing, has public IP address
 Offers two distribution modes
 Set-up public load balancer
i. Settings -> Back-end-pools-> Add VMs
ii. Settings -> Health-probe -> Add health probe
 E.g. tcp-80-probe (HTTP) probe
 Set interval -> time between prop events
 Set unhealth threshold (e.g. 2) before VM is dropped out from the pool
 Add load balancing port
 Incoming request from port 80 (port) will be passed to TCP passed 80 
(back-end port)
 Select backend pool & health-probe
 Set session persistence
 Floating IP (direct server return)
 Use with internal load balancers
 Use with SQL server always on cluster
 Used when same back-end port needs to be used across multiple 
rules in a single Load Balancer.
iii. Add inbound NAT rule
 Map TCP 5000 to a VMs RDP port (3389)
 Map TCP 5000 to a VMs RDP port (3389)
Internal load balancer
 OSI Layer 4 TCP and UDP
 Applies to traffic only within a virtual network
o No public IP address
 Good for applying load balancing to n-tier application services (database)
pg. 92
SKILLCERTPRO
Application Gateway
 OSI Layer 7 application
 Application Delivery Controller (ADC) as a service
 SSL offload
 Has Web Application Firewall (WAF)
Traffic Manager
 DNS-level
 Geographical load balancing
 Offers different routing methods