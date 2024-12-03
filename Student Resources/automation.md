# Automation Guide using Azure, PowerShell, and Terraform

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Azure Automation](#azure-automation)
    - [Setting up Azure CLI](#setting-up-azure-cli)
    - [Creating a Resource Group](#creating-a-resource-group)
- [PowerShell Automation](#powershell-automation)
    - [Installing Azure PowerShell Module](#installing-azure-powershell-module)
    - [Creating a Virtual Machine](#creating-a-virtual-machine)
- [Terraform Automation](#terraform-automation)
    - [Setting up Terraform](#setting-up-terraform)
    - [Creating Infrastructure with Terraform](#creating-infrastructure-with-terraform)
- [Examples](#examples)
    - [Creating a Resource Group](#creating-a-resource-group-1)
    - [Creating a Virtual Machine](#creating-a-virtual-machine-1)
- [Conclusion](#conclusion)

## Introduction
This guide provides an overview of how to automate tasks using Azure, PowerShell, and Terraform. Automation can help streamline processes, reduce errors, and save time.

## Prerequisites
- Azure Subscription
- Azure CLI installed
- PowerShell installed
- Terraform installed

## Azure Automation

### Setting up Azure CLI
1. Install Azure CLI from the [official documentation](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
2. Log in to your Azure account:
    ```sh
    az login
    ```

### Creating a Resource Group
1. Create a resource group using Azure CLI:
    ```sh
    az group create --name MyResourceGroup --location eastus
    ```

## PowerShell Automation

### Installing Azure PowerShell Module
1. Open PowerShell and install the Azure module:
    ```powershell
    Install-Module -Name Az -AllowClobber -Force
    ```
2. Import the module:
    ```powershell
    Import-Module Az
    ```

### Creating a Virtual Machine
1. Use the following script to create a VM:
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

## Terraform Automation

### Setting up Terraform
1. Download and install Terraform from the [official website](https://www.terraform.io/downloads.html).
2. Initialize Terraform:
    ```sh
    terraform init
    ```

### Creating Infrastructure with Terraform
1. Create a `main.tf` file with the following content:
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
2. Apply the configuration:
    ```sh
    terraform apply
    ```

## Examples

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
By using Azure CLI, PowerShell, and Terraform, you can automate the creation and management of Azure resources efficiently. This guide provides a starting point for automating your cloud infrastructure.
