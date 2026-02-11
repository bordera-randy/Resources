# AZ-104 -- Most Failed Areas

Microsoft Azure Administrator Associate

## Table of Contents

1. [RBAC vs Entra Roles](#1-rbac-vs-entra-roles)
2. [Storage Replication Differences](#2-storage-replication-differences)
3. [NSG Rule Evaluation](#3-nsg-rule-evaluation)
4. [Service Endpoints vs Private Endpoints](#4-service-endpoints-vs-private-endpoints)
5. [Availability Sets vs Availability Zones](#5-availability-sets-vs-availability-zones)
6. [App Service Plan vs Web App](#6-app-service-plan-vs-web-app)
7. [Autoscale Logic](#7-autoscale-logic)
8. [Route Tables & UDRs](#8-route-tables--udrs)
9. [Backup Vault Types](#9-backup-vault-types)
10. [Monitoring -- Metrics vs Logs](#10-monitoring----metrics-vs-logs)
11. [Conditional Access vs NSG](#11-conditional-access-vs-nsg)
12. [Scope Hierarchy](#12-scope-hierarchy)
13. [AKS vs ACI vs Container Apps](#13-aks-vs-aci-vs-container-apps)
14. [Final Reality](#final-reality)

------------------------------------------------------------------------

## 1. RBAC vs Entra Roles

**Entra roles** manage the directory.  
**RBAC roles** manage Azure resources.

### Key Differences

| Control Type | Controls |
|--------------|----------|
| Entra Role | Identity directory |
| RBAC Role | Azure resources |

**Common failures:**

- Confusing scope inheritance
- Assigning wrong role type
- Ignoring deny assignments

------------------------------------------------------------------------

## 2. Storage Replication Differences

### Replication Types

| Type | Zones | Regions | Read Access |
|----------|-------|---------|-------------|
| LRS | 1 | 1 | No |
| ZRS | 3 | 1 | No |
| GRS | 1 | 2 | No |
| RA-GRS | 1 | 2 | Yes |
| GZRS | 3 | 2 | No |
| RA-GZRS | 3 | 2 | Yes |

**Common failures:**

- Not knowing sync vs async replication
- Not knowing which provides read access
- Misunderstanding zone vs region protection

------------------------------------------------------------------------

## 3. NSG Rule Evaluation

Traffic must be allowed at:

- Subnet NSG
- NIC NSG

**Lower priority number wins.**

**Common failure:** Allowing traffic at NIC but blocking at subnet.

------------------------------------------------------------------------

## 4. Service Endpoints vs Private Endpoints

| Service Endpoint | Private Endpoint |
|------------------|------------------|
| Public endpoint remains | Private IP in VNet |
| Extends VNet identity | Fully private connectivity |
| Simpler | More secure |

**Common failure:** Choosing Service Endpoint when Private Endpoint is required.

------------------------------------------------------------------------

## 5. Availability Sets vs Availability Zones

| Feature | Protects From |
|---------|---------------|
| Availability Set | Hardware failure |
| Availability Zone | Datacenter failure |

**SLA:**

- Availability Set = 99.95%
- Availability Zone = 99.99%

------------------------------------------------------------------------

## 6. App Service Plan vs Web App

App Service Plan defines:

- Region
- VM size
- Pricing tier
- Scaling

**Scaling the app scales the plan.**

**Common failure:** Thinking scaling is per app instead of per plan.

------------------------------------------------------------------------

## 7. Autoscale Logic

Must define:

- Minimum instances
- Maximum instances
- Default instance count

Can scale based on:

- Metrics (CPU, memory, requests)
- Schedule

**Common failure:** Forgetting scale-in rules or cooldown settings.

------------------------------------------------------------------------

## 8. Route Tables & UDRs

- System routes exist by default
- UDR overrides system routes
- Next hop types matter

**Common failure:** Routing 0.0.0.0/0 incorrectly to firewall or appliance.

------------------------------------------------------------------------

## 9. Backup Vault Types

**Vault types:**

- Recovery Services Vault
- Backup Vault

**Common failure:** Confusing VM backups with storage backups.

**Soft delete default retention:** 14 days.

------------------------------------------------------------------------

## 10. Monitoring -- Metrics vs Logs

| Metrics | Logs |
|---------|------|
| Near real-time | Stored records |
| Numeric | Structured |
| Lightweight | Queryable (KQL) |

**Common failure:** Choosing wrong alert signal type.

------------------------------------------------------------------------

## 11. Conditional Access vs NSG

**Conditional Access** = Identity-based  
**NSG** = Network-based

They operate in different control planes.

------------------------------------------------------------------------

## 12. Scope Hierarchy

1. Management Group
2. Subscription
3. Resource Group
4. Resource

**Inheritance flows downward.**

**Common failure:** Assuming RG-level assignment applies to entire subscription.

------------------------------------------------------------------------

## 13. AKS vs ACI vs Container Apps

| Service | Orchestration Level |
|---------|---------------------|
| ACI | None |
| Container Apps | Managed |
| AKS | Full Kubernetes |

**Common failure:** Choosing ACI for complex orchestration scenarios.

------------------------------------------------------------------------

## Final Reality

The exam tests:

- Order of evaluation
- Scope inheritance
- Failure domains
- Network flow
- Responsibility boundaries

**Memorization is not enough. You must reason operationally.**
