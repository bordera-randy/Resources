# 🚀 Azure DevOps Terraform Pipeline Guide

**Complete Setup Guide for CI/CD Infrastructure as Code**

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Azure DevOps Project Setup](#azure-devops-project-setup)
3. [Service Connection Configuration](#service-connection-configuration)
4. [Repository Structure](#repository-structure)
5. [Pipeline YAML Configuration](#pipeline-yaml-configuration)
6. [Terraform Backend Configuration](#terraform-backend-configuration)
7. [Variable Groups & Secrets](#variable-groups--secrets)
8. [Pipeline Triggers & Gates](#pipeline-triggers--gates)
9. [Multi-Environment Setup](#multi-environment-setup)
10. [Troubleshooting & Best Practices](#troubleshooting--best-practices)

---

## Prerequisites

Before starting, ensure you have:

### Required Tools & Access
- ✓ Azure DevOps Organization (azure.microsoft.com/services/devops)
- ✓ Azure Subscription with appropriate permissions
- ✓ Terraform CLI installed locally (v1.0+)
- ✓ Git (for source control)
- ✓ Visual Studio Code or preferred editor
- ✓ Service Principal credentials (for Azure authentication)

### Permissions Required
- **Azure DevOps:** Project Administrator or higher
- **Azure Subscription:** Contributor or Owner role
- **GitHub/Azure Repos:** Read/Write access to repository

### Knowledge
- Basic understanding of Terraform
- Familiarity with YAML syntax
- Understanding of CI/CD concepts

---

## Azure DevOps Project Setup

### Step 1: Create Azure DevOps Organization

1. Navigate to https://dev.azure.com
2. Click **New organization**
3. Select region and accept terms
4. Name your organization (e.g., `MyCompanyDevOps`)

### Step 2: Create Project

1. In your organization, click **New project**
2. Configure:
   - **Project name:** `InfrastructureAsCode` (or your preference)
   - **Visibility:** Private (for production code)
   - **Version control:** Git
   - **Work item process:** Agile (or Scrum)
3. Click **Create**

### Step 3: Create Repositories

1. Go to **Repos** tab
2. Initialize or import Terraform repository:
   - **Option A:** Create new repo and clone locally
   - **Option B:** Import existing GitHub repo
3. Create folder structure:
   ```
   terraform/
   ├── dev/
   ├── staging/
   ├── prod/
   ├── modules/
   └── shared/
   
   pipelines/
   ├── terraform-plan.yml
   ├── terraform-apply.yml
   └── terraform-destroy.yml
   ```

---

## Service Connection Configuration

### Step 1: Create Service Principal in Azure

```bash
# Login to Azure
az login

# Create Service Principal
az ad sp create-for-rbac \
  --name "terraform-devops-sp" \
  --role Contributor \
  --scopes /subscriptions/<SUBSCRIPTION_ID>

# Output will show:
# appId (Client ID)
# password (Client Secret)
# tenant (Tenant ID)
```

### Step 2: Configure Service Connection in Azure DevOps

1. Navigate to **Project Settings** → **Service Connections**
2. Click **New service connection**
3. Select **Azure Resource Manager**
4. Choose **Service principal (manual)**
5. Configure:
   - **Subscription Name:** Your Azure subscription name
   - **Subscription ID:** Your subscription ID
   - **Tenant ID:** From Service Principal output
   - **Service Principal ID (Client ID):** From Service Principal output
   - **Service Principal key (Client Secret):** From Service Principal output
   - **Service connection name:** `AzureRM-Terraform`
6. Click **Save**

### Step 3: Grant Permission to Service Principal

```bash
# Optional: Add additional role assignments
az role assignment create \
  --assignee <CLIENT_ID> \
  --role "User Access Administrator" \
  --scope /subscriptions/<SUBSCRIPTION_ID>
```

---

## Repository Structure

### Recommended Layout

```
my-terraform-repo/
│
├── .gitignore                 # Git exclusions
├── README.md                  # Project documentation
├── terraform.tfvars.example   # Example variables
│
├── terraform/
│   ├── variables.tf           # Variable definitions
│   ├── outputs.tf             # Output values
│   ├── main.tf                # Primary configuration
│   ├── providers.tf           # Provider configuration
│   ├── backend.tf             # Remote backend config
│   │
│   ├── modules/               # Reusable modules
│   │   ├── networking/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   └── outputs.tf
│   │   ├── compute/
│   │   └── storage/
│   │
│   └── environments/          # Environment-specific configs
│       ├── dev/
│       │   ├── terraform.tfvars
│       │   └── backend.tf
│       ├── staging/
│       │   ├── terraform.tfvars
│       │   └── backend.tf
│       └── prod/
│           ├── terraform.tfvars
│           └── backend.tf
│
├── pipelines/
│   ├── terraform-plan.yml     # Plan pipeline
│   ├── terraform-apply.yml    # Apply pipeline
│   └── terraform-destroy.yml  # Destroy pipeline
│
├── scripts/
│   ├── validate.sh            # Validation script
│   ├── format-check.sh        # Format checking
│   └── security-scan.sh       # Security scanning
│
└── docs/
    ├── SETUP.md               # Setup guide
    ├── RUNBOOK.md             # Operational runbook
    └── TROUBLESHOOTING.md     # Troubleshooting guide
```

### .gitignore Example

```
# Terraform files
*.tfstate
*.tfstate.*
*.tfvars
!*.tfvars.example
.terraform/
.terraform.lock.hcl
crash.log
crash.*.log

# IDE
.vscode/
.idea/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db

# Secrets
.env
secrets.txt
```

---

## Pipeline YAML Configuration

### Pipeline 1: Terraform Plan (PR Validation)

**File: `pipelines/terraform-plan.yml`**

```yaml
trigger:
  branches:
    include:
    - main
    - develop
  paths:
    include:
    - terraform/**
    - pipelines/**

pr:
  branches:
    include:
    - main
  paths:
    include:
    - terraform/**

pool:
  vmImage: 'ubuntu-latest'

variables:
  terraformVersion: '1.6.0'
  backendStorageAccount: 'tfstate$(environment)'
  backendResourceGroup: 'rg-terraform-state'
  backendContainerName: 'tfstate'

stages:
- stage: Validate
  displayName: 'Validate Terraform'
  jobs:
  - job: ValidateTerraform
    displayName: 'Validate & Format Check'
    steps:
    
    - task: TerraformInstaller@0
      displayName: 'Install Terraform'
      inputs:
        terraformVersion: $(terraformVersion)
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Init'
      inputs:
        provider: 'azurerm'
        command: 'init'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
        backendServiceArm: 'AzureRM-Terraform'
        backendAzureRmResourceGroupName: $(backendResourceGroup)
        backendAzureRmStorageAccountName: $(backendStorageAccount)
        backendAzureRmContainerName: $(backendContainerName)
        backendAzureRmKey: 'terraform.tfstate'
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Validate'
      inputs:
        provider: 'azurerm'
        command: 'validate'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Format Check'
      inputs:
        provider: 'azurerm'
        command: 'custom'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
        customCommand: 'fmt'
        customArguments: '-check -recursive'
      continueOnError: true
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Plan'
      inputs:
        provider: 'azurerm'
        command: 'plan'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
        environmentServiceNameAzureRM: 'AzureRM-Terraform'
        commandOptions: '-var-file="environments/$(environment)/terraform.tfvars" -out=tfplan'

- stage: SecurityScan
  displayName: 'Security Scanning'
  dependsOn: Validate
  condition: succeeded()
  jobs:
  - job: Checkov
    displayName: 'Run Checkov Security Scan'
    steps:
    
    - task: UsePythonVersion@0
      displayName: 'Install Python'
      inputs:
        versionSpec: '3.x'
    
    - script: |
        pip install checkov
        checkov -d terraform/ \
          --framework terraform \
          --output cli \
          --quiet
      displayName: 'Run Checkov'
      continueOnError: true
    
    - script: |
        echo "##[warning]Review security scan results above"
      displayName: 'Security Scan Complete'

- stage: PlanOutput
  displayName: 'Display Plan'
  dependsOn: Validate
  condition: succeeded()
  jobs:
  - job: DisplayPlan
    displayName: 'Show Terraform Plan'
    steps:
    
    - task: PublishBuildArtifacts@1
      displayName: 'Publish Terraform Plan'
      inputs:
        pathToPublish: '$(System.DefaultWorkingDirectory)/terraform'
        artifactName: 'terraform-plan'
      continueOnError: true
    
    - script: |
        echo "##[section]Terraform plan completed successfully"
        echo "Review the plan output above before approving apply"
      displayName: 'Plan Summary'
```

### Pipeline 2: Terraform Apply (Main Branch)

**File: `pipelines/terraform-apply.yml`**

```yaml
trigger:
  branches:
    include:
    - main
  paths:
    include:
    - terraform/**

pool:
  vmImage: 'ubuntu-latest'

variables:
  terraformVersion: '1.6.0'
  environment: 'prod'
  backendStorageAccount: 'tfstateprod'
  backendResourceGroup: 'rg-terraform-state'
  backendContainerName: 'tfstate'

stages:
- stage: Plan
  displayName: 'Plan Infrastructure Changes'
  jobs:
  - job: PlanJob
    displayName: 'Generate Plan'
    steps:
    
    - task: TerraformInstaller@0
      displayName: 'Install Terraform'
      inputs:
        terraformVersion: $(terraformVersion)
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Init'
      inputs:
        provider: 'azurerm'
        command: 'init'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
        backendServiceArm: 'AzureRM-Terraform'
        backendAzureRmResourceGroupName: $(backendResourceGroup)
        backendAzureRmStorageAccountName: $(backendStorageAccount)
        backendAzureRmContainerName: $(backendContainerName)
        backendAzureRmKey: 'terraform.tfstate'
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Plan'
      inputs:
        provider: 'azurerm'
        command: 'plan'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
        environmentServiceNameAzureRM: 'AzureRM-Terraform'
        commandOptions: '-var-file="environments/$(environment)/terraform.tfvars" -out=tfplan'
    
    - task: PublishBuildArtifacts@1
      displayName: 'Publish Plan'
      inputs:
        pathToPublish: '$(System.DefaultWorkingDirectory)/terraform'
        artifactName: 'tfplan-$(Build.BuildId)'

- stage: ManualApproval
  displayName: 'Manual Approval Gate'
  dependsOn: Plan
  condition: succeeded()
  jobs:
  - job: waitForValidation
    displayName: 'Wait for Manual Approval'
    pool: server
    timeoutInMinutes: 1440  # 24 hours
    steps:
    - task: ManualValidation@0
      inputs:
        notifyUsers: 'terraform-team@company.com'
        instructions: 'Review plan and approve to apply infrastructure changes'

- stage: Apply
  displayName: 'Apply Infrastructure Changes'
  dependsOn: ManualApproval
  condition: succeeded()
  jobs:
  - job: ApplyJob
    displayName: 'Apply Changes'
    steps:
    
    - task: TerraformInstaller@0
      displayName: 'Install Terraform'
      inputs:
        terraformVersion: $(terraformVersion)
    
    - task: DownloadBuildArtifacts@0
      displayName: 'Download Plan'
      inputs:
        artifactName: 'tfplan-$(Build.BuildId)'
        downloadPath: '$(System.DefaultWorkingDirectory)'
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Init'
      inputs:
        provider: 'azurerm'
        command: 'init'
        workingDirectory: '$(System.DefaultWorkingDirectory)/tfplan-$(Build.BuildId)/terraform'
        backendServiceArm: 'AzureRM-Terraform'
        backendAzureRmResourceGroupName: $(backendResourceGroup)
        backendAzureRmStorageAccountName: $(backendStorageAccount)
        backendAzureRmContainerName: $(backendContainerName)
        backendAzureRmKey: 'terraform.tfstate'
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Apply'
      inputs:
        provider: 'azurerm'
        command: 'apply'
        workingDirectory: '$(System.DefaultWorkingDirectory)/tfplan-$(Build.BuildId)/terraform'
        environmentServiceNameAzureRM: 'AzureRM-Terraform'
        commandOptions: 'tfplan'
    
    - task: PublishBuildArtifacts@1
      displayName: 'Publish State File'
      inputs:
        pathToPublish: '$(System.DefaultWorkingDirectory)/tfplan-$(Build.BuildId)/terraform'
        artifactName: 'terraform-state-$(Build.BuildId)'
      condition: succeeded()
```

### Pipeline 3: Terraform Destroy (Manual Trigger)

**File: `pipelines/terraform-destroy.yml`**

```yaml
trigger: none

pr: none

pool:
  vmImage: 'ubuntu-latest'

variables:
  terraformVersion: '1.6.0'
  backendResourceGroup: 'rg-terraform-state'
  backendContainerName: 'tfstate'

parameters:
- name: environment
  displayName: 'Environment to Destroy'
  type: string
  default: 'dev'
  values:
  - dev
  - staging
  - prod

stages:
- stage: ConfirmDestroy
  displayName: 'Confirm Destruction'
  jobs:
  - job: waitForValidation
    displayName: 'CONFIRM DESTRUCTION'
    pool: server
    timeoutInMinutes: 60
    steps:
    - task: ManualValidation@0
      inputs:
        notifyUsers: 'terraform-admin@company.com'
        instructions: 'CAUTION: This will DESTROY all infrastructure in ${{ parameters.environment }}. Click Resume to confirm.'

- stage: Destroy
  displayName: 'Destroy Infrastructure'
  dependsOn: ConfirmDestroy
  condition: succeeded()
  jobs:
  - job: DestroyJob
    displayName: 'Run Terraform Destroy'
    steps:
    
    - task: TerraformInstaller@0
      displayName: 'Install Terraform'
      inputs:
        terraformVersion: $(terraformVersion)
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Init'
      inputs:
        provider: 'azurerm'
        command: 'init'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
        backendServiceArm: 'AzureRM-Terraform'
        backendAzureRmResourceGroupName: $(backendResourceGroup)
        backendAzureRmStorageAccountName: 'tfstate${{ parameters.environment }}'
        backendAzureRmContainerName: $(backendContainerName)
        backendAzureRmKey: 'terraform.tfstate'
    
    - task: TerraformTaskV4@4
      displayName: 'Terraform Destroy'
      inputs:
        provider: 'azurerm'
        command: 'destroy'
        workingDirectory: '$(System.DefaultWorkingDirectory)/terraform'
        environmentServiceNameAzureRM: 'AzureRM-Terraform'
        commandOptions: '-var-file="environments/${{ parameters.environment }}/terraform.tfvars" -auto-approve'
```

---

## Terraform Backend Configuration

### Step 1: Create Azure Storage for State

```bash
# Variables
RESOURCE_GROUP="rg-terraform-state"
STORAGE_ACCOUNT="tfstatedev$(date +%s)"
CONTAINER="tfstate"
LOCATION="eastus"

# Create resource group
az group create \
  --name $RESOURCE_GROUP \
  --location $LOCATION

# Create storage account
az storage account create \
  --resource-group $RESOURCE_GROUP \
  --name $STORAGE_ACCOUNT \
  --sku Standard_LRS \
  --encryption-services blob

# Get storage account key
ACCOUNT_KEY=$(az storage account keys list \
  --resource-group $RESOURCE_GROUP \
  --account-name $STORAGE_ACCOUNT \
  --query '[0].value' -o tsv)

# Create blob container
az storage container create \
  --name $CONTAINER \
  --account-name $STORAGE_ACCOUNT \
  --account-key $ACCOUNT_KEY

# Output values (save for later)
echo "Storage Account: $STORAGE_ACCOUNT"
echo "Resource Group: $RESOURCE_GROUP"
echo "Container: $CONTAINER"
echo "Account Key: $ACCOUNT_KEY"
```

### Step 2: Configure Backend in Terraform

**File: `terraform/backend.tf`**

```hcl
terraform {
  backend "azurerm" {
    # These values are provided by DevOps pipeline
    # Do NOT hardcode them in source control
  }
}
```

**File: `terraform/environments/dev/backend.tf`**

```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "rg-terraform-state"
    storage_account_name = "tfstatedev"
    container_name       = "tfstate"
    key                  = "dev/terraform.tfstate"
  }
}
```

### Step 3: Initialize Backend Locally

```bash
# Navigate to environment directory
cd terraform/environments/dev

# Initialize with backend config
terraform init

# Verify state is remote
terraform state list
```

---

## Variable Groups & Secrets

### Step 1: Create Variable Group in DevOps

1. Go to **Pipelines** → **Library**
2. Click **+ Variable group**
3. Name: `terraform-dev-vars`
4. Add variables:

```
TF_VAR_location          = "eastus"
TF_VAR_environment       = "dev"
TF_VAR_resource_prefix   = "dev"
TERRAFORM_VERSION        = "1.6.0"
AZURE_TENANT_ID          = "00000000-0000-0000-0000-000000000000"
```

### Step 2: Add Secrets

1. Click **+ Add** (at bottom)
2. Toggle "Keep this value secret" ✓
3. Add sensitive variables:

```
ARM_CLIENT_ID            = <Service Principal Client ID>
ARM_CLIENT_SECRET        = <Service Principal Secret>
ARM_TENANT_ID            = <Tenant ID>
ARM_SUBSCRIPTION_ID      = <Subscription ID>
```

### Step 3: Link Variable Group to Pipeline

In pipeline YAML:

```yaml
variables:
  - group: terraform-dev-vars  # References variable group

stages:
  - stage: Deploy
    jobs:
    - job: TerraformApply
      steps:
      - script: echo $(TF_VAR_location)
        displayName: 'Reference Variable'
```

---

## Pipeline Triggers & Gates

### Branch Policy Configuration

1. Go to **Repos** → **Branches**
2. Click **⋯** next to main branch → **Branch policies**
3. Configure:
   - **Require pull request reviews:** Yes
   - **Required reviewers:** 2
   - **Check for linked work items:** Yes
   - **Require a successful build:** Yes

### Add Build Validation

1. Under **Build validation:**
   - Click **+**
   - **Build pipeline:** Select `terraform-plan`
   - **Path filter:** `/terraform/**`
   - **Display name:** Terraform Plan Validation

### Step Gates for Production

1. In **terraform-apply** pipeline
2. Add stage condition:

```yaml
stages:
- stage: ManualApproval
  displayName: 'Require Human Approval'
  dependsOn: Plan
  condition: succeeded()
  jobs:
  - job: waitForValidation
    pool: server
    timeoutInMinutes: 1440
    steps:
    - task: ManualValidation@0
      inputs:
        notifyUsers: 'devops-team@company.com'
        instructions: 'Review terraform plan and infrastructure changes'
```

---

## Multi-Environment Setup

### Strategy 1: Separate Pipelines

Create individual pipelines for each environment:
- `terraform-plan-dev.yml`
- `terraform-plan-staging.yml`
- `terraform-plan-prod.yml`

**Advantages:**
- Different approval processes
- Environment-specific triggers
- Clear separation

**Disadvantages:**
- Duplicated YAML
- Maintenance overhead

### Strategy 2: Parameterized Pipeline

Single pipeline with environment parameter:

```yaml
parameters:
- name: environment
  displayName: 'Target Environment'
  type: string
  default: 'dev'
  values:
  - dev
  - staging
  - prod

variables:
  environment: ${{ parameters.environment }}
  backendStorageAccount: 'tfstate${{ parameters.environment }}'

stages:
- stage: Deploy
  displayName: 'Deploy to ${{ parameters.environment }}'
  jobs:
  - job: TerraformApply
    steps:
    - task: TerraformTaskV4@4
      inputs:
        commandOptions: '-var-file="environments/${{ parameters.environment }}/terraform.tfvars"'
```

### Environment-Specific Variables

**`terraform/environments/dev/terraform.tfvars`**

```hcl
location       = "eastus"
environment    = "dev"
vm_count       = 1
vm_size        = "Standard_B2s"
enable_scaling = false
```

**`terraform/environments/prod/terraform.tfvars`**

```hcl
location       = "eastus"
environment    = "prod"
vm_count       = 3
vm_size        = "Standard_D4s_v3"
enable_scaling = true
```

---

## Troubleshooting & Best Practices

### Common Issues & Solutions

#### Issue 1: Backend State Lock

**Error:** `Error acquiring the lease for Azure Blob Storage`

**Solution:**
```bash
# Check for locked state
az storage blob show \
  --account-name tfstatedev \
  --container-name tfstate \
  --name terraform.tfstate.lock \
  --query properties.lease

# Force unlock (use with caution)
az storage blob lease break \
  --account-name tfstatedev \
  --container-name tfstate \
  --blob-name terraform.tfstate.lock
```

#### Issue 2: Service Principal Permissions

**Error:** `InvalidScope: Scope provided in the token is not valid`

**Solution:**
```bash
# Grant subscription-level permissions
az role assignment create \
  --assignee <CLIENT_ID> \
  --role "Contributor" \
  --scope "/subscriptions/<SUBSCRIPTION_ID>"

# Verify permissions
az role assignment list \
  --assignee <CLIENT_ID>
```

#### Issue 3: Pipeline Timeout

**Error:** `Task timeout occurred while waiting for approval`

**Solution:**
Increase timeout in pipeline:

```yaml
- job: waitForValidation
  pool: server
  timeoutInMinutes: 2880  # 48 hours
```

### Best Practices

#### 1. State Management

```hcl
# Enable remote state locking
terraform {
  backend "azurerm" {
    skip_provider_registration = false
  }
}

# Prevent accidental state deletion
prevent_destroy = true
```

#### 2. Code Quality

```bash
# Format check in pipeline
terraform fmt -check -recursive

# Lint with TFLint
tflint --init
tflint --format compact
```

#### 3. Security

```yaml
# Scan for secrets before commit
- task: TruffleHogSecretScanning@0

# Use managed identities instead of service principals (when possible)
- task: UseManagedIdentity@1

# Rotate secrets regularly (every 90 days)
```

#### 4. Documentation

```hcl
# Add descriptions to all variables
variable "location" {
  type        = string
  description = "Azure region for resource deployment"
  
  validation {
    condition     = contains(["eastus", "westus", "northeurope"], var.location)
    error_message = "Location must be a supported region."
  }
}
```

#### 5. Cost Management

```yaml
# Add cost estimation to plan
- script: |
    terraform plan -json | \
    jq '.resource_changes[] | 
        select(.change.actions[] == "create") | 
        .address' > new_resources.txt
  displayName: 'Estimate New Resources'
```

### Monitoring & Logging

```yaml
# Enable debug logging
- task: TerraformTaskV4@4
  env:
    TF_LOG: DEBUG
    TF_LOG_PATH: $(Build.ArtifactStagingDirectory)/terraform.log

# Publish logs
- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: '$(Build.ArtifactStagingDirectory)/terraform.log'
    artifactName: 'terraform-logs'
```

---

## Advanced Topics

### Terraform Modules

**Structure:**
```
modules/
├── networking/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── README.md
└── compute/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    └── README.md
```

**Usage:**
```hcl
module "networking" {
  source = "./modules/networking"
  
  location       = var.location
  environment    = var.environment
  vnet_cidr      = "10.0.0.0/16"
}

module "compute" {
  source = "./modules/compute"
  
  location       = var.location
  subnet_id      = module.networking.subnet_id
  vm_size        = var.vm_size
}
```

### Remote State with Workspaces

```bash
# Create workspace for different deployments
terraform workspace new prod
terraform workspace select prod

# Use in code
locals {
  workspace = terraform.workspace
}
```

### Policy as Code (Sentinel)

```hcl
# sentinel.hcl
policy "require_azure_tags" {
  enforcement_level = "mandatory"
}

policy "restrict_instance_types" {
  enforcement_level = "soft-mandatory"
}
```

---

## Quick Reference Commands

```bash
# Local Development
terraform init                    # Initialize Terraform
terraform plan                    # Preview changes
terraform apply                   # Apply changes
terraform destroy                 # Destroy resources
terraform fmt                     # Format code
terraform validate                # Validate syntax

# Remote State
terraform state list              # List resources
terraform state show <resource>   # Show resource details
terraform state rm <resource>     # Remove from state
terraform refresh                 # Sync with real resources

# Debugging
terraform plan -json | jq .       # Parse plan as JSON
terraform graph                   # Visualize dependencies
TF_LOG=DEBUG terraform plan       # Enable debug logging
```

---

## Security Considerations

✓ **DO:**
- Store secrets in Azure Key Vault
- Use managed identities when available
- Implement approval gates for production
- Enable audit logging
- Rotate service principal secrets regularly
- Use separate service principals per environment
- Enable backend state encryption
- Validate all inputs with `validation` blocks

✗ **DON'T:**
- Commit `.tfvars` files with secrets
- Use hardcoded credentials in code
- Skip approval for production changes
- Disable state locking
- Share service principal credentials
- Run `terraform destroy` without confirmation
- Store state files in version control

---

**Last Updated:** February 1, 2026

**Related:** [← Back to Student Resources](/README.md) | [Terraform Guide](../../whitepapers/terraform/) | [Azure DevOps Docs](https://learn.microsoft.com/en-us/azure/devops/)
