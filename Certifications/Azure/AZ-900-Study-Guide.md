# AZ-900 Study Guide

Microsoft Azure Fundamentals

------------------------------------------------------------------------

## Table of Contents

1. [Learning Path 01 -- Cloud Concepts](#learning-path-01----cloud-concepts)
    - [What is Cloud Computing?](#what-is-cloud-computing)
    - [Cloud Models](#cloud-models)
    - [CapEx vs OpEx](#capex-vs-opex)
    - [Cloud Benefits](#cloud-benefits)
    - [Service Types](#service-types)
    - [Shared Responsibility](#shared-responsibility)
2. [Learning Path 02 -- Azure Architecture & Services](#learning-path-02----azure-architecture--services)
    - [Core Architecture](#core-architecture)
    - [Compute Services](#compute-services)
    - [Networking](#networking)
    - [Storage](#storage)
    - [Identity & Security](#identity--security)
3. [Learning Path 03 -- Management & Governance](#learning-path-03----management--governance)
    - [Cost Management](#cost-management)
    - [Governance](#governance)
    - [Deployment Tools](#deployment-tools)
    - [Monitoring](#monitoring)
4. [Final Exam Focus](#final-exam-focus)

------------------------------------------------------------------------


# Learning Path 01 -- Cloud Concepts

## What is Cloud Computing?

Cloud computing is the delivery of computing services over the internet,
enabling: - Faster innovation - Flexible resources - Economies of
scale - Pay-as-you-go pricing

## Cloud Models

### Public Cloud

-   Owned by cloud provider
-   Shared resources
-   No capital expenditure (CapEx)

### Private Cloud

-   Owned & managed by organization
-   Full control over hardware
-   Requires CapEx

### Hybrid Cloud

-   Combines public + private
-   Flexible workload placement

## CapEx vs OpEx

CapEx = Upfront hardware costs\
OpEx = Pay-as-you-go model (Azure uses OpEx)

## Cloud Benefits

-   High availability
-   Scalability
-   Elasticity
-   Reliability
-   Predictability
-   Security
-   Governance
-   Manageability

## Service Types

### IaaS

Infrastructure control (VMs, storage, networking)

### PaaS

Application hosting without OS management

### SaaS

Fully managed software (e.g., Microsoft 365)

## Shared Responsibility

IaaS → You manage OS & apps\
PaaS → You manage apps & data\
SaaS → You manage data & access

------------------------------------------------------------------------

# Learning Path 02 -- Azure Architecture & Services

## Core Architecture

Hierarchy: Management Groups → Subscriptions → Resource Groups →
Resources

### Regions

60+ global regions supporting data residency

### Availability Zones

Physically separate datacenters within a region

### Region Pairs

\~300 miles apart with replication support

## Compute Services

-   Virtual Machines (IaaS)
-   VM Scale Sets (auto-scale)
-   Availability Sets
-   Azure Virtual Desktop
-   Containers
-   Azure Functions (serverless)
-   Azure App Service (PaaS)

## Networking

-   Virtual Network (VNet)
-   Subnets
-   Peering
-   Public vs Private Endpoints
-   VPN Gateway
-   ExpressRoute
-   Azure DNS

## Storage

-   Storage Accounts (globally unique)
-   Redundancy: LRS, ZRS, GRS, RA-GRS
-   Tiers: Hot, Cool, Archive
-   Tools: AzCopy, Storage Explorer, File Sync
-   Migration: Azure Migrate, Data Box

## Identity & Security

-   Microsoft Entra ID
-   Entra Domain Services
-   MFA
-   Conditional Access
-   RBAC
-   Zero Trust
-   Defense in Depth
-   Microsoft Defender for Cloud

Authentication = Who you are\
Authorization = What you can do

------------------------------------------------------------------------

# Learning Path 03 -- Management & Governance

## Cost Management

-   Pricing Calculator
-   Azure Cost Management
-   Budgets & Alerts
-   Tags for cost tracking

## Governance

-   Azure Policy
-   Resource Locks (ReadOnly/Delete)
-   Service Trust Portal
-   Microsoft Purview

## Deployment Tools

-   Azure Portal
-   Azure CLI
-   Azure PowerShell
-   Cloud Shell
-   Azure Arc
-   ARM Templates (JSON)
-   Bicep

## Monitoring

-   Azure Advisor
-   Azure Service Health
-   Azure Monitor
-   Log Analytics
-   Application Insights

------------------------------------------------------------------------

# Final Exam Focus

✔ IaaS vs PaaS vs SaaS\
✔ Shared responsibility\
✔ Regions & availability zones\
✔ Resource hierarchy\
✔ Compute comparison\
✔ Storage redundancy\
✔ RBAC & Conditional Access\
✔ Cost tools\
✔ Azure Monitor & Advisor
