# 🧪 AZ-700 Hands-On Labs

**Azure Network Engineer Associate Practical Experience**

---

## Table of Contents

1. [Lab 1: Virtual Networks & Subnets](#lab-1-virtual-networks--subnets)
2. [Lab 2: Site-to-Site VPN & Hybrid Connectivity](#lab-2-site-to-site-vpn--hybrid-connectivity)
3. [Lab 3: Azure ExpressRoute Configuration](#lab-3-azure-expressroute-configuration)
4. [Lab 4: Load Balancing & Application Gateway](#lab-4-load-balancing--application-gateway)
5. [Lab 5: Network Security & Monitoring](#lab-5-network-security--monitoring)

---

## Lab 1: Virtual Networks & Subnets

**Objective:** Design and implement a multi-tier virtual network architecture with proper segmentation and routing

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

**Objective:** Configure a site-to-site VPN connection to simulate on-premises connectivity

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

**Objective:** Understand and configure Azure ExpressRoute for dedicated hybrid connectivity

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

**Objective:** Configure application-layer load balancing with URL-based routing

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

**Objective:** Implement comprehensive network security and monitoring with Azure Firewall and Network Watcher

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

## Summary

These five labs cover the core Azure Network Engineer competencies:

| Lab | Focus Area | Key Skills |
|-----|-----------|-----------|
| Lab 1 | VNet Design & Architecture | VNets, Subnets, Peering, Routing, DNS |
| Lab 2 | Hybrid Connectivity | VPN Gateways, Site-to-Site VPN, Route Tables |
| Lab 3 | ExpressRoute | Circuits, Peering, BGP, Route Filters |
| Lab 4 | Load Balancing | Application Gateway, Path-based Routing, Health Probes |
| Lab 5 | Security & Monitoring | Firewall, NSGs, Network Watcher, Flow Logs |

**Total Lab Time:** ~250 minutes (4+ hours)

---

## Additional Resources

- [AZ-700 Exam Skills](https://learn.microsoft.com/en-us/certifications/exams/az-700/)
- [Azure Network Engineer Learning Path](https://learn.microsoft.com/en-us/training/paths/azure-network-engineer-associate/)
- [Virtual Network Documentation](https://learn.microsoft.com/en-us/azure/virtual-network/)
- [Azure Firewall Documentation](https://learn.microsoft.com/en-us/azure/firewall/)
- [Network Watcher Documentation](https://learn.microsoft.com/en-us/azure/network-watcher/)
- [ExpressRoute Documentation](https://learn.microsoft.com/en-us/azure/expressroute/)
- [Application Gateway Documentation](https://learn.microsoft.com/en-us/azure/application-gateway/)

---

**Last Updated:** February 1, 2026

**Related:** [← Back to Student Resources](/README.md) | [AZ-700 Practice Test](../az700-practice-test.md) | [All Labs](../labs/)
