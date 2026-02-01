
# 🔧 Terraform Resources & Providers

<p align="right"><sub>Last updated: February 1, 2026</sub></p>

**Curated reference for Terraform providers, modules, and cloud-specific resources.**

<p align="center">
  <a href="#intro">Intro</a> •
  <a href="#how">How It Works</a> •
  <a href="#concepts">Concepts</a> •
  <a href="#providers">Providers</a> •
  <a href="#modules">Modules</a> •
  <a href="#examples">Examples</a> •
  <a href="#learn">Learn More</a> •
  <a href="#best-practices">Best Practices</a>
</p>

---

## 📖 What is Terraform?
<a id="intro"></a>

Terraform is an open-source **Infrastructure as Code (IaC)** tool created by HashiCorp. It enables you to define and provision cloud infrastructure using **HashiCorp Configuration Language (HCL)** or JSON.

**Why Terraform?**
- Version control your infrastructure
- Automated provisioning and scaling
- Multi-cloud support (AWS, Azure, GCP, and 300+ providers)
- Reproducible and predictable deployments

## ⚙️ How Terraform Works
<a id="how"></a>

Terraform follows a simple workflow:

1. **Write** — Define infrastructure in `.tf` files using HCL
2. **Plan** — Preview changes with `terraform plan`
3. **Apply** — Execute changes with `terraform apply`
4. **Monitor** — Track state and make updates as needed
5. **Destroy** — Tear down infrastructure with `terraform destroy`

## 🧩 Key Concepts
<a id="concepts"></a>

| Concept | Description |
|---------|-------------|
| **Providers** | Plugins that connect to cloud provider APIs (AWS, Azure, GCP, etc.) |
| **Resources** | Infrastructure components: VMs, buckets, networks, databases, etc. |
| **Modules** | Reusable, shareable Terraform configurations for common patterns |
| **Variables** | Input values for making configurations dynamic and reusable |
| **Outputs** | Return values from modules and configurations |
| **State** | File tracking infrastructure state for change management |
| **Workspaces** | Isolated environments (dev, staging, prod) from same codebase |

## 📦 Providers & Registries
<a id="providers"></a>

**Official Provider Registries:**
- [Terraform Registry](https://registry.terraform.io/) — 300+ official and community providers
- [AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
- [Google Cloud Provider](https://registry.terraform.io/providers/hashicorp/google/latest/docs)
- [Kubernetes Provider](https://registry.terraform.io/providers/hashicorp/kubernetes/latest/docs)

---

## 🎁 Modules
<a id="modules"></a>

**Using Terraform Registry Modules:**

```hcl
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"
  version = "3.0"
  
  name = "my-vpc"
  cidr = "10.0.0.0/16"
  azs  = ["us-west-2a", "us-west-2b"]
}
```

**Popular Module Collections:**
- [Terraform AWS Modules](https://github.com/terraform-aws-modules)
- [Azure Terraform Modules](https://registry.terraform.io/namespaces/Azure)
- [Google Cloud Modules](https://registry.terraform.io/namespaces/GoogleCloudPlatform)

---

## 💡 Common Examples
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
    
    uniform_bucket_level_access = true
    
    versioning {
        enabled = true
    }
}
```


## Learn More

Expand your Terraform knowledge with these official resources and cloud-specific learning paths:

### HashiCorp Official Learning
- **[Terraform Official Documentation](https://www.terraform.io/docs)** - Complete reference for all Terraform features
- **[HashiCorp Learning Portal](https://learn.hashicorp.com/terraform)** - Structured learning paths and tutorials
- **[Terraform Registry](https://registry.terraform.io/)** - Browse providers, modules, and policy libraries

### Cloud-Specific Learning Paths
- **Azure**: [Terraform on Azure Learning Collection](https://learn.hashicorp.com/collections/terraform/azure-get-started)
- **AWS**: [Terraform on AWS Learning Collection](https://learn.hashicorp.com/collections/terraform/aws-get-started)
- **Google Cloud**: [Terraform on Google Cloud Learning Collection](https://learn.hashicorp.com/collections/terraform/gcp-get-started)
- **Oracle Cloud**: [Terraform on Oracle Cloud Getting Started](https://www.oracle.com/cloud/iaas/terraform-getting-started.html)

### Community & Advanced Topics
- **[Terraform GitHub Repository](https://github.com/hashicorp/terraform)** - Source code and issue tracking
- **[Terraform Community Forum](https://discuss.hashicorp.com/c/terraform)** - Ask questions and share knowledge
- **[Awesome Terraform](https://github.com/shuaibiyy/awesome-terraform)** - Curated list of Terraform tools and resources

---

## 🏆 Best Practices

Follow these Terraform best practices to write maintainable, secure, and efficient infrastructure code:

1. **Use Remote State** - Store state files in remote backends (S3, Azure Storage, Terraform Cloud) for team collaboration and safety
2. **Version Your Code** - Keep Terraform configurations in version control (Git) with meaningful commit messages
3. **Separate Environments** - Use distinct directories or workspaces for dev, staging, and production environments
4. **Use Variables for Configuration** - Never hardcode values; use `variables.tf` for reusable and flexible code
5. **Implement State Locking** - Enable state locking to prevent concurrent modifications that could corrupt state
6. **Document Your Infrastructure** - Add comments explaining the purpose and behavior of resources and variables
7. **Use Modules for Reusability** - Organize code into modules for consistency across multiple projects
8. **Validate Before Applying** - Always run `terraform plan` and `terraform validate` before `terraform apply`
9. **Manage Secrets Carefully** - Use tools like HashiCorp Vault, AWS Secrets Manager, or environment variables for sensitive data
10. **Implement Code Review** - Require peer review of Terraform changes before merging to production
11. **Use Descriptive Naming** - Name resources clearly to identify their purpose and relationships
12. **Tag Your Resources** - Add metadata tags to resources for cost tracking, organization, and automation

---

<p align="right"><a href="../README.md">Back to Student Resources</a></p>
