# Terraform Basics

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Basic Commands](#basic-commands)
5. [Examples](#examples)
6. [Tips](#tips)
7. [Resources](#resources)

## Introduction
Terraform is an open-source infrastructure as code software tool created by HashiCorp. It allows users to define and provision data center infrastructure using a high-level configuration language.

## Installation
To install Terraform, follow these steps:
1. Download the appropriate package for your operating system from the [Terraform downloads page](https://www.terraform.io/downloads.html).
2. Unzip the package and place the `terraform` binary in a directory included in your system's `PATH`.

## Configuration
Create a new directory for your Terraform configuration files. Inside this directory, create a file named `main.tf` with the following content:

```hcl
provider "aws" {
    region = "us-west-2"
}

resource "aws_instance" "example" {
    ami           = "ami-0c55b159cbfafe1f0"
    instance_type = "t2.micro"
}
```

## Basic Commands
- `terraform init`: Initialize a new or existing Terraform configuration.
- `terraform plan`: Create an execution plan.
- `terraform apply`: Apply the changes required to reach the desired state of the configuration.
- `terraform destroy`: Destroy the Terraform-managed infrastructure.

## Examples
### Example 1: Creating an AWS EC2 Instance
```hcl
provider "aws" {
    region = "us-west-2"
}

resource "aws_instance" "example" {
    ami           = "ami-0c55b159cbfafe1f0"
    instance_type = "t2.micro"
}
```

### Example 2: Creating an S3 Bucket
```hcl
provider "aws" {
    region = "us-west-2"
}

resource "aws_s3_bucket" "example" {
    bucket = "my-unique-bucket-name"
    acl    = "private"
}
```
### Example 3: Creating an Azure Virtual Machine
```hcl
provider "azurerm" {
    features {}
}

resource "azurerm_resource_group" "example" {
    name     = "example-resources"
    location = "West US"
}

resource "azurerm_virtual_network" "example" {
    name                = "example-network"
    address_space       = ["10.0.0.0/16"]
    location            = azurerm_resource_group.example.location
    resource_group_name = azurerm_resource_group.example.name
}

resource "azurerm_subnet" "example" {
    name                 = "example-subnet"
    resource_group_name  = azurerm_resource_group.example.name
    virtual_network_name = azurerm_virtual_network.example.name
    address_prefixes     = ["10.0.2.0/24"]
}

resource "azurerm_network_interface" "example" {
    name                = "example-nic"
    location            = azurerm_resource_group.example.location
    resource_group_name = azurerm_resource_group.example.name

    ip_configuration {
        name                          = "internal"
        subnet_id                     = azurerm_subnet.example.id
        private_ip_address_allocation = "Dynamic"
    }
}

resource "azurerm_virtual_machine" "example" {
    name                  = "example-machine"
    location              = azurerm_resource_group.example.location
    resource_group_name   = azurerm_resource_group.example.name
    network_interface_ids = [azurerm_network_interface.example.id]
    vm_size               = "Standard_DS1_v2"

    storage_os_disk {
        name              = "example-os-disk"
        caching           = "ReadWrite"
        create_option     = "FromImage"
        managed_disk_type = "Standard_LRS"
    }

    storage_image_reference {
        publisher = "Canonical"
        offer     = "UbuntuServer"
        sku       = "18.04-LTS"
        version   = "latest"
    }

    os_profile {
        computer_name  = "example-machine"
        admin_username = "adminuser"
        admin_password = "Password1234!"
    }

    os_profile_linux_config {
        disable_password_authentication = false
    }
}
```

### Example 4: Creating a Google Cloud Storage Bucket
```hcl
provider "google" {
    project = "my-gcp-project"
    region  = "us-central1"
}

resource "google_storage_bucket" "example" {
    name     = "my-unique-bucket-name"
    location = "US"
}
```

## Tips
- Always use version control for your Terraform configuration files.
- Regularly run `terraform plan` to check for potential changes before applying them.
- Use modules to organize and reuse your Terraform code.

## Resources
- [Terraform Documentation](https://www.terraform.io/docs/index.html)
- [HashiCorp Learn](https://learn.hashicorp.com/terraform)
- [Terraform GitHub Repository](https://github.com/hashicorp/terraform)
