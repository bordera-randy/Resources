# 🏗️ Terraform Basics

<p align="right"><sub>Last updated: February 1, 2026</sub></p>

**A practical introduction to Terraform for beginners—Infrastructure as Code fundamentals.**

<p align="center">
  <a href="#intro">Intro</a> •
  <a href="#install">Install</a> •
  <a href="#config">Configuration</a> •
  <a href="#commands">Commands</a> •
  <a href="#examples">Examples</a> •
  <a href="#best-practices">Best Practices</a> •
  <a href="#resources">Resources</a>
</p>

---

## 📖 What is Terraform?
<a id="intro"></a>

Terraform is an open-source **Infrastructure as Code (IaC)** tool created by HashiCorp. It allows you to define and provision cloud infrastructure using declarative configuration files.

**Key Benefits:**
- Define infrastructure in version-controllable code
- Plan changes before applying them
- Manage infrastructure across AWS, Azure, Google Cloud, and more
- Enable team collaboration and reproducibility

---

## ⚙️ Installation
<a id="install"></a>

1. Download the latest version from the [Terraform downloads page](https://www.terraform.io/downloads).
2. Extract the binary and add it to your system `PATH`.
3. Verify installation:

```bash
terraform --version
```

## 📝 Configuration Structure
<a id="config"></a>

### File Organization
Create a working directory and add these standard files:

```
project/
├── main.tf           # Primary configuration
├── variables.tf      # Input variables
├── outputs.tf        # Output values
├── terraform.tfvars  # Variable values
└── .gitignore        # Exclude sensitive files
```

### Basic Example

```hcl
# main.tf
terraform {
  required_version = ">= 1.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = var.aws_region
}

resource "aws_instance" "example" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = var.instance_type

  tags = {
    Name = var.instance_name
  }
}
```

```hcl
# variables.tf
variable "aws_region" {
  description = "AWS region"
  type        = string
  default     = "us-west-2"
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

variable "instance_name" {
  description = "Name of the instance"
  type        = string
}
```

---

## 🎯 Core Commands
<a id="commands"></a>

| Command | Description |
|---------|-------------|
| `terraform init` | Initialize working directory, download providers |
| `terraform plan` | Preview changes without applying them |
| `terraform apply` | Apply configuration changes to cloud |
| `terraform destroy` | Destroy all managed infrastructure |
| `terraform fmt` | Format code to standard style |
| `terraform validate` | Check configuration syntax |
| `terraform import` | Import existing resources into state |
| `terraform state` | Manage Terraform state file |

## 📋 Practical Examples
<a id="examples"></a>

### Example 1: AWS EC2 Instance
```hcl
provider "aws" {
    region = "us-west-2"
}

resource "aws_instance" "example" {
    ami           = "ami-0c55b159cbfafe1f0"
    instance_type = "t2.micro"
}
```

### Example 2: AWS S3 Bucket
```hcl
resource "aws_s3_bucket" "example" {
  bucket = "my-unique-bucket-name"

  tags = {
    Environment = "production"
  }
}

resource "aws_s3_bucket_versioning" "example" {
  bucket = aws_s3_bucket.example.id
  versioning_configuration {
    status = "Enabled"
  }
}

resource "aws_s3_bucket_server_side_encryption_configuration" "example" {
  bucket = aws_s3_bucket.example.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}
```

### Example 3: Azure Virtual Machine
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

### Example 4: Google Cloud Storage Bucket
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

---

## 🎓 Best Practices
<a id="best-practices"></a>

- ✅ **Use version control** — commit all Terraform files to Git
- ✅ **Separate state files** — use remote backends for team collaboration
- ✅ **Plan before apply** — always review `terraform plan` output
- ✅ **Use variables** — avoid hardcoding values; use `variables.tf`
- ✅ **Organize with modules** — break complex configurations into reusable modules
- ✅ **Name resources clearly** — use consistent naming conventions
- ✅ **Add comments** — document complex logic and resource purposes
- ✅ **Enable state locking** — prevent concurrent modifications
- ✅ **Use `terraform.tfvars`** — keep secrets out of version control
- ✅ **Validate early** — run `terraform validate` and `terraform fmt` before committing

---

## 📚 Resources
<a id="resources"></a>

- [Terraform Official Docs](https://www.terraform.io/docs)
- [HashiCorp Learn Tutorials](https://learn.hashicorp.com/terraform)
- [Terraform Registry](https://registry.terraform.io/) — Providers, modules, and resources
- [Terraform GitHub](https://github.com/hashicorp/terraform)
- [Azure Terraform Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
- [AWS Terraform Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Google Cloud Terraform Provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs)

---

<p align="right"><a href="../README.md">Back to Student Resources</a></p>
