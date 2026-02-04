# 🧪 AZ-700 Hands-On Labs

**Azure Network Engineer Associate Practical Experience**

---

## Table of Contents

1. [Lab 1: Virtual Networks & Subnets](#lab-1-virtual-networks--subnets)
2. [Lab 2: Site-to-Site VPN & Hybrid Connectivity](#lab-2-site-to-site-vpn--hybrid-connectivity)
3. [Lab 3: Azure ExpressRoute Configuration](#lab-3-azure-expressroute-configuration)
4. [Lab 4: Load Balancing & Application Gateway](#lab-4-load-balancing--application-gateway)
5. [Lab 5: Network Security & Monitoring](#lab-5-network-security--monitoring)
6. [Lab 6: Azure DNS & Private DNS Zones](#lab-6-azure-dns--private-dns-zones)
7. [Lab 7: Network Security Groups & Application Security Groups](#lab-7-network-security-groups--application-security-groups)
8. [Lab 8: Azure Front Door & CDN Configuration](#lab-8-azure-front-door--cdn-configuration)
9. [Lab 9: Network Performance Monitoring & Connection Monitor](#lab-9-network-performance-monitoring--connection-monitor)
10. [Lab 10: Azure Bastion & Just-In-Time VM Access](#lab-10-azure-bastion--just-in-time-vm-access)

---

## Lab 1: Virtual Networks & Subnets

### Objective

Design and implement a multi-tier virtual network architecture with proper segmentation and routing

**Estimated Duration:** 50 minutes

**Prerequisites:**

- Azure subscription with Owner or Contributor role
- Access to Azure Portal
- Basic understanding of IP addressing (CIDR notation)

### Step-by-Step Instructions

#### Task 1: Create a Virtual Network with Multiple Subnets

1. Navigate to **Virtual networks** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az700-network-lab"
   - Name: `vnet-multitier`
   - Region: East US
   - IPv4 address space: 10.0.0.0/16
4. Click **Next: Subnets**
5. Delete the default subnet
6. Create multiple subnets:
   - **Web Tier**
     - Name: `subnet-web`
     - Address range: 10.0.1.0/24
   - **Application Tier**
     - Name: `subnet-app`
     - Address range: 10.0.2.0/24
   - **Database Tier**
     - Name: `subnet-db`
     - Address range: 10.0.3.0/24
   - **Gateway Subnet** (for VPN/ExpressRoute)
     - Name: `GatewaySubnet`
     - Address range: 10.0.0.0/27
7. Click **Review + create**, then **Create**

#### Task 2: Create Additional VNets for Peering

1. Repeat Task 1 to create a second VNet:
   - Name: `vnet-peered`
   - Resource Group: az700-network-lab
   - IPv4 address space: 10.1.0.0/16
   - Create subnet: `subnet-peered` (10.1.1.0/24)

#### Task 3: Implement VNet Peering

1. Navigate to the first VNet: `vnet-multitier`
2. Go to **Peerings** (under Settings)
3. Click **+ Add**
4. Configure peering:
   - Peering name: `peer-multitier-to-peered`
   - Remote VNet: `vnet-peered`
   - Allow forwarded traffic: **Checked**
   - Allow gateway transit: **Checked**
5. Click **Add**
6. Return to `vnet-peered` and verify peering appears
7. Click on the peering and modify:
   - Allow gateway transit: **Checked** (for hybrid connectivity)

#### Task 4: Create User Defined Routes

1. Navigate to **Route tables** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az700-network-lab
   - Name: `udr-app-tier`
   - Region: East US
4. After creation, click **Go to resource**
5. Go to **Routes**
6. Click **+ Add**
7. Create a custom route:
   - Route name: `route-to-db`
   - Address prefix: 10.0.3.0/24
   - Next hop type: Virtual Appliance
   - Next hop address: 10.0.2.254 (simulated appliance)
8. Click **Add**
9. Go to **Subnets**
10. Click **+ Associate**
11. Select VNet: `vnet-multitier`, Subnet: `subnet-app`
12. Click **OK**

#### Task 5: Configure DNS Settings

1. Navigate to `vnet-multitier`
2. Go to **DNS servers** (under Settings)
3. Select **Custom**
4. Add Azure-provided DNS: 168.63.129.16
5. Click **Save**
6. Navigate to `vnet-peered` and repeat

**Key Takeaways:**

- VNets provide network isolation and allow logical network segmentation
- Subnets enable further segmentation within a VNet
- VNet peering allows direct communication between VNets without routing through the internet
- User Defined Routes override default Azure routing behavior
- Gateway subnets are required for VPN/ExpressRoute connectivity
- Custom DNS enables hybrid cloud name resolution

**Troubleshooting:**

- **Issue:** Cannot ping between peered VNets
  - **Solution:** Verify NSG rules allow ICMP; ensure peering status shows "Connected"

- **Issue:** Peering shows "InitiatedByRemoteNetwork" and not "Connected"
  - **Solution:** Peering requires acceptance from the remote side; you created it from one side; verify the connection status

### Cleanup

1. Delete peering relationships
2. Delete route tables
3. Delete virtual networks
4. Delete the resource group "az700-network-lab"

---

## Lab 2: Site-to-Site VPN & Hybrid Connectivity

### Objective

Configure a site-to-site VPN connection to simulate on-premises connectivity

**Estimated Duration:** 55 minutes

**Prerequisites:**

- Lab 1 completed (or existing VNet with GatewaySubnet)
- Azure subscription with Owner or Contributor role

### Step-by-Step Instructions

#### Task 1: Create a VPN Gateway

1. Navigate to **Virtual network gateways** in Azure Portal
2. Click **Create**
3. Configure:
   - Name: `vpn-gateway-lab`
   - Gateway type: VPN
   - VPN type: Route-based
   - SKU: VpnGw1 (or VpnGw2 for higher throughput)
   - Virtual network: `vnet-multitier` (from Lab 1)
   - Gateway subnet: GatewaySubnet (should be auto-populated)
   - Public IP address: Create new `pip-vpn-gateway`
   - Enable active-active mode: Disabled (for this lab)
   - Configure BGP: Optional (enable for advanced routing)
4. Click **Review + create**, then **Create**
5. **Wait for deployment** (this typically takes 45 minutes)

#### Task 2: Create a Local Network Gateway

1. While VPN Gateway is deploying, navigate to **Local network gateways**
2. Click **Create**
3. Configure to simulate on-premises:
   - Resource Group: az700-network-lab
   - Name: `lng-onprem`
   - Endpoint: IP address (use a public IP you have access to, or simulate: 203.0.113.100)
   - Address space: 192.168.0.0/16 (representing on-premises network)
4. Click **Create**

#### Task 3: Create VPN Connection

1. Navigate back to **Virtual network gateways**
2. Once VPN gateway is deployed, click on `vpn-gateway-lab`
3. Go to **Connections** (under Settings)
4. Click **+ Add**
5. Configure connection:
   - Name: `conn-s2s-vpn`
   - Connection type: Site-to-Site (S2S)
   - Virtual network gateway: vpn-gateway-lab (auto-filled)
   - Local network gateway: lng-onprem
   - Shared key (PSK): `Azure123!@#` (create a strong pre-shared key)
   - Use Azure Private IP for local gateway: Unchecked
6. Click **OK**
7. **Status will show "Connecting"** - wait for it to reach "Connected"

#### Task 4: Configure On-Premises Simulation (Optional)

1. To fully test connectivity, you could:
   - Deploy a VPN client on an on-premises VM or local machine
   - Configure point-to-site VPN for personal testing
   - For this lab, we'll verify configuration instead
2. In Azure Portal, go to VPN gateway > **Connections**
3. Click on `conn-s2s-vpn`
4. Verify:
   - Connection status (should eventually show "Connected")
   - Egress/Ingress bytes (will show traffic flow once connected)
   - Connection speeds and diagnostics

#### Task 5: Create Route Table for On-Premises Traffic

1. Navigate to **Route tables**
2. Create new route table: `udr-onprem-routes`
3. Add routes to the VPN gateway:
   - Route name: `route-to-onprem`
   - Address prefix: 192.168.0.0/16 (on-premises)
   - Next hop type: Virtual network gateway
   - Next hop address: (auto-filled)
4. Associate with subnet: `subnet-web` in `vnet-multitier`
5. This ensures that traffic destined for on-premises routes through the VPN gateway

#### Task 6: Test Connectivity (Simulation)

1. Navigate to **Network Watcher** > **IP Flow Verify**
2. Configure:
   - Subscription: Your subscription
   - Resource Group: az700-network-lab
   - Network interface: Select a VM NIC (if you have VMs from previous labs)
   - Protocol: TCP or ICMP
   - Local IP: VM's private IP
   - Local port: 22 or 3389 (SSH/RDP)
   - Remote IP: On-premises network IP (192.168.1.100)
   - Remote port: 22 or 3389
3. Click **Check**
4. Result shows whether traffic WOULD be allowed based on NSGs and routes

**Key Takeaways:**

- VPN Gateways enable encrypted site-to-site connectivity
- Route-based VPNs use dynamic routing (BGP); Policy-based are legacy
- Local Network Gateways represent on-premises networks
- Shared keys (PSK) authenticate the VPN connection
- Route tables direct on-premises traffic through the VPN gateway
- Connection status indicates whether the tunnel is established

**Troubleshooting:**

- **Issue:** Connection status shows "NotConnected"
  - **Solution:** Verify VPN gateway has fully deployed (45+ minutes); check shared key matches both sides; verify local network gateway endpoint IP is reachable

- **Issue:** Traffic not routing through VPN
  - **Solution:** Verify route tables are associated with subnets; check that route points to the VPN gateway

### Cleanup

1. Delete VPN connections
2. Delete Virtual Network Gateways
3. Delete Local Network Gateways
4. Delete route tables
5. Delete public IPs associated with gateways
6. Delete the resource group "az700-network-lab"

---

## Lab 3: Azure ExpressRoute Configuration

### Objective

Understand and configure Azure ExpressRoute for dedicated hybrid connectivity

**Estimated Duration:** 45 minutes

**Prerequisites:**

- Lab 1 completed (or existing VNet)
- Azure subscription with Owner or Contributor role
- Note: Full ExpressRoute setup requires ISP coordination; this lab simulates the configuration

### Step-by-Step Instructions

#### Task 1: Create ExpressRoute Circuit

1. Navigate to **ExpressRoute circuits** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az700-expressroute-lab"
   - Name: `er-circuit-lab`
   - Port: Choose a location (e.g., New York, Silicon Valley)
   - Bandwidth: 50 Mbps (smallest option for lab)
   - Billing model: Metered
   - Classic/Resource Manager: Resource Manager
4. Click **Review + create**, then **Create**
5. Once created, navigate to the circuit
6. Note the **Service Key** - this is provided to the ISP to provision the circuit

#### Task 2: Configure Peering (Azure Private Peering)

1. In the ExpressRoute circuit, go to **Peerings** (under Settings)
2. Click **+ Add**
3. Configure Azure Private Peering:
   - Peering type: Azure private
   - State: Enabled
   - Primary subnet: 192.168.1.0/30
   - Secondary subnet: 192.168.2.0/30
   - VLAN ID: 100 (example)
   - ASN: 65515 (primary), 65516 (secondary)
   - MD5 Hash: (optional - for security)
4. Click **Save**
5. Verify status shows "Provisioned" once the circuit is ready

#### Task 3: Configure Microsoft Peering (Optional)

1. In the same Peerings section, click **+ Add**
2. Configure Microsoft Peering:
   - Peering type: Microsoft
   - State: Enabled
   - Advertised public prefixes: Your public IP range (e.g., 203.0.113.0/24)
   - Customer ASN: Your autonomous system number
   - Routing registry name: ARIN (or appropriate for your region)
   - MD5 Hash: (optional)
3. Click **Save**

#### Task 4: Create Virtual Network Gateway for ExpressRoute

1. Navigate to **Virtual network gateways**
2. Click **Create**
3. Configure:
   - Name: `er-gateway-lab`
   - Gateway type: ExpressRoute
   - SKU: Standard or HighPerformance
   - Virtual network: `vnet-multitier` (from Lab 1, or create new)
   - Gateway subnet: GatewaySubnet or create new
4. Click **Review + create**, then **Create**
5. Wait for deployment (typically 45 minutes)

#### Task 5: Create Connection between Circuit and Gateway

1. Once ExpressRoute gateway is deployed, navigate back to the **ExpressRoute circuit**
2. Go to **Connections** (under Settings)
3. Click **+ Add**
4. Configure:
   - Name: `conn-circuit-to-vnet`
   - Virtual network gateway: `er-gateway-lab`
   - Authorization key: (typically pre-generated from circuit)
5. Click **Create**
6. Status will show "Connecting" then progress to "Provisioned"

#### Task 6: Configure Route Filters (for Microsoft Peering)

1. Navigate to **Route filters** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az700-expressroute-lab
   - Name: `rf-expressroute-lab`
   - Region: Same as circuit
4. Go to **Manage rules**
5. Add a rule:
   - Service name: Office365 (or others like Azure)
   - Click **Add**
6. Associate with peering:
   - Go to ExpressRoute circuit > Peerings
   - Select Microsoft peering
   - Add route filter: rf-expressroute-lab

#### Task 7: Monitor Circuit Health

1. In the ExpressRoute circuit, go to **Metrics** (under Monitoring)
2. Configure charts to monitor:
   - **BitsInPerSecond**: Inbound traffic
   - **BitsOutPerSecond**: Outbound traffic
   - **BGP Availability**: BGP session status (should be 100% when connected)
   - **ARP Availability**: Link availability
3. Note: These metrics will show real values once the circuit is actively connected

#### Task 8: View BGP Configuration Details

1. In the ExpressRoute circuit, go to **Peerings**
2. Click on **Azure private** peering
3. View BGP configuration:
   - Primary BGP IP: Used for on-premises router BGP peering
   - Secondary BGP IP: Backup BGP connection
   - BGP status: Shows if sessions are established
   - Published prefixes: Routes Azure will advertise

**Key Takeaways:**

- ExpressRoute provides dedicated, private connectivity with guaranteed bandwidth
- Azure Private Peering connects on-premises to Azure VNets
- Microsoft Peering connects to Microsoft 365 and Azure services over the internet
- BGP manages dynamic routing and failover
- Route Filters control which service prefixes are advertised
- ExpressRoute requires ISP partnership; Azure's role is configuration and monitoring

**Troubleshooting:**

- **Issue:** Circuit status shows "NotProvisioned"
  - **Solution:** Service key must be sent to ISP; they provision the circuit; this is normal until ISP completes their side

- **Issue:** BGP status shows "Down"
  - **Solution:** Verify on-premises BGP configuration; ensure BGP IP addresses match what Azure expects

### Cleanup

1. Delete connections between circuit and gateway
2. Delete Virtual Network Gateways
3. Delete Route Filters
4. Delete ExpressRoute circuits
5. Delete the resource group "az700-expressroute-lab"

---

## Lab 4: Load Balancing & Application Gateway

### Objective

Configure application-layer load balancing with URL-based routing

**Estimated Duration:** 50 minutes

**Prerequisites:**

- Azure subscription with Contributor role
- 2-3 virtual machines or App Service instances (can be created in this lab)
- Basic understanding of HTTP/HTTPS

### Step-by-Step Instructions

#### Task 1: Create Backend Resources

1. Navigate to **Virtual machines** (or use existing App Services)
2. Create 2-3 VMs or web apps that will serve as backends:
   - VM1: `vm-backend-1` (Windows Server 2022 with IIS)
   - VM2: `vm-backend-2` (Windows Server 2022 with IIS)
   - VM3: `vm-backend-3` (optional, for testing failover)
3. Configure each with:
   - Resource Group: Create new "az700-appgw-lab"
   - Virtual Network: Create new `vnet-appgw`
   - Subnet: Create `subnet-backend` (10.2.1.0/24)
   - Public inbound ports: Allow HTTP (80) and HTTPS (443)
4. After deployment, RDP into each VM and:
   - Install IIS (if Windows Server)
   - Create simple web pages with identifying text (e.g., "Backend 1", "Backend 2")
   - Or deploy a basic web application

#### Task 2: Create an Application Gateway

1. Navigate to **Application Gateways** in Azure Portal
2. Click **Create**
3. Configure basics:
   - Resource Group: az700-appgw-lab
   - Name: `appgw-lab`
   - Region: Same as VMs
   - Tier: Standard v2
   - Enable autoscaling: Yes
   - Minimum scale units: 1
   - Maximum scale units: 3
4. Click **Next: Frontends**
5. Configure frontend:
   - Frontend IP address type: Public
   - Create new public IP: `pip-appgw-lab`
6. Click **Next: Backends**
7. Add backend pool:
   - Name: `backend-pool-1`
   - Target type: Virtual machine or IP address
   - Add your VMs/web apps to the pool
8. Click **Add another backend pool**
9. Create second pool: `backend-pool-api`
   - Add different targets or leave for later

#### Task 3: Configure HTTP Settings and Routing Rules

1. Click **Next: Configuration**
2. Create HTTP settings:
   - Name: `http-settings-1`
   - Backend protocol: HTTP
   - Backend port: 80
   - Cookie-based affinity: Disabled
   - Connection draining: Enabled (5 minutes)
   - Request timeout: 20 seconds
3. Create routing rules:
   - Rule name: `rule-path-based`
   - Listener name: `listener-http`
   - Frontend IP: Public
   - Protocol: HTTP
   - Port: 80
   - Rule type: Path-based
4. Configure paths:
   - Path 1: `/api/*` → Route to `backend-pool-api`
   - Path 2: `/` → Route to `backend-pool-1`
5. Click **Next: Tags**
6. Add tags (optional):
   - Environment: Lab
   - Purpose: AZ-700
7. Click **Review + create**, then **Create**

#### Task 4: Test Load Balancing

1. Once Application Gateway is deployed, navigate to its overview page
2. Note the **Frontend public IP address**
3. Open a web browser and navigate to: `http://<frontend-ip>/`
4. You should see content from one of your backend VMs
5. Refresh the page multiple times
6. Observe if the backend changes (load balancing in action)
7. Navigate to: `http://<frontend-ip>/api/` (if you configured API backend)
8. Should route to the API backend pool

#### Task 5: Configure Health Probes

1. In the Application Gateway, go to **Health probes** (under Settings)
2. The default health probe should already exist
3. Review its configuration:
   - Protocol: HTTP
   - Host: 127.0.0.1
   - Path: /
   - Interval: 30 seconds
   - Timeout: 30 seconds
4. Modify to match your backend:
   - Host: Leave as is (or use FQDN if needed)
   - Path: /health (if your app has a health endpoint)
5. Click **Save**

#### Task 6: Test Failover

1. Go to one of your backend VMs
2. Stop the VM (simulate failure)
3. Return to the Application Gateway browser test
4. The health probe will detect the unhealthy backend within 30 seconds
5. Refresh the browser page
6. Traffic should now route to the remaining healthy backend
7. Start the VM again
8. After health checks pass, traffic will resume routing to it

#### Task 7: Configure HTTPS (Optional)

1. For production, configure HTTPS:
   - Obtain or create a self-signed certificate
   - In Application Gateway > Listeners, create HTTPS listener
   - Upload certificate
   - Create HTTPS routing rule
   - Configure HTTP-to-HTTPS redirect

**Key Takeaways:**

- Application Gateway provides Layer 7 (application) load balancing
- Path-based routing routes requests based on URL paths
- Health probes detect unhealthy backends automatically
- Connection draining ensures graceful shutdown of connections
- Autoscaling handles traffic spikes automatically
- Sticky sessions can enable cookie-based affinity if needed

**Troubleshooting:**

- **Issue:** Application Gateway shows "Unhealthy" backends
  - **Solution:** Verify health probe settings; ensure backend listens on the probe port; check NSG allows traffic from gateway to backend

- **Issue:** Load balancing not occurring (same backend every time)
  - **Solution:** Check if sticky sessions are enabled; disable them for round-robin distribution

### Cleanup

1. Delete Application Gateway
2. Delete Virtual Machines or App Services
3. Delete Virtual Network
4. Delete public IPs
5. Delete the resource group "az700-appgw-lab"

---

## Lab 5: Network Security & Monitoring

### Objective

Implement comprehensive network security and monitoring with Azure Firewall and Network Watcher

**Estimated Duration:** 50 minutes

**Prerequisites:**

- Lab 1 completed (or existing VNet)
- Azure subscription with Owner or Contributor role

### Step-by-Step Instructions

#### Task 1: Create a Hub-and-Spoke Network with Azure Firewall

1. Navigate to **Virtual networks** in Azure Portal
2. Create hub VNet:
   - Name: `vnet-hub`
   - Resource Group: Create new "az700-security-lab"
   - Address space: 10.10.0.0/16
   - Subnet: `AzureFirewallSubnet` (10.10.0.0/26) - **MUST be named exactly this**
   - Additional subnet: `subnet-jumpbox` (10.10.1.0/24)
3. Create spoke VNet:
   - Name: `vnet-spoke`
   - Address space: 10.20.0.0/16
   - Subnet: `subnet-workload` (10.20.1.0/24)

#### Task 2: Create and Configure Azure Firewall

1. Navigate to **Firewalls** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az700-security-lab
   - Name: `fw-hub`
   - Region: East US
   - Firewall tier: Standard (or Premium for advanced features)
   - Virtual network: `vnet-hub`
   - Public IP: Create new `pip-firewall`
4. Click **Review + create**, then **Create**
5. After deployment, navigate to the firewall
6. Note its private IP address (e.g., 10.10.0.4)

#### Task 3: Configure Firewall Rules

1. In the Firewall, go to **Rules** (under Settings)
2. Click **+ Add NAT Rule Collection**:
   - Name: `nat-rules-lab`
   - Rule collection type: NAT
   - Add rule:
     - Name: `nat-rdp`
     - Protocol: TCP
     - Source: * (any)
     - Destination address: `pip-firewall` public IP
     - Destination port: 3389
     - Translated address: 10.10.1.4 (jumpbox VM IP)
     - Translated port: 3389
   - Click **Add**
3. Click **+ Add Network Rule Collection**:
   - Name: `net-rules-lab`
   - Rule collection type: Network
   - Action: Allow
   - Add rule:
     - Name: `allow-dns`
     - Protocol: UDP
     - Source addresses: 10.20.0.0/16 (spoke network)
     - Destination addresses: * (any)
     - Destination ports: 53 (DNS)
   - Click **Add**
4. Click **+ Add Application Rule Collection**:
   - Name: `app-rules-lab`
   - Rule collection type: Application
   - Action: Allow
   - Add rule:
     - Name: `allow-https-microsoft`
     - Source addresses: 10.20.0.0/16
     - Protocol:port: https:443
     - Target FQDNs: microsoft.com, azure.microsoft.com
   - Click **Add**

#### Task 4: Configure Firewall Routes

1. Navigate to **Route tables**
2. Create route table for spoke:
   - Name: `udr-spoke-to-fw`
   - Resource Group: az700-security-lab
3. Add route:
   - Name: `route-default-firewall`
   - Address prefix: 0.0.0.0/0
   - Next hop type: Virtual appliance
   - Next hop address: 10.10.0.4 (firewall's private IP)
4. Associate with spoke subnet:
   - Subnets > Associate
   - VNet: vnet-spoke
   - Subnet: subnet-workload

#### Task 5: Implement Network Segmentation with NSGs

1. Navigate to **Network security groups**
2. Create NSG for the hub:
   - Name: `nsg-hub`
   - Resource Group: az700-security-lab
3. Create NSG for the spoke:
   - Name: `nsg-spoke`
4. In `nsg-spoke`, configure inbound rules:
   - Allow traffic from hub to spoke (for firewall inspection)
   - Source: 10.10.0.0/16
   - Destination: Any
   - Protocol: Any
   - Action: Allow
5. Associate NSGs with subnets:
   - Hub NSG → subnet-jumpbox
   - Spoke NSG → subnet-workload

#### Task 6: Configure Azure Network Watcher

1. Navigate to **Network Watcher** in Azure Portal
2. Ensure it's enabled for your region
3. Go to **Topology** to visualize your network:
   - Select Resource Group: az700-security-lab
   - View the visual representation of your VNets, subnets, and connections
4. Go to **IP Flow Verify** to test connectivity:
   - VM: Select a VM in the spoke
   - Interface: Select its network interface
   - Protocol: TCP
   - Local IP: VM's private IP
   - Local port: 443
   - Remote IP: An Azure service IP (e.g., 13.107.42.14 for Microsoft)
   - Remote port: 443
   - Click **Check**
   - Result shows whether firewall rules allow the traffic

#### Task 7: Enable NSG Flow Logs

1. In Network Watcher, go to **NSG flow logs** (under Logs)
2. Click **+ Create**
3. Configure:
   - Select NSG: `nsg-spoke`
   - Subscription: Your subscription
   - Flow logs version: Version 2 (includes traffic tuple)
   - Storage account: Create new or select existing
   - Retention: 30 days
   - Traffic Analytics: Enable (recommended)
   - Workspace: Create new Log Analytics workspace
4. Click **Create**
5. After enabling, NSG flow logs will capture all traffic patterns

#### Task 8: Configure Azure Monitor Alerts

1. Navigate to **Monitor** > **Alerts**
2. Click **+ Create alert rule**
3. Configure alert:
   - Resource: Select your firewall
   - Condition: Create custom
   - Signal: Firewall rule hit count
   - Operator: Greater than
   - Threshold: 1000 (example)
   - Aggregation type: Total
   - Check frequency: 5 minutes
4. Configure notification:
   - Action group: Create new
   - Name: `ag-firewall-alerts`
   - Add notification: Email
5. Click **Create alert rule**

#### Task 9: Review Firewall Logs

1. In the Azure Firewall, go to **Logs** (under Monitoring)
2. Run a pre-built query:
   - Select **AzureDiagnostics**
   - Filter: where ResourceType == "AZUREFIREWALLS"
3. Review:
   - Denied connections (high priority)
   - Allowed connections
   - Rule hits
   - Protocol distributions

**Key Takeaways:**

- Azure Firewall provides centralized application and network filtering
- NSGs provide granular, network-interface-level security
- Network Watcher provides visibility and troubleshooting tools
- NAT rules enable port forwarding (RDP, SSH to internal resources)
- Network and Application rules control traffic flow
- Flow logs enable detailed traffic analysis and compliance auditing
- Traffic Analytics provides automated insights into traffic patterns

**Troubleshooting:**

- **Issue:** Traffic blocked by firewall unexpectedly
  - **Solution:** Check firewall rules; verify source/destination addresses; check NSG rules as well

- **Issue:** NSG flow logs showing no data
  - **Solution:** Ensure storage account is accessible; verify Log Analytics workspace is created; wait 5-10 minutes for data to appear

### Cleanup

1. Delete Azure Firewall
2. Delete route tables
3. Delete Network Security Groups
4. Delete virtual networks
5. Delete public IPs
6. Delete Log Analytics workspace (optional, for cost)
7. Delete the resource group "az700-security-lab"

---

## Lab 6: Azure DNS & Private DNS Zones

### Objective

Configure Azure DNS for public domain resolution and Private DNS Zones for internal name resolution

**Estimated Duration:** 40 minutes

**Prerequisites:**

- Azure subscription with Contributor role
- A domain name (optional for full testing)
- Existing VNet from previous labs or create new

### Step-by-Step Instructions

#### Task 1: Create a Public DNS Zone

1. Navigate to **DNS zones** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az700-dns-lab"
   - Name: `contoso.com` (use your own domain if available)
   - Resource group location: East US
4. Click **Review + create**, then **Create**
5. Once created, note the **Name servers** (e.g., ns1-01.azure-dns.com)
6. If you own the domain, update your domain registrar to use these Azure DNS name servers

#### Task 2: Add DNS Records to Public Zone

1. Navigate to your DNS zone: `contoso.com`
2. Click **+ Record set**
3. Create an A record:
   - Name: `www`
   - Type: A
   - TTL: 3600
   - IP address: 20.81.111.50 (example public IP)
4. Click **OK**
5. Create a CNAME record:
   - Name: `blog`
   - Type: CNAME
   - TTL: 3600
   - Alias: `www.contoso.com`
6. Click **OK**
7. Create an MX record (for email):
   - Name: `@` (represents root domain)
   - Type: MX
   - TTL: 3600
   - Preference: 10
   - Mail server: `mail.contoso.com`
8. Click **OK**

#### Task 3: Create a Private DNS Zone

1. Navigate to **Private DNS zones** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: az700-dns-lab
   - Name: `internal.contoso.com`
4. Click **Review + create**, then **Create**

#### Task 4: Link Private DNS Zone to Virtual Networks

1. Once Private DNS Zone is created, go to the resource
2. Navigate to **Virtual network links** (under Settings)
3. Click **+ Add**
4. Configure:
   - Link name: `link-vnet-multitier`
   - Virtual network: Select `vnet-multitier` (from Lab 1 or create new)
   - Enable auto registration: **Checked** (automatically registers VM DNS records)
5. Click **OK**
6. Repeat for additional VNets if needed

#### Task 5: Add Records to Private DNS Zone

1. In the Private DNS Zone `internal.contoso.com`, click **+ Record set**
2. Create an A record for a database server:
   - Name: `sql-primary`
   - Type: A
   - TTL: 300
   - IP address: 10.0.3.4 (database tier subnet IP)
3. Click **OK**
4. Create another A record:
   - Name: `sql-secondary`
   - Type: A
   - IP address: 10.0.3.5
5. Create a PTR record for reverse DNS (optional):
   - Navigate to the corresponding reverse lookup zone or manually configure

#### Task 6: Test DNS Resolution from VMs

1. Deploy or access a VM in the linked VNet
2. RDP or SSH into the VM
3. Test public DNS resolution:

   ```powershell
   nslookup www.contoso.com
   ```

   Should resolve to the public IP you configured
4. Test private DNS resolution:

   ```powershell
   nslookup sql-primary.internal.contoso.com
   ```

   Should resolve to 10.0.3.4
5. Test auto-registration (if enabled):
   - Create a new VM in the linked VNet
   - The VM's name should automatically appear in the Private DNS Zone

#### Task 7: Configure DNS Forwarding (Conditional Forwarders)

1. To enable hybrid DNS resolution, configure conditional forwarding on on-premises DNS servers:
   - Forward queries for `internal.contoso.com` to Azure DNS: 168.63.129.16
   - This allows on-premises resources to resolve Azure private DNS names
2. In Azure, configure custom DNS on VNets:
   - Navigate to VNet > DNS servers
   - Select Custom
   - Add on-premises DNS server IPs
   - This allows Azure VMs to resolve on-premises DNS names

#### Task 8: Create DNS Alias Records

1. In the Public DNS Zone, create an alias record:
   - Name: `app`
   - Type: A
   - Alias: Yes
   - Alias type: Azure resource
   - Azure resource: Select an Application Gateway or Public IP
2. Click **OK**
3. Alias records automatically update when the target resource IP changes

#### Task 9: Monitor DNS Queries

1. Navigate to **DNS zones** > `contoso.com`
2. Go to **Metrics** (under Monitoring)
3. Add metrics:
   - **Query Volume**: Total DNS queries
   - **Record Set Query Rate**: Queries per record set
   - **Record Set Count**: Number of records
4. Set time range to view recent activity
5. For advanced monitoring, enable diagnostic logs:
   - Go to **Diagnostic settings**
   - Add diagnostic setting
   - Send to Log Analytics workspace
   - Enable QueryLog

**Key Takeaways:**

- Azure DNS provides highly available, scalable DNS hosting
- Public DNS zones host internet-facing domain records
- Private DNS zones enable internal name resolution without custom DNS servers
- Auto-registration automatically adds VM DNS records
- VNet links connect Private DNS zones to virtual networks
- DNS forwarding enables hybrid cloud name resolution
- Alias records simplify DNS management for Azure resources

**Troubleshooting:**

- **Issue:** Private DNS not resolving from VMs
  - **Solution:** Verify VNet link is created and active; check VM is using Azure DNS (168.63.129.16); ensure NSG allows DNS traffic

- **Issue:** Auto-registration not working
  - **Solution:** Verify auto-registration is enabled on VNet link; check VM has a network interface in the linked VNet

### Cleanup

1. Delete Private DNS zone virtual network links
2. Delete Private DNS zones
3. Delete Public DNS zones (if testing only)
4. Delete the resource group "az700-dns-lab"

---

## Lab 7: Network Security Groups & Application Security Groups

### Objective

Implement granular network security using NSGs and simplify rule management with Application Security Groups

**Estimated Duration:** 45 minutes

**Prerequisites:**

- Azure subscription with Contributor role
- Existing VNet with multiple subnets (from Lab 1 or create new)
- Multiple VMs representing different application tiers

### Step-by-Step Instructions

#### Task 1: Create Application Security Groups

1. Navigate to **Application security groups** in Azure Portal
2. Click **Create**
3. Create ASG for web tier:
   - Resource Group: Create new "az700-asg-lab"
   - Name: `asg-web-servers`
   - Region: East US
4. Click **Review + create**, then **Create**
5. Repeat to create additional ASGs:
   - `asg-app-servers` (for application tier)
   - `asg-db-servers` (for database tier)
   - `asg-mgmt-servers` (for management/jumpbox VMs)

#### Task 2: Assign VMs to Application Security Groups

1. Navigate to one of your web tier VMs
2. Go to **Networking** > **Application security groups**
3. Click **Configure the application security groups**
4. Add the VM to `asg-web-servers`
5. Click **Save**
6. Repeat for other VMs:
   - Application tier VMs → `asg-app-servers`
   - Database tier VMs → `asg-db-servers`
   - Management VMs → `asg-mgmt-servers`

#### Task 3: Create Network Security Groups

1. Navigate to **Network security groups**
2. Click **Create**
3. Create NSG for web tier:
   - Resource Group: az700-asg-lab
   - Name: `nsg-web-tier`
   - Region: East US
4. Click **Review + create**, then **Create**
5. Repeat to create NSGs for other tiers:
   - `nsg-app-tier`
   - `nsg-db-tier`

#### Task 4: Configure NSG Rules Using ASGs

1. Navigate to `nsg-web-tier`
2. Go to **Inbound security rules**
3. Click **+ Add**
4. Create rule to allow HTTP traffic:
   - Source: Any (Internet)
   - Source port ranges: *
   - Destination: Application security group
   - Destination ASG: `asg-web-servers`
   - Service: HTTP
   - Action: Allow
   - Priority: 100
   - Name: `Allow-HTTP-Internet`
5. Click **Add**
6. Create rule to allow HTTPS:
   - Source: Any
   - Destination ASG: `asg-web-servers`
   - Service: HTTPS
   - Priority: 110
   - Name: `Allow-HTTPS-Internet`
7. Create rule to deny all other inbound traffic:
   - Source: Any
   - Destination ASG: `asg-web-servers`
   - Service: Custom
   - Protocol: Any
   - Action: Deny
   - Priority: 4096
   - Name: `Deny-All-Inbound`

#### Task 5: Configure Application Tier NSG Rules

1. Navigate to `nsg-app-tier`
2. Add inbound rule to allow traffic from web tier:
   - Source: Application security group
   - Source ASG: `asg-web-servers`
   - Destination ASG: `asg-app-servers`
   - Service: Custom
   - Port range: 8080 (or your app port)
   - Protocol: TCP
   - Action: Allow
   - Priority: 100
   - Name: `Allow-Web-to-App`
3. Add rule to allow management access:
   - Source ASG: `asg-mgmt-servers`
   - Destination ASG: `asg-app-servers`
   - Service: RDP or SSH
   - Priority: 110
   - Name: `Allow-Mgmt-RDP`
4. Deny all other traffic:
   - Priority: 4096
   - Name: `Deny-All-Inbound`

#### Task 6: Configure Database Tier NSG Rules

1. Navigate to `nsg-db-tier`
2. Add rule to allow database connections from app tier:
   - Source ASG: `asg-app-servers`
   - Destination ASG: `asg-db-servers`
   - Service: MS SQL (1433) or MySQL (3306)
   - Priority: 100
   - Name: `Allow-App-to-DB`
3. Add management access:
   - Source ASG: `asg-mgmt-servers`
   - Destination ASG: `asg-db-servers`
   - Service: RDP/SSH
   - Priority: 110
   - Name: `Allow-Mgmt-Access`
4. Deny all other inbound:
   - Priority: 4096

#### Task 7: Associate NSGs with Subnets

1. Navigate to `nsg-web-tier`
2. Go to **Subnets** (under Settings)
3. Click **+ Associate**
4. Select VNet and web tier subnet
5. Click **OK**
6. Repeat for other NSGs and their corresponding subnets

#### Task 8: Create Outbound Security Rules

1. In `nsg-app-tier`, go to **Outbound security rules**
2. Add rule to allow internet access for updates:
   - Source ASG: `asg-app-servers`
   - Destination: Internet
   - Service: HTTPS
   - Priority: 100
   - Name: `Allow-Internet-HTTPS`
3. Add rule to allow Azure service access:
   - Destination: Service Tag
   - Service Tag: AzureCloud
   - Priority: 110
   - Name: `Allow-Azure-Services`
4. Optionally deny all other outbound:
   - Priority: 4096
   - Action: Deny

#### Task 9: Test and Validate NSG Rules

1. Navigate to **Network Watcher** > **NSG diagnostics**
2. Select a VM in the web tier
3. Test connectivity:
   - Direction: Inbound
   - Protocol: TCP
   - Source IP: 203.0.113.100 (simulated internet IP)
   - Source port: *
   - Destination port: 80
4. Click **Check**
5. Result shows whether traffic is allowed and which rule applies
6. Test denied traffic:
   - Change destination port to 22 (SSH)
   - Should be denied by `Deny-All-Inbound` rule

#### Task 10: View Effective Security Rules

1. Navigate to a VM's network interface
2. Go to **Effective security rules** (under Support + troubleshooting)
3. View the combined rules from:
   - NSG associated with subnet
   - NSG associated with network interface
   - Default Azure security rules
4. This view shows the actual enforced rules in priority order

**Key Takeaways:**

- NSGs provide stateful packet filtering at subnet and NIC levels
- Application Security Groups simplify rule management by grouping VMs logically
- Rules are evaluated by priority (lower number = higher priority)
- Default rules allow VNet-to-VNet and load balancer traffic; deny all inbound internet
- NSG flow logs capture detailed traffic information
- Service tags represent groups of IP addresses (e.g., Internet, AzureCloud)
- Effective security rules show the actual enforced ruleset

**Troubleshooting:**

- **Issue:** Traffic unexpectedly blocked
  - **Solution:** Check effective security rules; verify ASG membership; ensure priority order is correct

- **Issue:** ASG rules not applying
  - **Solution:** Verify VM network interfaces are associated with ASGs; check NSG is associated with subnet or NIC

### Cleanup

1. Disassociate NSGs from subnets
2. Delete Network Security Groups
3. Delete Application Security Groups
4. Delete VMs (optional, if created for this lab)
5. Delete the resource group "az700-asg-lab"

---

## Lab 8: Azure Front Door & CDN Configuration

### Objective

Configure global load balancing and content delivery with Azure Front Door and CDN

**Estimated Duration:** 50 minutes

**Prerequisites:**

- Azure subscription with Contributor role
- Multiple web applications or storage accounts in different regions
- Basic understanding of HTTP/HTTPS and caching

### Step-by-Step Instructions

#### Task 1: Create Backend Web Applications

1. Navigate to **App Services** in Azure Portal
2. Create first web app:
   - Resource Group: Create new "az700-frontdoor-lab"
   - Name: `webapp-eastus-<unique>` (must be globally unique)
   - Publish: Code
   - Runtime: .NET, Node.js, or Python
   - Region: East US
   - Pricing plan: Basic B1
3. Click **Review + create**, then **Create**
4. Create second web app:
   - Name: `webapp-westus-<unique>`
   - Region: West US
   - Same configuration as first app
5. Optionally create a third app in Europe (West Europe or North Europe)
6. After deployment, add unique content to each app to identify the backend:
   - In App Service, use App Service Editor or upload via FTP
   - Create `index.html` with text like "East US Backend" or "West US Backend"

#### Task 2: Create Azure Front Door Profile

1. Navigate to **Front Door and CDN profiles** in Azure Portal
2. Click **Create**
3. Select **Azure Front Door** (not Classic)
4. Configure:
   - Resource Group: az700-frontdoor-lab
   - Name: `fd-global-<unique>`
   - Tier: Standard (or Premium for advanced features)
   - Endpoint name: `fd-endpoint-<unique>`
5. Click **Next: Origins**

#### Task 3: Configure Origin Groups and Origins

1. In the Origins tab, click **+ Add an origin group**
2. Configure origin group:
   - Name: `og-webapps`
   - Health probe: Enabled
   - Probe path: /
   - Probe protocol: HTTP
   - Probe method: HEAD
   - Interval: 30 seconds
3. Add origins to the group:
   - Click **+ Add an origin**
   - Origin name: `origin-eastus`
   - Origin type: App Service
   - Host name: Select `webapp-eastus-<unique>`
   - Priority: 1
   - Weight: 1000
4. Click **Add**
5. Add second origin:
   - Origin name: `origin-westus`
   - Host name: `webapp-westus-<unique>`
   - Priority: 1
   - Weight: 1000
6. Add third origin if available (same priority and weight for load balancing)
7. Click **Add** to save the origin group

#### Task 4: Configure Routes

1. Click **Next: Routing**
2. Configure default route:
   - Name: `route-default`
   - Domains: `fd-endpoint-<unique>.azurefd.net` (auto-populated)
   - Patterns to match: `/*`
   - Accepted protocols: HTTP and HTTPS
   - HTTPS redirect: Enabled (redirect HTTP to HTTPS)
   - Origin group: `og-webapps`
   - Forwarding protocol: HTTPS only
   - Caching: Enabled
   - Query string caching: Ignore query strings
3. Click **Add**
4. Click **Review + create**, then **Create**
5. Wait for Front Door deployment (5-10 minutes)

#### Task 5: Test Global Load Balancing

1. Once deployed, navigate to your Front Door resource
2. Note the **Endpoint hostname**: `fd-endpoint-<unique>.azurefd.net`
3. Open a web browser and navigate to: `https://fd-endpoint-<unique>.azurefd.net`
4. You should see content from one of your backend apps
5. Refresh multiple times - Front Door load balances across healthy origins
6. To test geographic routing:
   - Use a VPN to connect from different geographic locations
   - Front Door may route to the nearest available origin

#### Task 6: Configure Custom Domain (Optional)

1. If you have a custom domain, configure it:
   - In Front Door, go to **Domains** (under Settings)
   - Click **+ Add**
   - Enter your domain: `www.contoso.com`
   - DNS management: Azure DNS or external
2. Verify domain ownership:
   - Front Door provides a TXT or CNAME record
   - Add this record to your DNS zone
3. Associate domain with route:
   - Go to **Routes**
   - Edit `route-default`
   - Add custom domain to accepted domains
4. Enable HTTPS for custom domain:
   - Front Door auto-provisions SSL certificate (if using Azure DNS)
   - Or upload your own certificate

#### Task 7: Configure Caching Rules

1. In Front Door, go to **Rules engine** (under Settings)
2. Click **+ Add rule**
3. Create caching rule for static content:
   - Rule name: `cache-static-content`
   - Condition: Path
   - Operator: Contains
   - Value: `/images/`, `/css/`, `/js/`
   - Action: Override cache behavior
   - Cache duration: 1 day
4. Create rule for dynamic content:
   - Condition: Path
   - Value: `/api/`
   - Action: Bypass cache
5. Click **Save**

#### Task 8: Configure Web Application Firewall (WAF)

1. In Front Door, go to **Web Application Firewall** (under Settings)
2. Click **Create WAF policy**
3. Configure:
   - Resource Group: az700-frontdoor-lab
   - Name: `waf-frontdoor`
   - Policy mode: Prevention (blocks malicious requests)
   - Policy state: Enabled
4. Configure managed rules:
   - Enable default rule set (protects against OWASP Top 10)
   - Enable bot protection (optional)
5. Configure custom rules (optional):
   - Add rule to block specific IP ranges
   - Rate limiting rules to prevent DDoS
6. Click **Review + create**, then **Create**
7. Associate WAF policy with Front Door:
   - In Front Door > Security policies
   - Add the WAF policy to your endpoint

#### Task 9: Monitor Front Door Performance

1. In Front Door, go to **Metrics** (under Monitoring)
2. Add metrics to monitor:
   - **Request count**: Total requests
   - **Response time**: Latency for requests
   - **Backend health**: Health status of origins
   - **Cache hit ratio**: Percentage of cached responses
   - **WAF blocked requests**: Malicious requests blocked
3. Create dashboard for ongoing monitoring
4. Navigate to **Logs** to query detailed request logs:

   ```kql
   AzureDiagnostics
   | where ResourceType == "FRONTDOORS"
   | summarize count() by clientIp_s, httpStatusCode_s
   ```

#### Task 10: Test Failover

1. Stop one of your backend web apps (e.g., `webapp-eastus`)
2. Front Door's health probe detects the unhealthy backend within 30 seconds
3. Navigate to your Front Door endpoint
4. All traffic should now route to healthy backends only
5. In Front Door > Origins, verify the origin shows as unhealthy
6. Start the web app again
7. After health checks pass, traffic resumes routing to it

**Key Takeaways:**

- Azure Front Door provides global load balancing with intelligent routing
- Origin groups contain multiple backends for high availability
- Health probes automatically detect and route around unhealthy backends
- Caching at edge locations reduces latency and backend load
- WAF protects against common web vulnerabilities and bots
- Front Door supports both global and geo-based routing strategies
- Custom domains can be configured with auto-provisioned SSL certificates

**Troubleshooting:**

- **Issue:** Front Door returns 502 Bad Gateway
  - **Solution:** Verify origins are running and accessible; check health probe settings; ensure firewall/NSG allows Front Door traffic

- **Issue:** Caching not working
  - **Solution:** Verify caching is enabled in route configuration; check Cache-Control headers from origin; review Rules Engine configuration

### Cleanup

1. Delete Web Application Firewall policy
2. Delete Front Door profile
3. Delete App Services
4. Delete the resource group "az700-frontdoor-lab"

---

## Lab 9: Network Performance Monitoring & Connection Monitor

### Objective

Implement comprehensive network performance monitoring using Azure Monitor and Connection Monitor

**Estimated Duration:** 45 minutes

**Prerequisites:**

- Azure subscription with Contributor role
- Multiple VMs in different regions or VNets (from previous labs)
- Log Analytics workspace

### Step-by-Step Instructions

#### Task 1: Enable Network Watcher

1. Navigate to **Network Watcher** in Azure Portal
2. Verify Network Watcher is enabled for your regions:
   - Expand your subscription
   - Check that regions show "Enabled"
   - If not, click region and select **Enable Network Watcher**
3. Enable for all regions where you have resources:
   - East US
   - West US
   - (Any other regions with VMs/VNets)

#### Task 2: Create Log Analytics Workspace

1. Navigate to **Log Analytics workspaces**
2. Click **Create**
3. Configure:
   - Resource Group: Create new "az700-monitoring-lab"
   - Name: `law-network-monitoring`
   - Region: East US
   - Pricing tier: Pay-as-you-go
4. Click **Review + create**, then **Create**

#### Task 3: Install Network Watcher Extension on VMs

1. Navigate to one of your VMs
2. Go to **Extensions + applications** (under Settings)
3. Click **+ Add**
4. Search for and select **Network Watcher Agent for Windows** (or Linux)
5. Click **Next**, then **Review + create**, then **Create**
6. Wait for installation to complete
7. Repeat for all VMs you want to monitor

#### Task 4: Create Connection Monitor

1. Navigate to **Network Watcher** > **Connection monitor**
2. Click **+ Create**
3. Configure basics:
   - Name: `cm-vnet-connectivity`
   - Subscription: Your subscription
   - Region: East US
   - Workspace: `law-network-monitoring`
4. Click **Next: Test groups**
5. Click **+ Add test group**
6. Configure test group:
   - Name: `tg-web-to-app`
   - Sources: Add VMs from web tier
   - Destinations: Add VMs from app tier
   - Test configuration: Create new
     - Name: `tc-http-test`
     - Protocol: HTTP
     - Destination port: 80
     - Test frequency: 30 seconds
     - HTTP configuration: GET method, Path: `/`
7. Click **Add test group**
8. Create another test group for database connectivity:
   - Name: `tg-app-to-db`
   - Sources: App tier VMs
   - Destinations: DB tier VMs
   - Protocol: TCP
   - Port: 1433 (or 3306 for MySQL)
9. Click **Review + create**, then **Create**

#### Task 5: Configure Network Performance Monitor

1. In Network Watcher, go to **Network Performance Monitor** (under Monitoring)
2. If not already configured, click **Configure**
3. Select your Log Analytics workspace: `law-network-monitoring`
4. Enable the solution
5. Configure Performance Monitor:
   - Add monitoring rules for subnet-to-subnet connectivity
   - Set thresholds for packet loss (e.g., > 5%)
   - Set latency thresholds (e.g., > 100ms)
6. Configure Service Connectivity Monitor:
   - Add Office 365 endpoints to monitor
   - Add Azure service endpoints
7. Configure ExpressRoute Monitor (if you have ExpressRoute from Lab 3):
   - Monitor ExpressRoute circuit health
   - Track BGP status

#### Task 6: Enable Traffic Analytics

1. Navigate to **Network Watcher** > **Traffic Analytics**
2. Click **+ Add**
3. Configure:
   - NSG flow logs: Select NSGs from previous labs
   - Storage account: Select existing or create new
   - Traffic Analytics workspace: `law-network-monitoring`
   - Processing interval: 10 minutes
4. Click **OK**
5. Wait 10-20 minutes for data to start appearing

#### Task 7: Analyze Connection Monitor Data

1. In Network Watcher > Connection monitor, select `cm-vnet-connectivity`
2. View the **Dashboard**:
   - Overall health percentage
   - Failed tests
   - Latency trends
3. Go to **Test groups**:
   - Select `tg-web-to-app`
   - View hop-by-hop latency
   - Identify network bottlenecks
4. Go to **Alerts** (optional):
   - Create alert rules based on thresholds
   - Example: Alert when success rate < 95%

#### Task 8: View Traffic Analytics Insights

1. Navigate to **Network Watcher** > **Traffic Analytics**
2. View the **Geo map view**:
   - Shows traffic flow between regions
   - Identifies cross-region traffic patterns
3. View **Application ports** section:
   - Identifies which ports have the most traffic
   - Detects unexpected port usage (potential security issue)
4. View **Malicious flows**:
   - Shows traffic to/from known malicious IPs
   - Provides security insights
5. View **Flow distribution**:
   - Top talkers (VMs with most traffic)
   - Traffic volume trends

#### Task 9: Create Custom Log Queries

1. Navigate to **Log Analytics workspace** > `law-network-monitoring`
2. Go to **Logs**
3. Run query to analyze network performance:

   ```kql
   NetworkMonitoring
   | where TimeGenerated > ago(1h)
   | summarize avg(LossHealthPercentage), avg(LatencyHealthPercentage) by SubType, CircuitName
   | order by avg_LossHealthPercentage desc
   ```

4. Query Connection Monitor results:

   ```kql
   NWConnectionMonitorTestResult
   | where TimeGenerated > ago(1h)
   | summarize SuccessfulTests = countif(TestResult == "Pass"), FailedTests = countif(TestResult == "Fail") by TestGroupName
   ```

5. Query Traffic Analytics data:

   ```kql
   AzureNetworkAnalytics_CL
   | where TimeGenerated > ago(1d)
   | summarize TotalBytes = sum(InboundBytes_d + OutboundBytes_d) by SrcIP_s, DestIP_s
   | top 10 by TotalBytes
   ```

6. Save useful queries for future use

#### Task 10: Configure Alerting

1. In Log Analytics workspace, create an alert:
   - Go to **Alerts** > **+ New alert rule**
   - Scope: Your Log Analytics workspace
   - Condition: Custom log search
   - Query:

     ```kql
     NWConnectionMonitorTestResult
     | where TestResult == "Fail"
     | summarize FailureCount = count() by TestGroupName
     | where FailureCount > 5
     ```

   - Threshold: Greater than 0
2. Configure action group:
   - Create new action group
   - Add email notification
   - Add SMS (optional)
3. Create alert rule:
   - Name: `Network-Connection-Failures`
   - Severity: Warning
   - Evaluation frequency: 5 minutes
4. Click **Create alert rule**

**Key Takeaways:**

- Network Watcher provides comprehensive network diagnostic tools
- Connection Monitor continuously tests network connectivity
- Traffic Analytics provides AI-powered insights into network traffic
- Network Performance Monitor tracks latency, packet loss, and connectivity
- Log Analytics enables custom queries and correlation
- Alerts proactively notify of network issues
- Geo-map views help identify cross-region traffic patterns

**Troubleshooting:**

- **Issue:** Connection Monitor showing no data
  - **Solution:** Verify Network Watcher Agent is installed on VMs; check that VMs are running; ensure firewall/NSG allows test traffic

- **Issue:** Traffic Analytics showing no data
  - **Solution:** Wait 10-20 minutes for data processing; verify NSG flow logs are enabled; check storage account is accessible

### Cleanup

1. Delete Connection Monitor tests
2. Disable Traffic Analytics
3. Delete Network Performance Monitor configurations
4. Delete Log Analytics workspace (optional, as it contains historical data)
5. Delete the resource group "az700-monitoring-lab"

---

## Lab 10: Azure Bastion & Just-In-Time VM Access

### Objective

Implement secure VM access using Azure Bastion and Just-In-Time (JIT) access policies

**Estimated Duration:** 40 minutes

**Prerequisites:**

- Azure subscription with Contributor role
- Existing VNet with VMs (from previous labs or create new)
- Microsoft Defender for Cloud enabled (for JIT)

### Step-by-Step Instructions

#### Task 1: Prepare Virtual Network for Bastion

1. Navigate to your existing VNet (e.g., `vnet-multitier` from Lab 1)
2. Go to **Subnets** (under Settings)
3. Click **+ Subnet**
4. Configure AzureBastionSubnet:
   - Name: `AzureBastionSubnet` (MUST be exact name)
   - Address range: 10.0.255.0/26 (minimum /27, recommended /26)
   - Leave other settings as default
5. Click **Save**

#### Task 2: Create Azure Bastion Resource

1. Navigate to **Bastions** in Azure Portal
2. Click **Create**
3. Configure:
   - Resource Group: Select existing (e.g., az700-network-lab)
   - Name: `bastion-lab`
   - Region: Same as VNet
   - Tier: Standard (for additional features) or Basic
   - Virtual network: Select your VNet
   - Subnet: AzureBastionSubnet (auto-populated)
   - Public IP: Create new `pip-bastion`
4. Click **Review + create**, then **Create**
5. Wait for deployment (5-10 minutes)

#### Task 3: Connect to VM Using Bastion

1. Navigate to one of your VMs in the VNet
2. Click **Connect** > **Bastion**
3. If prompted, allow pop-ups for this site
4. Enter credentials:
   - Username: Your VM username
   - Password: Your VM password
   - Or use SSH key (for Linux VMs)
5. Click **Connect**
6. A new browser tab opens with RDP/SSH session
7. You're now connected without exposing RDP/SSH ports to the internet

#### Task 4: Configure Bastion Features (Standard Tier)

If you deployed Standard tier Bastion:

1. Navigate to your Bastion resource
2. Go to **Configuration** (under Settings)
3. Enable additional features:
   - **Native client support**: Connect using local RDP/SSH client
   - **IP-based connection**: Connect to VMs using private IP (not just by name)
   - **Shareable link**: Generate time-limited access links for users
   - **File transfer**: Upload/download files during session (Windows only)
4. Click **Apply**

#### Task 5: Enable Microsoft Defender for Cloud

1. Navigate to **Microsoft Defender for Cloud**
2. Go to **Environment settings**
3. Select your subscription
4. Enable Defender plans:
   - Servers: On (for JIT access)
   - Storage: Optional
   - Databases: Optional
5. Click **Save**
6. Wait a few minutes for Defender to initialize

#### Task 6: Configure Just-In-Time VM Access

1. In Microsoft Defender for Cloud, go to **Workload protections**
2. Click **Just-in-time VM access**
3. Select the **Not Configured** tab
4. Select VMs to protect:
   - Choose your VMs (e.g., web and app tier VMs)
   - Click **Enable JIT on X VMs**
5. Configure JIT policy:
   - Port 22 (SSH):
     - Action: Allow
     - Max request time: 3 hours
     - Allowed source IPs: Per request (users specify their IP)
   - Port 3389 (RDP):
     - Action: Allow
     - Max request time: 3 hours
     - Allowed source IPs: Per request
   - Port 5985 (PowerShell Remoting):
     - Action: Deny (or Allow with restrictions)
6. Click **Save**

#### Task 7: Request JIT Access

1. Go back to **Just-in-time VM access**
2. Select the **Configured** tab
3. Select a VM you want to access
4. Click **Request access**
5. Configure access request:
   - Port: 3389 (RDP) or 22 (SSH)
   - Time range: Select duration (e.g., 1 hour)
   - My IP: Azure auto-detects your current public IP
   - Or specify custom IP range
6. Click **Open ports**
7. Azure temporarily adds an NSG rule allowing your IP to access the VM
8. Connect to the VM using your preferred RDP/SSH client
9. After the time expires, the NSG rule is automatically removed

#### Task 8: Configure Conditional Access with Bastion (Optional)

If you have Azure AD Premium:

1. Navigate to **Azure Active Directory** > **Security** > **Conditional Access**
2. Click **+ New policy**
3. Configure policy:
   - Name: `Bastion-MFA-Required`
   - Users: Select user group
   - Cloud apps: Microsoft Azure Management
   - Conditions: Device platforms - Any device
   - Grant: Require multi-factor authentication
4. Enable policy: On
5. Click **Create**
6. Now users must complete MFA before connecting via Bastion

#### Task 9: Monitor Bastion Sessions

1. Navigate to your Bastion resource
2. Go to **Monitoring** > **Metrics**
3. Add metrics:
   - **Sessions**: Active sessions count
   - **Total sessions**: All sessions over time
   - **Session duration**: Average session length
4. Go to **Diagnostic settings** (under Monitoring)
5. Click **+ Add diagnostic setting**
6. Configure:
   - Name: `bastion-logs`
   - Log categories: Select all
   - Destination: Send to Log Analytics workspace
7. Click **Save**
8. Query Bastion logs in Log Analytics:

   ```kql
   AzureDiagnostics
   | where ResourceType == "BASTIONHOSTS"
   | summarize SessionCount = count() by UserName, Protocol_s, TargetResourceId
   ```

#### Task 10: Review JIT Access Audit Logs

1. In Microsoft Defender for Cloud, go to **Just-in-time VM access**
2. Select a VM
3. Click **Activity log**
4. Review:
   - Who requested access and when
   - Which ports were opened
   - Request duration
   - IP addresses allowed
5. For detailed querying, use Azure Monitor:

   ```kql
   AzureActivity
   | where OperationNameValue contains "JIT"
   | project TimeGenerated, Caller, OperationName, ResourceGroup, Properties
   ```

**Key Takeaways:**

- Azure Bastion provides secure RDP/SSH access without public IPs
- Bastion eliminates the need for jump boxes or VPNs for admin access
- Just-In-Time access reduces attack surface by limiting port exposure
- JIT automatically opens and closes NSG rules based on time windows
- Bastion integrates with Azure AD for authentication and conditional access
- All Bastion sessions are logged for compliance and auditing
- Standard tier Bastion offers native client support and file transfer

**Troubleshooting:**

- **Issue:** Cannot connect via Bastion
  - **Solution:** Verify AzureBastionSubnet exists with correct name and size (/26 or /27); check VM is in the same VNet; ensure VM is running

- **Issue:** JIT access request fails
  - **Solution:** Verify Microsoft Defender for Cloud is enabled for servers; check that you have sufficient permissions; ensure NSG allows rule modifications

### Cleanup

1. Disable JIT policies on VMs
2. Delete Azure Bastion resource
3. Delete AzureBastionSubnet (optional)
4. Delete diagnostic settings and logs (optional)
5. Disable Microsoft Defender for Cloud plans (if only used for this lab)

---

## Summary

These ten labs provide comprehensive coverage of Azure Network Engineer competencies:

| Lab | Focus Area | Key Skills |
| --- | --- | --- |
| Lab 1 | VNet Design & Architecture | VNets, Subnets, Peering, Routing, DNS |
| Lab 2 | Hybrid Connectivity | VPN Gateways, Site-to-Site VPN, Route Tables |
| Lab 3 | ExpressRoute | Circuits, Peering, BGP, Route Filters |
| Lab 4 | Load Balancing | Application Gateway, Path-based Routing, Health Probes |
| Lab 5 | Security & Monitoring | Firewall, NSGs, Network Watcher, Flow Logs |
| Lab 6 | DNS Management | Public DNS, Private DNS, Auto-registration, Hybrid DNS |
| Lab 7 | Advanced Security | NSGs, ASGs, Rule Management, Segmentation |
| Lab 8 | Global Delivery | Front Door, CDN, WAF, Global Load Balancing |
| Lab 9 | Performance Monitoring | Connection Monitor, NPM, Traffic Analytics |
| Lab 10 | Secure Access | Azure Bastion, JIT Access, Secure Administration |

**Total Lab Time:** ~445 minutes (7.5 hours)

---

## Additional Resources

- [AZ-700 Exam Skills](https://learn.microsoft.com/en-us/certifications/exams/az-700/)
- [Azure Network Engineer Learning Path](https://learn.microsoft.com/en-us/training/paths/azure-network-engineer-associate/)
- [Virtual Network Documentation](https://learn.microsoft.com/en-us/azure/virtual-network/)
- [Azure Firewall Documentation](https://learn.microsoft.com/en-us/azure/firewall/)
- [Network Watcher Documentation](https://learn.microsoft.com/en-us/azure/network-watcher/)
- [ExpressRoute Documentation](https://learn.microsoft.com/en-us/azure/expressroute/)
- [Application Gateway Documentation](https://learn.microsoft.com/en-us/azure/application-gateway/)
- [Azure Front Door Documentation](https://learn.microsoft.com/en-us/azure/frontdoor/)
- [Azure DNS Documentation](https://learn.microsoft.com/en-us/azure/dns/)
- [Azure Bastion Documentation](https://learn.microsoft.com/en-us/azure/bastion/)

---

**Last Updated:** February 1, 2026

**Related:** [← Back to Student Resources](/README.md) | [AZ-700 Practice Test](../az700-practice-test.md) | [All Labs](../labs/)

