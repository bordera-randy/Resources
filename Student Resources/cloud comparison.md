# Cloud Services Comparison Cheat Sheet

## ☁️ Core Compute Services

| Capability                   | Microsoft Azure                       | Amazon Web Services         | Google Cloud Platform   |
| ---------------------------- | ------------------------------------- | --------------------------- | ----------------------- |
| Virtual Machines             | Azure Virtual Machines                | EC2 (Elastic Compute Cloud) | Compute Engine          |
| VM Scale Sets / Auto Scaling | Virtual Machine Scale Sets (VMSS)     | Auto Scaling Groups         | Managed Instance Groups |
| Dedicated Hosts              | Azure Dedicated Host                  | EC2 Dedicated Hosts         | Sole-Tenant Nodes       |
| Spot / Preemptible VMs       | Spot VMs                              | EC2 Spot Instances          | Preemptible VMs         |
| Bare Metal                   | Azure BareMetal Infrastructure        | AWS Bare Metal Instances    | Bare Metal Solution     |
| Custom Images                | Managed Images / Shared Image Gallery | AMIs                        | Custom Images           |
| GPU Instances                | GPU-enabled VMs                       | GPU EC2 Instances           | GPU VMs                 |

---

## 📦 Containers & Kubernetes

| Capability             | Azure                          | AWS                      | GCP                            |
| ---------------------- | ------------------------------ | ------------------------ | ------------------------------ |
| Managed Kubernetes     | Azure Kubernetes Service (AKS) | Amazon EKS               | Google Kubernetes Engine (GKE) |
| Serverless Containers  | Azure Container Apps           | AWS App Runner / Fargate | Cloud Run                      |
| Container Registry     | Azure Container Registry (ACR) | Amazon ECR               | Artifact Registry              |
| Managed Docker Hosting | App Service (Containers)       | Elastic Beanstalk        | App Engine (Flex)              |
| Service Mesh           | Open Service Mesh / Istio      | App Mesh                 | Anthos Service Mesh            |

---

## 🗄️ Storage Services

| Capability             | Azure                | AWS                   | GCP                   |
| ---------------------- | -------------------- | --------------------- | --------------------- |
| Object Storage         | Blob Storage         | S3                    | Cloud Storage         |
| File Storage           | Azure Files          | EFS                   | Filestore             |
| Block Storage          | Managed Disks        | EBS                   | Persistent Disk       |
| Archive Storage        | Blob Archive Tier    | S3 Glacier            | Archive Storage       |
| Data Transfer          | Azure Data Box       | Snowball              | Transfer Appliance    |
| Storage Lifecycle Mgmt | Blob Lifecycle Rules | S3 Lifecycle Policies | Object Lifecycle Mgmt |

---

## 🧠 Databases (Managed)

### Relational

| Capability                 | Azure                         | AWS                     | GCP                  |
| -------------------------- | ----------------------------- | ----------------------- | -------------------- |
| Managed SQL (General)      | Azure SQL Database            | RDS                     | Cloud SQL            |
| MySQL                      | Azure Database for MySQL      | RDS MySQL / Aurora      | Cloud SQL MySQL      |
| PostgreSQL                 | Azure Database for PostgreSQL | RDS PostgreSQL / Aurora | Cloud SQL PostgreSQL |
| SQL Server                 | Azure SQL / SQL MI            | RDS SQL Server          | Cloud SQL SQL Server |
| Enterprise Distributed SQL | Azure SQL Hyperscale          | Aurora                  | Spanner              |

### NoSQL

| Capability           | Azure                     | AWS         | GCP         |
| -------------------- | ------------------------- | ----------- | ----------- |
| Key-Value / Document | Cosmos DB                 | DynamoDB    | Firestore   |
| Wide-Column          | Cosmos DB (Cassandra API) | Keyspaces   | Bigtable    |
| Cache (Redis)        | Azure Cache for Redis     | ElastiCache | Memorystore |

---

## 🌐 Networking

| Capability           | Azure                  | AWS                       | GCP                     |
| -------------------- | ---------------------- | ------------------------- | ----------------------- |
| Virtual Network      | Virtual Network (VNet) | VPC                       | VPC                     |
| Subnets              | Subnets                | Subnets                   | Subnets                 |
| Load Balancer (L4)   | Azure Load Balancer    | Network Load Balancer     | TCP/UDP Load Balancer   |
| Application LB (L7)  | Application Gateway    | Application Load Balancer | HTTP(S) Load Balancer   |
| Global Traffic Mgmt  | Traffic Manager        | Route 53                  | Cloud DNS + Global LB   |
| Private Connectivity | Private Endpoint       | PrivateLink               | Private Service Connect |
| NAT Gateway          | NAT Gateway            | NAT Gateway               | Cloud NAT               |
| DDoS Protection      | Azure DDoS Protection  | AWS Shield                | Cloud Armor             |

---

## 🔐 Identity, Security & Governance

| Capability            | Azure                      | AWS                 | GCP                 |
| --------------------- | -------------------------- | ------------------- | ------------------- |
| IAM                   | Entra ID (Azure AD) + RBAC | IAM                 | Cloud IAM           |
| Identity Federation   | Entra ID                   | IAM Identity Center | Workforce Identity  |
| Secrets Mgmt          | Key Vault                  | Secrets Manager     | Secret Manager      |
| HSM                   | Azure Managed HSM          | CloudHSM            | Cloud HSM           |
| Policy Enforcement    | Azure Policy               | AWS Config + SCP    | Organization Policy |
| Compliance Blueprints | Azure Blueprints           | Control Tower       | Assured Workloads   |

---

## ⚙️ DevOps & Automation

| Capability             | Azure                   | AWS                        | GCP                            |
| ---------------------- | ----------------------- | -------------------------- | ------------------------------ |
| CI/CD                  | Azure DevOps            | CodePipeline               | Cloud Build                    |
| Infrastructure as Code | ARM / Bicep / Terraform | CloudFormation / Terraform | Deployment Manager / Terraform |
| Artifact Repo          | Azure Artifacts         | CodeArtifact               | Artifact Registry              |
| Automation             | Azure Automation        | Systems Manager            | Cloud Scheduler                |
| Serverless Functions   | Azure Functions         | Lambda                     | Cloud Functions                |

---

## 📊 Monitoring, Logging & Observability

| Capability     | Azure                   | AWS               | GCP              |
| -------------- | ----------------------- | ----------------- | ---------------- |
| Metrics & Logs | Azure Monitor           | CloudWatch        | Cloud Monitoring |
| Log Analytics  | Log Analytics Workspace | CloudWatch Logs   | Log Explorer     |
| Tracing        | Application Insights    | X-Ray             | Cloud Trace      |
| Alerts         | Azure Alerts            | CloudWatch Alarms | Alerting         |
| Cost Mgmt      | Cost Management         | Cost Explorer     | Billing Reports  |

---

## 📩 Messaging & Integration

| Capability             | Azure                        | AWS            | GCP       |
| ---------------------- | ---------------------------- | -------------- | --------- |
| Message Queue          | Storage Queues / Service Bus | SQS            | Pub/Sub   |
| Pub/Sub                | Event Grid                   | SNS            | Pub/Sub   |
| Event Streaming        | Event Hubs                   | Kinesis        | Pub/Sub   |
| Workflow Orchestration | Logic Apps                   | Step Functions | Workflows |

---

## 🧪 Analytics & Big Data

| Capability       | Azure                  | AWS               | GCP                |
| ---------------- | ---------------------- | ----------------- | ------------------ |
| Data Warehouse   | Synapse Analytics      | Redshift          | BigQuery           |
| ETL / ELT        | Data Factory           | Glue              | Dataflow           |
| Data Lake        | Data Lake Storage Gen2 | Lake Formation    | Cloud Storage      |
| Stream Analytics | Stream Analytics       | Kinesis Analytics | Dataflow Streaming |

---

## 🧠 AI & Machine Learning

| Capability      | Azure                    | AWS                 | GCP                  |
| --------------- | ------------------------ | ------------------- | -------------------- |
| ML Platform     | Azure Machine Learning   | SageMaker           | Vertex AI            |
| Cognitive APIs  | Azure AI Services        | AI Services         | Cloud AI APIs        |
| LLM / GenAI     | Azure OpenAI             | Bedrock             | Gemini               |
| Speech / Vision | Speech Services / Vision | Rekognition / Polly | Vision / Speech APIs |

---

## 🌐 Application Platform / PaaS (Web Apps & APIs)

| Capability             | Microsoft Azure          | Amazon Web Services        | Google Cloud Platform |
| ---------------------- | ------------------------ | -------------------------- | --------------------- |
| Core PaaS Web Hosting  | Azure App Service        | Elastic Beanstalk          | App Engine            |
| Containerized Web Apps | App Service (Containers) | Elastic Beanstalk (Docker) | App Engine Flex       |
| Serverless Web Apps    | Azure Functions          | Lambda + API Gateway       | Cloud Functions       |
| Modern PaaS Containers | Azure Container Apps     | App Runner                 | Cloud Run             |
