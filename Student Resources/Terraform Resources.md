
# Terraform Resources

## Table of Contents
- [Basic Info About Terraform](#basic-info-about-terraform)
- [How Terraform Works](#how-terraform-works)
- [Key Concepts](#key-concepts)
- [How to Install Terraform](#how-to-install-terraform)
- [How to Use Terraform](#how-to-use-terraform)
    - [Installation](#installation)
    - [Configuration](#configuration)
    - [Basic Commands](#basic-commands)
    - [Examples](#examples)
        - [Example 1: Creating an AWS EC2 Instance](#example-1-creating-an-aws-ec2-instance)
        - [Example 2: Creating an S3 Bucket](#example-2-creating-an-s3-bucket)
        - [Example 3: Creating an Azure Virtual Machine](#example-3-creating-an-azure-virtual-machine)
        - [Example 4: Creating a Google Cloud Storage Bucket](#example-4-creating-a-google-cloud-storage-bucket)
- [Learn Terraform on Different Cloud Providers](#learn-terraform-on-different-cloud-providers)

## Basic Info About Terraform
Terraform is an open-source infrastructure as code software tool created by HashiCorp. It enables users to define and provision data center infrastructure using a high-level configuration language known as HashiCorp Configuration Language (HCL), or optionally JSON.

## How Terraform Works
Terraform uses a simple, human-readable language called HashiCorp Configuration Language (HCL) to define infrastructure as code. The process of using Terraform typically involves the following steps:

1. **Write Configuration**: Define the desired state of your infrastructure using HCL in `.tf` files.
2. **Initialize**: Run `terraform init` to download the necessary provider plugins and initialize the working directory.
3. **Plan**: Run `terraform plan` to create an execution plan, which shows the changes that will be made to achieve the desired state.
4. **Apply**: Run `terraform apply` to execute the changes required to reach the desired state of the configuration.
5. **Destroy**: Run `terraform destroy` to remove all resources defined in the configuration.

## Key Concepts
- **Providers**: Plugins that interact with APIs of cloud providers or other services to manage resources.
- **Resources**: The components of your infrastructure, such as virtual machines, storage accounts, and networking components.
- **Modules**: Reusable configurations that can be shared and used across different projects.
- **State**: A file that keeps track of the current state of your infrastructure, allowing Terraform to determine what changes need to be applied.

## How to Install Terraform
1. **Download Terraform**: Visit the [Terraform download page](https://www.terraform.io/downloads.html) and download the appropriate package for your operating system.
2. **Install Terraform**:
    - **Windows**: Unzip the downloaded package and place the `terraform.exe` file in a directory included in your system's PATH.
    - **macOS**: Use Homebrew: `brew install terraform`
    - **Linux**: Unzip the downloaded package and move the `terraform` binary to `/usr/local/bin/`.

3. **Verify Installation**: Open a terminal and run `terraform -v` to verify the installation.

## How to Use Terraform
1. **Write Configuration**: Create a `.tf` file with the desired infrastructure configuration.
2. **Initialize**: Run `terraform init` to initialize the working directory.
3. **Plan**: Run `terraform plan` to see the changes that will be made.
4. **Apply**: Run `terraform apply` to apply the changes and provision the infrastructure.
5. **Destroy**: Run `terraform destroy` to tear down the infrastructure.


### Installation
To install Terraform, follow these steps:
1. Download the appropriate package for your operating system from the [Terraform downloads page](https://www.terraform.io/downloads.html).
2. Unzip the package and place the `terraform` binary in a directory included in your system's `PATH`.

### Configuration
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

### Basic Commands
- `terraform init`: Initialize a new or existing Terraform configuration.
- `terraform plan`: Create an execution plan.
- `terraform apply`: Apply the changes required to reach the desired state of the configuration.
- `terraform destroy`: Destroy the Terraform-managed infrastructure.

### Examples
#### Example 1: Creating an AWS EC2 Instance
```hcl
provider "aws" {
    region = "us-west-2"
}

resource "aws_instance" "example" {
    ami           = "ami-0c55b159cbfafe1f0"
    instance_type = "t2.micro"
}
```

#### Example 2: Creating an S3 Bucket
```hcl
provider "aws" {
    region = "us-west-2"
}

resource "aws_s3_bucket" "example" {
    bucket = "my-unique-bucket-name"
    acl    = "private"
}
```
#### Example 3: Creating an Azure Virtual Machine
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

#### Example 4: Creating a Google Cloud Storage Bucket
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


## Learn Terraform on Different Cloud Providers
- **Azure**: [Terraform on Azure](https://learn.hashicorp.com/collections/terraform/azure-get-started)
- **AWS**: [Terraform on AWS](https://learn.hashicorp.com/collections/terraform/aws-get-started)
- **Google Cloud**: [Terraform on Google Cloud](https://learn.hashicorp.com/collections/terraform/gcp-get-started)
- **Oracle Cloud**: [Terraform on Oracle Cloud](https://www.oracle.com/cloud/iaas/terraform-getting-started.html)
