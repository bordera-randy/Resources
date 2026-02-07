# 🛠️ Admin Tools Reference Guide
<a id="admin-tools-reference-guide"></a>

<p align="right"><sub>Last updated: February 7, 2026</sub></p>

This document is a **practical reference for IT administrators, cloud engineers, and sysadmins**.  
It groups commonly used **administrative, diagnostic, security, and operations tools**, with detailed explanations, use cases, and direct links to each tool.

**Quick Links:**
[General Admin](#general-admin-utilities) •
[Networking](#networking--dns-tools) •
[Email](#email--messaging-diagnostics) •
[Security](#security--identity-tools) •
[Cloud](#cloud--infrastructure-tools) •
[Monitoring](#monitoring--troubleshooting) •
[Open Source](#open-source-tools) •
[SaaS Tools](#third-party--saas-tools)

---

## 📋 Table of Contents

- [🛠️ Admin Tools Reference Guide](#️-admin-tools-reference-guide)
  - [📋 Table of Contents](#-table-of-contents)
  - [🧭 Overview](#-overview)
  - [⚙️ General Admin Utilities](#️-general-admin-utilities)
    - [Ping / Traceroute](#ping--traceroute)
    - [WHOIS](#whois)
    - [Telnet / Netcat (nc)](#telnet--netcat-nc)
    - [SSH (Secure Shell)](#ssh-secure-shell)
    - [PowerShell](#powershell)
    - [Bash / Zsh](#bash--zsh)
  - [🌐 Networking \& DNS Tools](#-networking--dns-tools)
    - [DNS Lookup (nslookup / dig)](#dns-lookup-nslookup--dig)
    - [IP Reputation Checkers](#ip-reputation-checkers)
    - [Network Scanners (nmap)](#network-scanners-nmap)
    - [IPConfig / ifconfig](#ipconfig--ifconfig)
    - [Route](#route)
    - [ARP](#arp)
    - [Netstat](#netstat)
  - [📧 Email \& Messaging Diagnostics](#-email--messaging-diagnostics)
    - [MX Records](#mx-records)
    - [SPF / DKIM / DMARC](#spf--dkim--dmarc)
    - [Email Header Analyzers](#email-header-analyzers)
    - [SMTP Test Tools](#smtp-test-tools)
  - [🔒 Security \& Identity Tools](#-security--identity-tools)
    - [Password \& Hash Utilities](#password--hash-utilities)
    - [Certificate Inspectors](#certificate-inspectors)
    - [Vulnerability Scanners](#vulnerability-scanners)
    - [SIEM \& Log Analysis](#siem--log-analysis)
    - [Multi-Factor Authentication (MFA)](#multi-factor-authentication-mfa)
    - [Identity Providers](#identity-providers)
  - [☁️ Cloud \& Infrastructure Tools](#️-cloud--infrastructure-tools)
    - [Cloud Provider Portals](#cloud-provider-portals)
    - [Infrastructure as Code (IaC)](#infrastructure-as-code-iac)
    - [Container Tools](#container-tools)
    - [Kubernetes Management](#kubernetes-management)
    - [CI/CD Platforms](#cicd-platforms)
  - [📊 Monitoring \& Troubleshooting](#-monitoring--troubleshooting)
    - [Log Search \& Analysis](#log-search--analysis)
    - [Status Pages](#status-pages)
    - [Application Performance Monitoring (APM)](#application-performance-monitoring-apm)
    - [Network Monitoring](#network-monitoring)
    - [Uptime Monitoring](#uptime-monitoring)
  - [🔓 Open Source Tools](#-open-source-tools)
    - [OpenSSL](#openssl)
    - [Wireshark](#wireshark)
    - [curl](#curl)
    - [wget](#wget)
    - [Git](#git)
    - [Ansible](#ansible)
    - [Nagios](#nagios)
  - [🌟 Third‑Party / SaaS Tools](#third-party--saas-tools)
    - [Qvert Utilities](#qvert-utilities)
    - [MXToolbox](#mxtoolbox)
    - [Cloudflare Tools](#cloudflare-tools)
    - [Postman](#postman)
    - [Pingdom](#pingdom)
  - [🏢 Vendor \& Platform Portals](#-vendor--platform-portals)
    - [Ticketing Systems (Jira / Service Desk)](#ticketing-systems-jira--service-desk)
    - [MSP \& Partner Portals](#msp--partner-portals)
    - [Licensing Portals](#licensing-portals)
  - [📚 How to Use This Document](#-how-to-use-this-document)

---

## 🧭 Overview
<a id="overview"></a>

This reference guide provides **practical, operational information** for the tools most commonly used in IT administration, cloud operations, and security engineering.

**What you'll find here:**
- ✅ Tool names with direct links
- ✅ Clear use cases for each tool
- ✅ Practical troubleshooting scenarios
- ✅ Platform-specific commands and examples

**Intended audience:**
- IT Administrators
- Cloud Engineers
- DevOps Engineers
- Security Operations Teams
- Systems Architects

---

## ⚙️ General Admin Utilities
<a id="general-admin-utilities"></a>

### Ping / Traceroute

**Links:**
- Windows: Built-in (`ping`, `tracert`)
- Linux/macOS: Built-in (`ping`, `traceroute`)
- [Online Ping Tool](https://ping.eu/)

**Purpose:**  
Basic network reachability and latency testing.

**Use cases:**
- ✅ Verify a host is reachable
- ✅ Identify routing or latency issues
- ✅ Quick sanity checks during incidents
- ✅ Measure round-trip time (RTT) to endpoints

**Common commands:**
```bash
# Ping a host
ping google.com

# Traceroute to destination
traceroute google.com  # Linux/macOS
tracert google.com     # Windows

# Limit ping count
ping -c 4 google.com   # Linux/macOS
ping -n 4 google.com   # Windows
```

---

### WHOIS

**Links:**
- [WHOIS Lookup (ICANN)](https://lookup.icann.org/)
- [WHOIS.com](https://www.whois.com/)
- [DomainTools WHOIS](https://whois.domaintools.com/)

**Purpose:**  
Query domain registration and ownership information.

**Use cases:**
- ✅ Identify domain owners
- ✅ Investigate suspicious domains
- ✅ Validate DNS registration details
- ✅ Check domain expiration dates
- ✅ Find registrar and nameserver information

**Common commands:**
```bash
# WHOIS lookup from command line
whois example.com

# Get detailed registration info
whois -h whois.verisign-grs.com example.com
```

---

### Telnet / Netcat (nc)

**Links:**
- Windows: Built-in (Telnet must be enabled as Windows feature)
- Linux/macOS: Built-in
- [Netcat Documentation](http://netcat.sourceforge.net/)
- [Ncat (Nmap Project)](https://nmap.org/ncat/)

**Purpose:**  
Test TCP connectivity and troubleshoot network services.

**Use cases:**
- ✅ Test port connectivity
- ✅ Verify service availability
- ✅ Debug SMTP, HTTP, POP3 connections
- ✅ Banner grabbing for service identification

**Common commands:**
```bash
# Test port connectivity
telnet mail.example.com 25
nc -zv mail.example.com 25

# Test HTTPS connection
openssl s_client -connect example.com:443

# Listen on a port
nc -l 8080
```

---

### SSH (Secure Shell)

**Links:**
- [OpenSSH](https://www.openssh.com/)
- [PuTTY (Windows)](https://www.putty.org/)
- [MobaXterm (Windows)](https://mobaxterm.mobatek.net/)

**Purpose:**  
Secure remote access and administration.

**Use cases:**
- ✅ Remote server management
- ✅ Secure file transfer (SCP, SFTP)
- ✅ Port forwarding and tunneling
- ✅ Key-based authentication

**Common commands:**
```bash
# SSH to remote host
ssh user@hostname

# SSH with specific key
ssh -i ~/.ssh/id_rsa user@hostname

# Copy files with SCP
scp file.txt user@hostname:/path/

# Port forwarding
ssh -L 8080:localhost:80 user@hostname
```

---

### PowerShell

**Links:**
- [PowerShell Documentation](https://docs.microsoft.com/en-us/powershell/)
- [PowerShell Gallery](https://www.powershellgallery.com/)
- [PowerShell GitHub](https://github.com/PowerShell/PowerShell)

**Purpose:**  
Windows automation and administration framework.

**Use cases:**
- ✅ Windows system administration
- ✅ Azure and Microsoft 365 management
- ✅ Automation scripting
- ✅ Active Directory management

**Common commands:**
```powershell
# Get system info
Get-ComputerInfo

# List services
Get-Service

# Azure login
Connect-AzAccount

# Microsoft 365 management
Connect-MgGraph
```

---

### Bash / Zsh

**Links:**
- [Bash Manual](https://www.gnu.org/software/bash/manual/)
- [Zsh Documentation](https://zsh.sourceforge.io/Doc/)
- [Oh My Zsh](https://ohmyz.sh/)

**Purpose:**  
Unix/Linux shell scripting and administration.

**Use cases:**
- ✅ Linux/macOS system administration
- ✅ Automation and scripting
- ✅ Text processing and data manipulation
- ✅ Pipeline operations

**Common commands:**
```bash
# System monitoring
top
htop
df -h

# Process management
ps aux | grep nginx
kill -9 <PID>

# File operations
find / -name "*.log"
grep -r "error" /var/log/
```

---

## 🌐 Networking & DNS Tools
<a id="networking--dns-tools"></a>

### DNS Lookup (nslookup / dig)

**Links:**
- Windows: Built-in (`nslookup`)
- Linux/macOS: Built-in (`dig`, `nslookup`)
- [DNS Lookup Online](https://www.nslookup.io/)
- [DNSChecker](https://dnschecker.org/)
- [Google DNS Lookup](https://dns.google/)

**Purpose:**  
Query DNS records directly from authoritative or recursive servers.

**Use cases:**
- ✅ Validate A, CNAME, MX, TXT, SPF, DKIM records
- ✅ Troubleshoot DNS propagation issues
- ✅ Confirm changes before production cutover
- ✅ Identify authoritative nameservers
- ✅ Debug DNS resolution problems

**Common commands:**
```bash
# Basic DNS lookup
nslookup example.com

# Query specific record type
dig example.com MX
dig example.com TXT

# Query specific DNS server
dig @8.8.8.8 example.com

# Trace DNS resolution path
dig +trace example.com

# Get all DNS records
dig example.com ANY
```

---

### IP Reputation Checkers

**Links:**
- [MXToolbox Blacklist Check](https://mxtoolbox.com/blacklists.aspx)
- [Talos Intelligence](https://talosintelligence.com/reputation_center)
- [AbuseIPDB](https://www.abuseipdb.com/)
- [IPVoid](https://www.ipvoid.com/)
- [Spamhaus](https://www.spamhaus.org/lookup/)

**Purpose:**  
Determine whether an IP address is listed on blacklists.

**Use cases:**
- ✅ Email delivery troubleshooting
- ✅ Incident response
- ✅ Security investigations
- ✅ Validate IP reputation before deployment
- ✅ Monitor for compromised systems

---

### Network Scanners (nmap)

**Links:**
- [Nmap Official Site](https://nmap.org/)
- [Nmap Documentation](https://nmap.org/book/man.html)
- [Zenmap (GUI)](https://nmap.org/zenmap/)

**Purpose:**  
Network discovery and security auditing.

**Use cases:**
- ✅ Port scanning and service detection
- ✅ Network inventory
- ✅ Security assessments
- ✅ Vulnerability discovery

**Common commands:**
```bash
# Basic port scan
nmap example.com

# Scan specific ports
nmap -p 22,80,443 example.com

# Service version detection
nmap -sV example.com

# OS detection
nmap -O example.com

# Scan entire subnet
nmap 192.168.1.0/24
```

---

### IPConfig / ifconfig

**Links:**
- Windows: Built-in (`ipconfig`)
- Linux/macOS: Built-in (`ifconfig`, `ip`)
- [IP Command Cheat Sheet](https://access.redhat.com/sites/default/files/attachments/rh_ip_command_cheatsheet_1214_jcs_print.pdf)

**Purpose:**  
Display and configure network interface parameters.

**Use cases:**
- ✅ View IP address configuration
- ✅ Troubleshoot network connectivity
- ✅ Renew DHCP leases
- ✅ Display MAC addresses

**Common commands:**
```bash
# Windows
ipconfig /all
ipconfig /release
ipconfig /renew
ipconfig /flushdns

# Linux/macOS
ifconfig
ip addr show
ip link show
```

---

### Route

**Links:**
- Windows: Built-in (`route`)
- Linux/macOS: Built-in (`route`, `ip route`)

**Purpose:**  
View and manipulate the IP routing table.

**Use cases:**
- ✅ Troubleshoot routing issues
- ✅ Add static routes
- ✅ Identify default gateway
- ✅ Debug network path problems

**Common commands:**
```bash
# Windows
route print
route add 10.0.0.0 mask 255.0.0.0 192.168.1.1

# Linux/macOS
route -n
ip route show
ip route add 10.0.0.0/8 via 192.168.1.1
```

---

### ARP

**Links:**
- Windows/Linux/macOS: Built-in (`arp`)

**Purpose:**  
Display and modify the Address Resolution Protocol (ARP) cache.

**Use cases:**
- ✅ Troubleshoot local network connectivity
- ✅ Identify MAC addresses
- ✅ Detect ARP spoofing
- ✅ Clear stale ARP entries

**Common commands:**
```bash
# Display ARP cache
arp -a

# Clear ARP cache
arp -d *  # Windows
sudo ip -s -s neigh flush all  # Linux
```

---

### Netstat

**Links:**
- Windows/Linux/macOS: Built-in (`netstat`, `ss`)

**Purpose:**  
Display network connections, routing tables, and interface statistics.

**Use cases:**
- ✅ View active connections
- ✅ Identify listening ports
- ✅ Troubleshoot port conflicts
- ✅ Monitor network usage

**Common commands:**
```bash
# Show all connections
netstat -a

# Show listening ports
netstat -an | grep LISTEN

# Show process using ports (Windows)
netstat -ano

# Modern alternative (Linux)
ss -tulpn
```

---

## 📧 Email & Messaging Diagnostics
<a id="email--messaging-diagnostics"></a>

### MX Records

**Links:**
- [MXToolbox MX Lookup](https://mxtoolbox.com/MXLookup.aspx)
- [DNS Checker MX](https://dnschecker.org/mx-lookup.php)
- [Google Admin Toolbox](https://toolbox.googleapps.com/apps/checkmx/)

**Purpose:**  
Define mail routing for a domain.

**Use cases:**
- ✅ Verify email delivery paths
- ✅ Confirm mail provider configuration
- ✅ Troubleshoot inbound email failures
- ✅ Validate MX priority settings
- ✅ Check mail server DNS resolution

**Common commands:**
```bash
# Query MX records
dig example.com MX
nslookup -type=MX example.com

# Test SMTP connection to MX
telnet mail.example.com 25
```

---

### SPF / DKIM / DMARC

**Links:**
- [MXToolbox SPF Check](https://mxtoolbox.com/spf.aspx)
- [DMARC Analyzer](https://www.dmarcanalyzer.com/)
- [Google DMARC Tool](https://toolbox.googleapps.com/apps/checkmx/)
- [SPF Record Checker](https://www.kitterman.com/spf/validate.html)
- [DKIM Validator](https://dkimvalidator.com/)

**Purpose:**  
Email authentication and anti‑spoofing controls.

**Use cases:**
- ✅ Prevent domain spoofing
- ✅ Improve email deliverability
- ✅ Meet security and compliance requirements
- ✅ Monitor unauthorized use of domain
- ✅ Configure email authentication policies

**Record examples:**
```dns
; SPF Record
example.com. IN TXT "v=spf1 include:_spf.google.com ~all"

; DKIM Record
default._domainkey.example.com. IN TXT "v=DKIM1; k=rsa; p=MIGfMA0..."

; DMARC Record
_dmarc.example.com. IN TXT "v=DMARC1; p=quarantine; rua=mailto:dmarc@example.com"
```

---

### Email Header Analyzers

**Links:**
- [MXToolbox Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx)
- [Google Message Header Analyzer](https://toolbox.googleapps.com/apps/messageheader/)
- [Microsoft Message Header Analyzer](https://mha.azurewebsites.net/)
- [Mail Header Analyzer](https://mailheader.org/)

**Purpose:**  
Parse and analyze email headers for delivery troubleshooting.

**Use cases:**
- ✅ Trace email delivery path
- ✅ Identify spam filtering issues
- ✅ Verify authentication (SPF/DKIM/DMARC)
- ✅ Troubleshoot delayed or bounced emails
- ✅ Investigate suspicious emails

---

### SMTP Test Tools

**Links:**
- [MXToolbox SMTP Test](https://mxtoolbox.com/diagnostic.aspx)
- [WormlyFree SMTP Test](https://www.wormly.com/test-smtp-server)
- [Email on Acid SMTP Test](https://www.emailonacid.com/)

**Purpose:**  
Test SMTP server configuration and connectivity.

**Use cases:**
- ✅ Verify SMTP server settings
- ✅ Test email relay configuration
- ✅ Validate TLS/SSL settings
- ✅ Troubleshoot authentication issues
- ✅ Check open relay status

**Common commands:**
```bash
# Test SMTP connection
telnet mail.example.com 25

# Test with OpenSSL (TLS)
openssl s_client -connect mail.example.com:587 -starttls smtp

# Send test email via telnet
EHLO example.com
MAIL FROM: test@example.com
RCPT TO: recipient@example.com
DATA
Subject: Test
Test message
.
QUIT
```

---

## 🔒 Security & Identity Tools
<a id="security--identity-tools"></a>

### Password & Hash Utilities

**Links:**
- [Bcrypt Generator](https://bcrypt-generator.com/)
- [MD5 Hash Generator](https://www.md5hashgenerator.com/)
- [SHA Hash Generator](https://passwordsgenerator.net/sha256-hash-generator/)
- [John the Ripper](https://www.openwall.com/john/)
- [Hashcat](https://hashcat.net/hashcat/)

**Purpose:**  
Generate, validate, or inspect password hashes.

**Use cases:**
- ✅ Secure credential handling
- ✅ Migration or validation tasks
- ✅ Security testing
- ✅ Password strength verification
- ✅ Hash cracking for security audits

**Common commands:**
```bash
# Generate bcrypt hash
htpasswd -bnBC 10 "" password123

# Generate SHA-256 hash
echo -n "password" | shasum -a 256

# OpenSSL password generation
openssl rand -base64 32
```

---

### Certificate Inspectors

**Links:**
- [SSL Labs SSL Test](https://www.ssllabs.com/ssltest/)
- [SSL Checker](https://www.sslshopper.com/ssl-checker.html)
- [DigiCert Certificate Inspector](https://www.digicert.com/help/)
- [Certificate Decoder](https://www.sslshopper.com/certificate-decoder.html)

**Purpose:**  
Inspect SSL/TLS certificates for validity and configuration.

**Use cases:**
- ✅ Detect expired certificates
- ✅ Validate trust chains
- ✅ Troubleshoot HTTPS issues
- ✅ Check certificate Subject Alternative Names (SAN)
- ✅ Verify cipher suite configuration

**Common commands:**
```bash
# Check certificate details
openssl s_client -connect example.com:443 -showcerts

# View certificate file
openssl x509 -in cert.pem -text -noout

# Check certificate expiration
openssl s_client -connect example.com:443 | openssl x509 -noout -dates

# Verify certificate chain
openssl verify -CAfile ca-bundle.crt certificate.crt
```

---

### Vulnerability Scanners

**Links:**
- [Nessus](https://www.tenable.com/products/nessus)
- [OpenVAS](https://www.openvas.org/)
- [Qualys](https://www.qualys.com/)
- [Rapid7 Nexpose](https://www.rapid7.com/products/nexpose/)
- [Acunetix](https://www.acunetix.com/)

**Purpose:**  
Identify security vulnerabilities in systems and applications.

**Use cases:**
- ✅ Security assessments
- ✅ Compliance scanning
- ✅ Vulnerability management
- ✅ Penetration testing
- ✅ Patch management validation

---

### SIEM & Log Analysis

**Links:**
- [Splunk](https://www.splunk.com/)
- [Elastic Stack (ELK)](https://www.elastic.co/elastic-stack/)
- [Microsoft Sentinel](https://azure.microsoft.com/en-us/services/microsoft-sentinel/)
- [Sumo Logic](https://www.sumologic.com/)
- [Graylog](https://www.graylog.org/)

**Purpose:**  
Centralized security information and event management.

**Use cases:**
- ✅ Security monitoring and alerting
- ✅ Threat detection
- ✅ Compliance reporting
- ✅ Incident investigation
- ✅ Log aggregation and analysis

---

### Multi-Factor Authentication (MFA)

**Links:**
- [Microsoft Authenticator](https://www.microsoft.com/en-us/security/mobile-authenticator-app)
- [Google Authenticator](https://support.google.com/accounts/answer/1066447)
- [Authy](https://authy.com/)
- [Duo Security](https://duo.com/)
- [YubiKey](https://www.yubico.com/)

**Purpose:**  
Add additional authentication factors beyond passwords.

**Use cases:**
- ✅ Secure user authentication
- ✅ Compliance requirements
- ✅ Reduce credential-based attacks
- ✅ Protect privileged accounts
- ✅ Zero Trust implementations

---

### Identity Providers

**Links:**
- [Azure Active Directory (Entra ID)](https://azure.microsoft.com/en-us/services/active-directory/)
- [Okta](https://www.okta.com/)
- [Auth0](https://auth0.com/)
- [Ping Identity](https://www.pingidentity.com/)
- [OneLogin](https://www.onelogin.com/)

**Purpose:**  
Centralized identity and access management.

**Use cases:**
- ✅ Single Sign-On (SSO)
- ✅ User provisioning and deprovisioning
- ✅ Access control policies
- ✅ Federation with external partners
- ✅ Identity governance

---

## ☁️ Cloud & Infrastructure Tools
<a id="cloud--infrastructure-tools"></a>

### Cloud Provider Portals

**Links:**
- [Azure Portal](https://portal.azure.com/)
- [AWS Management Console](https://aws.amazon.com/console/)
- [Google Cloud Console](https://console.cloud.google.com/)
- [Oracle Cloud Console](https://cloud.oracle.com/)
- [IBM Cloud Console](https://cloud.ibm.com/)

**Purpose:**  
Management consoles for infrastructure and identity.

**Use cases:**
- ✅ Resource provisioning
- ✅ Monitoring and diagnostics
- ✅ Identity and access management
- ✅ Billing and cost management
- ✅ Security configuration

**Common tasks:**
- Create virtual machines and networks
- Configure storage and databases
- Set up monitoring and alerts
- Manage user permissions
- Review cost analytics

---

### Infrastructure as Code (IaC)

**Links:**
- [Terraform](https://www.terraform.io/)
- [Azure Resource Manager (ARM)](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
- [Azure Bicep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/)
- [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
- [Pulumi](https://www.pulumi.com/)
- [CDK (Cloud Development Kit)](https://aws.amazon.com/cdk/)

**Purpose:**  
Define and deploy infrastructure using code.

**Use cases:**
- ✅ Repeatable deployments
- ✅ Compliance enforcement
- ✅ Environment standardization
- ✅ Version control for infrastructure
- ✅ Automated disaster recovery

**Example Terraform:**
```hcl
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "East US"
}

resource "azurerm_virtual_network" "example" {
  name                = "example-network"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
}
```

---

### Container Tools

**Links:**
- [Docker](https://www.docker.com/)
- [Podman](https://podman.io/)
- [containerd](https://containerd.io/)
- [Docker Hub](https://hub.docker.com/)
- [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/)
- [Amazon ECR](https://aws.amazon.com/ecr/)

**Purpose:**  
Container runtime and image management.

**Use cases:**
- ✅ Application containerization
- ✅ Development environment consistency
- ✅ Microservices deployment
- ✅ CI/CD pipelines
- ✅ Image registry management

**Common commands:**
```bash
# Build image
docker build -t myapp:latest .

# Run container
docker run -d -p 8080:80 myapp:latest

# List containers
docker ps

# View logs
docker logs container_id

# Push to registry
docker push myregistry.azurecr.io/myapp:latest
```

---

### Kubernetes Management

**Links:**
- [Kubernetes](https://kubernetes.io/)
- [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/services/kubernetes-service/)
- [Amazon EKS](https://aws.amazon.com/eks/)
- [Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine)
- [kubectl Documentation](https://kubernetes.io/docs/reference/kubectl/)
- [Helm](https://helm.sh/)
- [K9s](https://k9scli.io/)

**Purpose:**  
Container orchestration and management.

**Use cases:**
- ✅ Orchestrate containerized applications
- ✅ Auto-scaling and load balancing
- ✅ Service discovery and networking
- ✅ Rolling updates and rollbacks
- ✅ Resource management

**Common commands:**
```bash
# Get cluster info
kubectl cluster-info

# List pods
kubectl get pods -A

# Deploy application
kubectl apply -f deployment.yaml

# Scale deployment
kubectl scale deployment myapp --replicas=3

# View logs
kubectl logs pod-name

# Install with Helm
helm install myapp ./chart
```

---

### CI/CD Platforms

**Links:**
- [Azure DevOps](https://azure.microsoft.com/en-us/services/devops/)
- [GitHub Actions](https://github.com/features/actions)
- [GitLab CI/CD](https://docs.gitlab.com/ee/ci/)
- [Jenkins](https://www.jenkins.io/)
- [CircleCI](https://circleci.com/)
- [Travis CI](https://travis-ci.org/)

**Purpose:**  
Continuous integration and continuous deployment automation.

**Use cases:**
- ✅ Automated build and test
- ✅ Deployment pipelines
- ✅ Code quality checks
- ✅ Release management
- ✅ Infrastructure provisioning

---

## 📊 Monitoring & Troubleshooting
<a id="monitoring--troubleshooting"></a>

### Log Search & Analysis

**Links:**
- [Azure Monitor Logs](https://docs.microsoft.com/en-us/azure/azure-monitor/logs/log-query-overview)
- [AWS CloudWatch](https://aws.amazon.com/cloudwatch/)
- [Google Cloud Logging](https://cloud.google.com/logging)
- [Splunk](https://www.splunk.com/)
- [Datadog](https://www.datadoghq.com/)
- [New Relic](https://newrelic.com/)

**Purpose:**  
Search and analyze application and infrastructure logs.

**Use cases:**
- ✅ Incident response
- ✅ Root cause analysis
- ✅ Performance tuning
- ✅ Security investigations
- ✅ Compliance auditing

**Example queries:**
```kusto
# Azure Monitor KQL
AzureActivity
| where TimeGenerated > ago(1h)
| where Level == "Error"
| summarize count() by ResourceGroup

# Splunk SPL
index=main sourcetype=access_combined status>=500
| stats count by status, host
```

---

### Status Pages

**Links:**
- [Azure Status](https://status.azure.com/)
- [AWS Service Health Dashboard](https://status.aws.amazon.com/)
- [Google Cloud Status](https://status.cloud.google.com/)
- [Microsoft 365 Status](https://status.office365.com/)
- [GitHub Status](https://www.githubstatus.com/)
- [Cloudflare Status](https://www.cloudflarestatus.com/)

**Purpose:**  
Check real‑time service health from vendors.

**Use cases:**
- ✅ Confirm upstream outages
- ✅ Reduce mean time to resolution (MTTR)
- ✅ Communicate incident scope
- ✅ Plan maintenance windows
- ✅ Subscribe to service alerts

---

### Application Performance Monitoring (APM)

**Links:**
- [Azure Application Insights](https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview)
- [New Relic APM](https://newrelic.com/products/application-monitoring)
- [Datadog APM](https://www.datadoghq.com/product/apm/)
- [AppDynamics](https://www.appdynamics.com/)
- [Dynatrace](https://www.dynatrace.com/)

**Purpose:**  
Monitor application performance and user experience.

**Use cases:**
- ✅ Track response times and throughput
- ✅ Identify performance bottlenecks
- ✅ Monitor error rates
- ✅ Distributed tracing
- ✅ User experience analytics

---

### Network Monitoring

**Links:**
- [Azure Network Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/)
- [PRTG Network Monitor](https://www.paessler.com/prtg)
- [SolarWinds Network Performance Monitor](https://www.solarwinds.com/network-performance-monitor)
- [Zabbix](https://www.zabbix.com/)
- [Nagios](https://www.nagios.org/)

**Purpose:**  
Monitor network infrastructure and connectivity.

**Use cases:**
- ✅ Bandwidth monitoring
- ✅ Network topology mapping
- ✅ Packet capture and analysis
- ✅ Flow monitoring
- ✅ Alerting on network issues

---

### Uptime Monitoring

**Links:**
- [Pingdom](https://www.pingdom.com/)
- [UptimeRobot](https://uptimerobot.com/)
- [StatusCake](https://www.statuscake.com/)
- [Site24x7](https://www.site24x7.com/)
- [Better Uptime](https://betteruptime.com/)

**Purpose:**  
Continuously monitor availability and performance.

**Use cases:**
- ✅ SLA validation
- ✅ Real-time alerting
- ✅ Proactive issue detection
- ✅ Geographic performance testing
- ✅ Public status pages

---

## 🔓 Open Source Tools
<a id="open-source-tools"></a>

### OpenSSL

**Links:**
- [OpenSSL Official Site](https://www.openssl.org/)
- [OpenSSL Documentation](https://www.openssl.org/docs/)
- [OpenSSL Cookbook](https://www.feistyduck.com/books/openssl-cookbook/)

**Purpose:**  
Toolkit for TLS, certificates, and cryptography.

**Use cases:**
- ✅ Certificate inspection and generation
- ✅ Key generation and management
- ✅ Secure communications testing
- ✅ File encryption/decryption
- ✅ Hash generation

**Common commands:**
```bash
# Generate private key
openssl genrsa -out private.key 2048

# Generate CSR
openssl req -new -key private.key -out request.csr

# Check certificate
openssl x509 -in cert.pem -text -noout

# Test TLS connection
openssl s_client -connect example.com:443

# Encrypt file
openssl enc -aes-256-cbc -salt -in file.txt -out file.enc
```

---

### Wireshark

**Links:**
- [Wireshark Official Site](https://www.wireshark.org/)
- [Wireshark User Guide](https://www.wireshark.org/docs/wsug_html_chunked/)
- [Wireshark Download](https://www.wireshark.org/download.html)

**Purpose:**  
Packet capture and protocol analysis.

**Use cases:**
- ✅ Deep network troubleshooting
- ✅ Security investigations
- ✅ Protocol validation
- ✅ Performance analysis
- ✅ Malware analysis

**Common filters:**
```
# HTTP traffic
http

# Specific IP
ip.addr == 192.168.1.1

# TCP handshake issues
tcp.flags.syn == 1 and tcp.flags.ack == 0

# DNS queries
dns

# TLS handshake
ssl.handshake
```

---

### curl

**Links:**
- [curl Official Site](https://curl.se/)
- [curl Documentation](https://curl.se/docs/)
- [Everything curl Book](https://everything.curl.dev/)

**Purpose:**  
Command‑line HTTP client and data transfer tool.

**Use cases:**
- ✅ API testing
- ✅ Connectivity validation
- ✅ Automation scripting
- ✅ Download files
- ✅ Test HTTP methods

**Common commands:**
```bash
# Basic GET request
curl https://api.example.com/data

# POST with JSON
curl -X POST -H "Content-Type: application/json" \
  -d '{"key":"value"}' https://api.example.com/endpoint

# Include headers in output
curl -i https://example.com

# Follow redirects
curl -L https://example.com

# Authentication
curl -u username:password https://api.example.com

# Download file
curl -O https://example.com/file.zip
```

---

### wget

**Links:**
- [GNU Wget](https://www.gnu.org/software/wget/)
- [Wget Manual](https://www.gnu.org/software/wget/manual/wget.html)

**Purpose:**  
Non-interactive network downloader.

**Use cases:**
- ✅ Download files and websites
- ✅ Recursive downloads
- ✅ Mirror websites
- ✅ Background downloads
- ✅ Resume interrupted downloads

**Common commands:**
```bash
# Download file
wget https://example.com/file.zip

# Recursive download
wget -r https://example.com/

# Mirror website
wget -m https://example.com/

# Download in background
wget -b https://example.com/largefile.iso

# Resume download
wget -c https://example.com/file.zip
```

---

### Git

**Links:**
- [Git Official Site](https://git-scm.com/)
- [Git Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/en/v2)
- [GitHub](https://github.com/)
- [GitLab](https://gitlab.com/)

**Purpose:**  
Distributed version control system.

**Use cases:**
- ✅ Source code management
- ✅ Collaboration and branching
- ✅ Version history tracking
- ✅ Code review workflows
- ✅ Infrastructure as Code versioning

**Common commands:**
```bash
# Clone repository
git clone https://github.com/user/repo.git

# Create branch
git checkout -b feature-branch

# Commit changes
git add .
git commit -m "Add new feature"

# Push changes
git push origin feature-branch

# Pull updates
git pull origin main
```

---

### Ansible

**Links:**
- [Ansible Official Site](https://www.ansible.com/)
- [Ansible Documentation](https://docs.ansible.com/)
- [Ansible Galaxy](https://galaxy.ansible.com/)

**Purpose:**  
IT automation and configuration management.

**Use cases:**
- ✅ Configuration management
- ✅ Application deployment
- ✅ Orchestration
- ✅ Provisioning
- ✅ Compliance automation

**Example playbook:**
```yaml
---
- name: Configure web servers
  hosts: webservers
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
    
    - name: Start nginx service
      service:
        name: nginx
        state: started
        enabled: yes
```

---

### Nagios

**Links:**
- [Nagios Official Site](https://www.nagios.org/)
- [Nagios Core](https://www.nagios.org/projects/nagios-core/)
- [Nagios Documentation](https://www.nagios.org/documentation/)

**Purpose:**  
Infrastructure monitoring and alerting.

**Use cases:**
- ✅ Server monitoring
- ✅ Network device monitoring
- ✅ Service availability checks
- ✅ Performance metrics
- ✅ Alert notification

---

## 🌟 Third‑Party / SaaS Tools
<a id="third-party--saas-tools"></a>

### Qvert Utilities
<a id="qvert-utilities"></a>

**Links:**
- [Qvert Utilities](https://qvert.net/)

**Purpose:**  
Collection of lightweight web tools for QR codes, encoders/decoders, and data formatting.

**Use cases:**
- ✅ Generate QR codes for WiFi, links, reviews, and calls
- ✅ Convert CSV to JSON, prettify/minify JSON
- ✅ Encode/decode URLs, Base64, Base32, Base62
- ✅ Extract URL parameters and test regex patterns
- ✅ Create UUIDs, hashes, and timestamps for testing

**Highlights:**
- QR Code Generator, WiFi QR Generator, Batch Generator
- JSON Prettifier/Minifier, JSON Schema Validator
- URL Encoder/Decoder, URL Parameter Extractor
- CSV to JSON Converter, Markdown to HTML
- Base64 Image Encode/Decode, SHA‑256 Hasher
- UUID Generator, Regex Tester, Timestamp Converter

---

### MXToolbox

**Links:**
- [MXToolbox](https://mxtoolbox.com/)
- [MXToolbox SuperTool](https://mxtoolbox.com/SuperTool.aspx)
- [MXToolbox Monitoring](https://mxtoolbox.com/products/monitoring)

**Purpose:**  
All‑in‑one DNS, MX, blacklist, and email diagnostics.

**Use cases:**
- ✅ Email delivery troubleshooting
- ✅ DNS validation
- ✅ Blacklist monitoring
- ✅ SMTP diagnostics
- ✅ Domain health checks

**Why it's useful:**  
Fast, visual, and widely trusted for day‑to‑day email and DNS diagnostics. Comprehensive suite of tools in one place.

**Key features:**
- MX Lookup
- Blacklist Check
- DNS Lookup
- SMTP Test
- SPF/DKIM/DMARC Validation

---

### Cloudflare Tools

**Links:**
- [Cloudflare](https://www.cloudflare.com/)
- [Cloudflare DNS](https://1.1.1.1/)
- [Is It Down?](https://www.isitdownrightnow.com/)
- [Cloudflare Radar](https://radar.cloudflare.com/)

**Purpose:**  
CDN, DNS, security, and performance tools.

**Use cases:**
- ✅ DDoS protection
- ✅ Content delivery network
- ✅ DNS management
- ✅ SSL/TLS encryption
- ✅ Web application firewall

---

### Postman

**Links:**
- [Postman](https://www.postman.com/)
- [Postman Learning Center](https://learning.postman.com/)
- [Postman API Platform](https://www.postman.com/api-platform/)

**Purpose:**  
API development and testing platform.

**Use cases:**
- ✅ API testing and debugging
- ✅ Request collection management
- ✅ Automated testing
- ✅ API documentation
- ✅ Team collaboration

**Key features:**
- REST, GraphQL, SOAP support
- Environment variables
- Pre-request scripts
- Test automation
- Mock servers

---

### Pingdom

**Links:**
- [Pingdom](https://www.pingdom.com/)
- [Pingdom Free Tools](https://tools.pingdom.com/)
- [Page Speed Test](https://tools.pingdom.com/)

**Purpose:**  
Uptime and synthetic monitoring.

**Use cases:**
- ✅ Website uptime monitoring
- ✅ Performance testing
- ✅ Page speed analysis
- ✅ Transaction monitoring
- ✅ Real user monitoring (RUM)

**Key features:**
- Multi-location checks
- Alerting
- Public status pages
- Root cause analysis
- Performance reports

---

## 🏢 Vendor & Platform Portals
<a id="vendor--platform-portals"></a>

### Ticketing Systems (Jira / Service Desk)

**Links:**
- [Jira Service Management](https://www.atlassian.com/software/jira/service-management)
- [ServiceNow](https://www.servicenow.com/)
- [Zendesk](https://www.zendesk.com/)
- [Freshservice](https://freshservice.com/)

**Purpose:**  
Track incidents, requests, and changes.

**Use cases:**
- ✅ ITSM workflows
- ✅ Audit trails
- ✅ Operational reporting
- ✅ Change management
- ✅ Knowledge base management

---

### MSP & Partner Portals

**Links:**
- [Microsoft Partner Center](https://partner.microsoft.com/)
- [AWS Partner Central](https://partnercentral.awspartner.com/)
- [Google Cloud Partner Advantage](https://cloud.google.com/partners)

**Purpose:**  
Manage licenses, customers, and integrations.

**Use cases:**
- ✅ Subscription management
- ✅ Customer onboarding/offboarding
- ✅ Billing and reporting
- ✅ Deal registration
- ✅ Technical support

---

### Licensing Portals

**Links:**
- [Microsoft 365 Admin Center](https://admin.microsoft.com/)
- [Azure Portal Licensing](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)
- [Adobe Admin Console](https://adminconsole.adobe.com/)
- [VMware Customer Connect](https://customerconnect.vmware.com/)

**Purpose:**  
Manage software licenses and subscriptions.

**Use cases:**
- ✅ License assignment and removal
- ✅ Usage monitoring
- ✅ Renewal management
- ✅ Compliance tracking
- ✅ Cost optimization

---

## 📚 How to Use This Document
<a id="how-to-use-this-document"></a>

**Best practices:**
- ✅ Treat this as a **living reference**
- ✅ Add internal tools and links specific to your environment
- ✅ Keep descriptions short and operationally focused
- ✅ Link this file from READMEs and onboarding docs
- ✅ Update regularly as new tools are adopted
- ✅ Share with new team members during onboarding

**Maintenance:**
- Review quarterly for outdated links
- Add new tools as they are adopted
- Include feedback from team members
- Document internal tool access procedures

**Related Resources:**
- [PowerShell Training](./Student%20Resources/PowerShell/README.md)
- [Terraform Training](./Student%20Resources/Terraform/README.md)
- [Cloud Resources](./README.md#-cloud--platform-resources)

---

<p align="center">
  <sub>Last updated: February 7, 2026</sub><br>
  <sub><strong>Maintained by:</strong> Resources Repository Contributors</sub>
</p>

---

**[⬆ Back to Top](#️-admin-tools-reference-guide)**
