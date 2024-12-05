
# Terraform Resources

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

## Learn Terraform on Different Cloud Providers
- **Azure**: [Terraform on Azure](https://learn.hashicorp.com/collections/terraform/azure-get-started)
- **AWS**: [Terraform on AWS](https://learn.hashicorp.com/collections/terraform/aws-get-started)
- **Google Cloud**: [Terraform on Google Cloud](https://learn.hashicorp.com/collections/terraform/gcp-get-started)
- **Oracle Cloud**: [Terraform on Oracle Cloud](https://www.oracle.com/cloud/iaas/terraform-getting-started.html)
