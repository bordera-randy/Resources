# Automation Guide: Azure, PowerShell, and Terraform

> **Automate cloud infrastructure with Azure CLI, PowerShell, and Terraform.**

Streamline processes, reduce errors, and save time by automating Azure resource management. This guide covers setup, core commands, and practical examples.

---

## 📚 Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Azure Automation](#azure-automation)
- [PowerShell Automation](#powershell-automation)
- [Terraform Automation](#terraform-automation)
- [Examples](#examples)
- [Conclusion](#conclusion)
- [Back to Top](#automation-guide-azure-powershell-and-terraform)

---

## Introduction

This guide demonstrates how to automate Azure infrastructure tasks using three powerful tools:
- **Azure CLI:** Command-line interface for Azure management
- **PowerShell:** Scripting and automation with Azure PowerShell module
- **Terraform:** Infrastructure as Code (IaC) for declarative resource management

Each tool has strengths—choose based on your workflow and team expertise.

---

## Prerequisites

**You'll need:**
- Azure subscription (free tier available)
- Azure CLI installed
- PowerShell installed
- Terraform installed

### Installing Prerequisites

#### Azure CLI
1. Download from [official documentation](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
2. Verify installation:
    ```sh
    az --version
    ```

#### PowerShell
1. Download from [official documentation](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell)
2. Verify installation:
    ```powershell
    $PSVersionTable.PSVersion
    ```

#### Terraform
1. Download from [official website](https://www.terraform.io/downloads.html)
2. Follow OS-specific installation instructions
3. Verify installation:
    ```sh
    terraform -v
    ```

---

## Azure Automation

**Azure CLI** provides cross-platform command-line access to Azure resources.

### Setting up Azure CLI
1. Install from [official documentation](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
2. Log in to Azure:
    ```sh
    az login
    ```
3. Set default subscription (optional):
    ```sh
    az account set --subscription "Your-Subscription-Name"
    ```

### Creating a Resource Group
```sh
az group create --name MyResourceGroup --location eastus
```

**Tip:** List available locations with `az account list-locations -o table`

---

## PowerShell Automation

**Azure PowerShell** provides cmdlets for managing Azure resources via PowerShell scripts.

### Installing Azure PowerShell Module
1. Open PowerShell as Administrator and install the Azure module:
    ```powershell
    Install-Module -Name Az -AllowClobber -Force
    ```
2. Import the module:
    ```powershell
    Import-Module Az
    ```
3. Connect to Azure:
    ```powershell
    Connect-AzAccount
    ```

### Creating a Virtual Machine
```powershell
$resourceGroup = "MyResourceGroup"
$location = "East US"
$vmName = "MyVM"
$cred = Get-Credential

New-AzVm `
    -ResourceGroupName $resourceGroup `
    -Name $vmName `
    -Location $location `
    -Credential $cred `
    -ImageName "Win2019Datacenter"
```

**Tip:** Use `-WhatIf` to preview changes before applying them.

---

## Terraform Automation

**Terraform** enables Infrastructure as Code (IaC) with declarative configuration files.

### Setting up Terraform
1. Download from [official website](https://www.terraform.io/downloads.html)
2. Initialize Terraform in your project directory:
    ```sh
    terraform init
    ```
3. (Optional) Configure Azure authentication:
    ```sh
    az login
    ```

### Creating Infrastructure with Terraform
1. Create a `main.tf` file:
    ```hcl
    provider "azurerm" {
      features {}
    }

    resource "azurerm_resource_group" "example" {
      name     = "MyResourceGroup"
      location = "East US"
    }

    resource "azurerm_virtual_network" "example" {
      name                = "example-network"
      address_space       = ["10.0.0.0/16"]
      location            = azurerm_resource_group.example.location
      resource_group_name = azurerm_resource_group.example.name
    }
    ```
2. Preview changes:
    ```sh
    terraform plan
    ```
3. Apply the configuration:
    ```sh
    terraform apply
    ```

**Tip:** Use `terraform destroy` to tear down infrastructure when done.

---

## Examples

**Side-by-side comparisons** of common tasks across all three tools.

### Creating a Resource Group

#### Using Azure CLI
```sh
az group create --name MyResourceGroup --location eastus
```

#### Using PowerShell
```powershell
New-AzResourceGroup -Name "MyResourceGroup" -Location "East US"
```

#### Using Terraform
```hcl
resource "azurerm_resource_group" "example" {
    name     = "MyResourceGroup"
    location = "East US"
}
```

### Creating a Virtual Machine

#### Using Azure CLI
```sh
az vm create \
    --resource-group MyResourceGroup \
    --name MyVM \
    --image Win2019Datacenter \
    --admin-username azureuser \
    --generate-ssh-keys
```

#### Using PowerShell
```powershell
$resourceGroup = "MyResourceGroup"
$location = "East US"
$vmName = "MyVM"
$cred = Get-Credential

New-AzVm `
        -ResourceGroupName $resourceGroup `
        -Name $vmName `
        -Location $location `
        -Credential $cred `
        -ImageName "Win2019Datacenter"
```

#### Using Terraform
```hcl
resource "azurerm_virtual_machine" "example" {
    name                  = "MyVM"
    location              = azurerm_resource_group.example.location
    resource_group_name   = azurerm_resource_group.example.name
    network_interface_ids = [azurerm_network_interface.example.id]
    vm_size               = "Standard_DS1_v2"

    storage_os_disk {
        name              = "myosdisk"
        caching           = "ReadWrite"
        create_option     = "FromImage"
        managed_disk_type = "Standard_LRS"
    }

    storage_image_reference {
        publisher = "MicrosoftWindowsServer"
        offer     = "WindowsServer"
        sku       = "2019-Datacenter"
        version   = "latest"
    }

    os_profile {
        computer_name  = "hostname"
        admin_username = "azureuser"
        admin_password = "Password1234!"
    }

    os_profile_windows_config {}
}
```


## Conclusion

By mastering Azure CLI, PowerShell, and Terraform, you can:
- **Automate** repetitive tasks
- **Version control** your infrastructure
- **Reduce errors** through consistency
- **Scale** operations efficiently

**Next steps:**
- Explore CI/CD integration with Azure DevOps or GitHub Actions
- Learn about state management in Terraform
- Study Azure Resource Manager (ARM) templates as an alternative

---

**Back to [Student Resources](../README.md)**
