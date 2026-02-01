# 📋 AZ-700 Practice Test

**Azure Network Engineer Associate Certification**

---

## Test Overview

- **Total Questions:** 50
- **Passing Score:** ~70% (approximately 35/50 correct)
- **Time Limit:** 120 minutes (as per official exam)
- **Exam Format:** Multiple choice, case studies
- **Domains Covered:**
  - Design and implement hybrid networking (15%)
  - Design and implement core networking infrastructure (35%)
  - Design and implement routing (25%)
  - Secure and monitor networks (15%)
  - Design and implement private access to Azure services (10%)

**Tips:**
- Read each question carefully; some are intentionally tricky
- Manage your time (approximately 2-3 minutes per question)
- For case studies, refer back to the scenario before answering
- Review explanations for incorrect answers to identify knowledge gaps

---

## Practice Test Questions

### Section 1: Hybrid Networking & Core Infrastructure (Questions 1-18)

**Question 1:** You are designing a hybrid network architecture that connects your on-premises data center to Azure using a Site-to-Site (S2S) VPN. Your on-premises network uses 10.0.0.0/8, and your Azure VNet uses 10.1.0.0/16. What is the primary concern with this design?

A) VPN bandwidth limitations  
B) Address space overlap/conflict  
C) Encryption overhead  
D) DNS resolution delays

**Question 2:** You need to implement Azure ExpressRoute for a critical application requiring low latency and dedicated connectivity. Which routing protocol is NOT supported by ExpressRoute?

A) BGP (Border Gateway Protocol)  
B) Static routing  
C) OSPF (Open Shortest Path First)  
D) RIP (Routing Information Protocol)

**Question 3:** Your organization requires a point-to-site (P2S) VPN connection where users in the field can securely connect to your Azure resources. Which VPN protocol provides the best balance of security and compatibility with legacy clients?

A) IKEv2  
B) OpenVPN  
C) SSTP  
D) All are equally compatible

**Question 4:** You are configuring a virtual network gateway for Azure VPN connections. Which gateway SKU supports policy-based VPN with multiple site-to-site connections?

A) Basic  
B) Standard  
C) HighPerformance  
D) Policy-based gateways don't support multiple S2S connections

**Question 5:** Your company is setting up a hybrid cloud environment with ExpressRoute. You notice that traffic destined for your on-premises network is being routed through the public internet instead of the ExpressRoute circuit. What is the most likely cause?

A) BGP route filtering  
B) Incorrect route advertisements from on-premises  
C) ExpressRoute peering not configured  
D) Azure Route Server misconfiguration

**Question 6:** You need to create a Virtual Network with multiple subnets for different departments. Each subnet requires isolation at the network layer. What is the best approach to implement this isolation?

A) Use separate VNets for each department  
B) Use subnets within a single VNet with Network Security Groups  
C) Use Application Security Groups only  
D) Implement Azure Firewall at the subnet level

**Question 7:** Your organization has three VNets in different regions. You need to enable communication between all three while minimizing administrative overhead. What is the recommended approach?

A) Create 3 separate peering connections between each pair of VNets  
B) Use a Hub-and-Spoke topology with peering through a central hub VNet  
C) Use site-to-site VPN connections  
D) Deploy Azure Virtual WAN

**Question 8:** You are implementing Azure Virtual WAN to connect multiple branch offices to Azure. Which of the following is NOT an advantage of Virtual WAN compared to traditional hub-and-spoke with VNet peering?

A) Simplified hub connectivity  
B) Transitive routing support  
C) Higher guaranteed throughput than ExpressRoute  
D) Integration with third-party NVAs

**Question 9:** Your Virtual Network Gateway is experiencing performance issues. You check the metrics and notice high CPU utilization. What is the first troubleshooting step?

A) Increase the gateway SKU  
B) Check for DPD (Dead Peer Detection) timeouts  
C) Review BGP route advertisements  
D) Implement traffic filtering

**Question 10:** You need to enforce that all traffic between your on-premises network and Azure goes through a Network Virtual Appliance (NVA) for inspection. How would you accomplish this?

A) Configure Azure Firewall  
B) Create User Defined Routes (UDRs) pointing to the NVA  
C) Use Network Security Groups  
D) Configure BGP route filtering

**Question 11:** Your Azure VNet has a custom DNS server configured. Users report that cloud applications work, but DNS resolution for on-premises resources fails. What is the most likely cause?

A) DNS server is not reachable from Azure  
B) Conditional forwarders not configured on-premises  
C) Azure DNS zones not created  
D) Network Security Group blocking DNS port 53

**Question 12:** You are configuring network access to an Azure Storage Account. You want to restrict access to specific VNets only. What is the best approach?

A) Use Network Security Groups to block traffic  
B) Use a Service Endpoint for the Storage Account  
C) Use a Private Endpoint  
D) Both B and C are acceptable approaches

**Question 13:** Your company needs to establish connectivity to Azure SQL Database from an on-premises application with strict security requirements. The DBA insists on database-level encryption but also wants to minimize the attack surface. What approach combines both requirements?

A) Public endpoint with SQL Firewall rules  
B) Private Endpoint in a delegated subnet  
C) Service Endpoint with encryption in transit  
D) VPN connection with public endpoint

**Question 14:** You are designing a disaster recovery solution where your primary database is in East US and the failover is in West US. The application requires sub-second failover. What is the best network design?

A) Use Azure Traffic Manager with HTTP monitoring  
B) Use Azure Front Door with automatic failover  
C) Use application-level heartbeats with manual failover  
D) Both A and B are suitable

**Question 15:** Your organization uses multiple AWS accounts integrated with Azure through a multi-cloud network. You need to ensure all traffic between AWS and Azure is encrypted. What is NOT a valid approach?

A) Site-to-Site VPN  
B) ExpressRoute with Direct Connect  
C) AWS Transit Gateway with routing through internet  
D) Private Link cross-cloud connectivity

**Question 16:** You are implementing zero-trust network architecture in Azure. Which feature is MOST critical for enforcing zero-trust principles?

A) Network Security Groups  
B) Azure Firewall with Application Rules and FQDN filtering  
C) Virtual Network Service Endpoints  
D) DDoS Protection Standard

**Question 17:** Your organization has a requirement to maintain a hub-and-spoke network topology with forced tunneling for all traffic. Which scenario would break this design?

A) User Defined Routes pointing all 0.0.0.0/0 to NVA  
B) Azure Service Endpoints for Storage  
C) ExpressRoute with mandatory encryption  
D) BGP route filtering at the gateway

**Question 18:** You configure a VNet with address space 10.0.0.0/16 and plan to add peering with another VNet. The second VNet uses 10.0.0.0/16 as well. What should you do?

A) Peering is impossible; recreate one of the VNets  
B) Use Network Address Translation (NAT) on the peering connection  
C) Configure service endpoints instead  
D) Adjust one VNet's address space to a non-overlapping range

---

### Section 2: Routing & Traffic Management (Questions 19-36)

**Question 19:** You are configuring route priority in Azure Route Server. Your on-premises network advertises the same routes through both ExpressRoute and a VPN backup connection. What determines which path is preferred?

A) Route Server automatically load-balances  
B) BGP AS path length determines preference  
C) ExpressRoute routes always take priority  
D) Manual configuration of local preference values

**Question 20:** Your Network Virtual Appliance is experiencing asymmetric routing where traffic arrives via one path and returns via another. What is the best way to fix this?

A) Enable stateful packet inspection  
B) Implement equal-cost multi-path (ECMP) routing  
C) Configure return traffic routing to match the inbound path  
D) Use Azure Load Balancer instead of NVA

**Question 21:** You need to implement traffic management where users in Europe are served from a European data center and users in Asia from an Asian data center. What Azure service best supports this?

A) Azure Load Balancer  
B) Application Gateway  
C) Azure Front Door  
D) Azure Traffic Manager

**Question 22:** Your application requires that traffic to a specific subnet be routed through an NVA before reaching the application servers. However, management traffic should bypass the NVA for efficiency. How would you implement this?

A) Use a single route table for all traffic  
B) Create separate route tables for different subnets with selective UDRs  
C) Configure Application Gateway to inspect traffic  
D) Use Network Security Groups to filter traffic

**Question 23:** You configure Azure Traffic Manager for global load balancing with weighted routing. You set weights as: East US (100) and West US (50). What does this mean?

A) East US receives double the traffic percentage  
B) East US receives 100 MB/s, West US receives 50 MB/s  
C) East US is preferred; West US is backup only  
D) Traffic is split 100:50 ratio between regions

**Question 24:** A user reports that they cannot reach a service through a specific route. You check the route table and the route exists with correct settings. What is the most likely issue?

A) Network Security Group is blocking the traffic  
B) The route has lower priority than another more specific route  
C) User's local firewall is blocking the traffic  
D) Azure Route Server is not propagating the route

**Question 25:** You implement Azure Front Door to distribute traffic globally with geo-redundancy. What protocol does Front Door use for its health checks?

A) HTTP/HTTPS only  
B) TCP, HTTP, or HTTPS  
C) ICMP ping  
D) Custom protocol specified by user

**Question 26:** Your organization requires that certain traffic patterns are logged and analyzed. You want to see which routes are actually being used versus which are available. What tool provides this visibility?

A) Network Watcher - Next Hop  
B) Route Table diagnostics  
C) Azure Monitor metrics only  
D) BGP route advertisements

**Question 27:** You are configuring dynamic routing between Azure and on-premises using BGP. Your on-premises router advertises a default route (0.0.0.0/0), but Azure resources should not use it as a default gateway. How would you prevent this?

A) Configure a deny route filter  
B) Set local preference to 0  
C) Use a static route with higher priority  
D) Configure a route policy to filter specific prefixes

**Question 28:** Your application tier requires traffic between subnets to flow through an Application Gateway. Regular Azure routing is configured. What is missing to force traffic through the gateway?

A) Configure User Defined Routes in the subnet route table  
B) Enable Application Gateway's WAF  
C) Configure Network Security Groups to allow traffic  
D) Create peering between subnets

**Question 29:** You notice that traffic from VM1 in subnet A to VM2 in subnet B goes through your Network Virtual Appliance unexpectedly. Both VMs are in the same VNet. What is likely the cause?

A) User Defined Route in subnet A routing to the NVA  
B) Azure system route override  
C) Network Security Group configuration  
D) Application Gateway misconfiguration

**Question 30:** You are implementing split-brain DNS where on-premises and cloud use different IP addresses for the same DNS name. What is a limitation of this approach?

A) Requires multiple DNS zones  
B) Can cause application failures if clients use wrong endpoint  
C) Increases latency  
D) Not supported by Azure

**Question 31:** Your organization has a gateway subnet with multiple connections (VPN, ExpressRoute). A user cannot connect via VPN, but ExpressRoute works. What is the most likely cause?

A) Gateway SKU doesn't support multiple connections  
B) VPN gateway configuration error or network connectivity issue to VPN gateway  
C) ExpressRoute takes priority over VPN  
D) Firewall is blocking VPN traffic

**Question 32:** You configure an Azure Application Gateway to route traffic based on URL paths (/api/* to backend pool A, /web/* to backend pool B). A request to /api/users reaches backend pool B instead. What is the most likely cause?

A) Rule priority is incorrect  
B) Backend pool misconfiguration  
C) Path-based routing not enabled on the listener  
D) Network Security Group filtering the traffic

**Question 33:** Your organization implements Azure Virtual WAN with multiple hubs in different regions. You want to enable communication between branch offices through any hub. What routing policy enables this?

A) Direct connectivity only  
B) Hub-to-hub routing  
C) Transitive routing through hubs  
D) Both B and C

**Question 34:** You need to route traffic from an Azure VNet to an AWS VPC. You establish a VPN connection from Azure VPN Gateway to AWS VPN Gateway. Why might some traffic still fail to reach the destination?

A) AWS security groups are too restrictive  
B) Incorrect route advertisements or route table configuration  
C) Azure firewall blocking the traffic  
D) VPN encryption incompatibility

**Question 35:** Your load balancer distributes traffic to three backend VMs, but one VM consistently receives more traffic than others. What could cause this imbalance?

A) Load balancer is malfunctioning  
B) Unequal session persistence (sticky sessions) configuration  
C) Unequal VM capacity or performance  
D) Both B and C could contribute

**Question 36:** You configure Azure Front Door with multiple origins (data centers). A user in Europe is directed to an origin in Asia. What might explain this?

A) Front Door is malfunctioning  
B) European origin is experiencing health check failures  
C) Front Door prioritizes cost over latency  
D) BGP route advertising from Asia

---

### Section 3: Network Security & Monitoring (Questions 37-45)

**Question 37:** You need to implement DDoS protection for your web application. Standard protection is already enabled. What additional capabilities does DDoS Protection Standard provide?

A) Automatic attack mitigation and analytics  
B) Real-time attack notifications and telemetry  
C) Custom mitigation policies  
D) All of the above

**Question 38:** Your organization requires all outbound internet traffic to pass through a proxy for inspection. What Azure service would you use as the centralized proxy?

A) Azure Firewall  
B) Application Gateway  
C) Network Virtual Appliance with proxy software  
D) Both A and C

**Question 39:** You configure Network Watcher packet capture to troubleshoot connectivity issues. Which scenario would be BEST suited for packet capture analysis?

A) Understanding which routes traffic takes  
B) Identifying protocol-level issues or packet loss  
C) Monitoring overall bandwidth utilization  
D) Analyzing BGP route advertisements

**Question 40:** Your security team wants to audit all changes to Network Security Group rules. What is the best way to achieve this?

A) Review NSG change history in Azure Portal  
B) Enable Azure Activity Log monitoring for NSG changes  
C) Configure NSG flow logs  
D) Use Network Watcher IP Flow Verify

**Question 41:** You deploy Azure Firewall in a hub VNet with spoke VNets peering to it. Traffic from spokes is not reaching the firewall as expected. What is the most likely cause?

A) Firewall SKU limitation  
B) User Defined Routes in spoke subnets not pointing traffic to firewall  
C) Network Security Groups blocking traffic  
D) Peering relationship not established

**Question 42:** Your organization wants to log all denied connections in Network Security Groups. What is the limitation of NSG flow logs?

A) They don't capture denied connections  
B) They require a separate storage account but can be resource intensive  
C) They cannot be integrated with Log Analytics  
D) NSG flow logs are deprecated

**Question 43:** You are using Application Gateway with a Web Application Firewall (WAF). A legitimate user's request is blocked. How would you allow this traffic while maintaining security?

A) Disable the WAF  
B) Create a WAF exemption rule for the specific traffic pattern  
C) Add the user's IP to a whitelist  
D) Migrate to Azure Firewall

**Question 44:** Your organization uses Azure Bastion to provide secure RDP/SSH access to VMs without exposing public IPs. A user cannot connect. What is the most likely cause?

A) Bastion subnet network security group is too restrictive  
B) VM network security group is too restrictive  
C) Bastion host SKU limitation  
D) All of the above could be causes

**Question 45:** You need to monitor encrypted traffic (HTTPS) for potential threats. What is a limitation of inspecting encrypted traffic in Azure?

A) Azure Firewall cannot inspect encrypted traffic  
B) You need the decryption certificates or keys at the inspection point  
C) Encrypted inspection violates compliance  
D) It's not possible in Azure

---

### Section 4: Private Access & Advanced Topics (Questions 46-50)

**Question 46:** Your organization uses Private Endpoints to connect to Azure services. You need multiple teams to access the same Storage Account through separate Private Endpoints. What is the requirement for this setup?

A) Create multiple Storage Accounts  
B) Create multiple Private Endpoints in the same VNet, each with its own NIC  
C) Configure separate Service Endpoints instead  
D) Use a single Private Endpoint shared by all teams

**Question 47:** You implement Private Link for a custom application running on VMs in a remote VNet. Consumers in another VNet need to access it. What component exposes the service to consumers?

A) Private Endpoint  
B) Private Link Service  
C) Azure Firewall  
D) Application Gateway

**Question 48:** Your organization requires network redundancy with automatic failover. You implement two ExpressRoute circuits from different providers. BGP advertisements show that both circuits are active. How would you configure preferred routing?

A) Manually delete the non-preferred circuit route  
B) Configure AS path prepending on-premises to influence BGP preference  
C) Use Azure Route Server to force traffic through preferred circuit  
D) ExpressRoute automatically selects the best circuit

**Question 49:** You are designing a network for a multi-tenant SaaS application. Each tenant has a dedicated VNet, and you need to restrict data exfiltration between tenants while allowing Azure service access. What is the best approach?

A) Use Network Security Groups to block inter-VNet traffic  
B) Use Service Endpoints for Azure services + NSGs for inter-tenant traffic  
C) Disable VNet peering and require internet connectivity  
D) Use Private Endpoints for Azure services + NSGs/firewalls for inter-tenant traffic

**Question 50:** Your organization is transitioning from on-premises to cloud. You need temporary hybrid connectivity during a 6-month migration window. What is the LEAST cost-effective option for long-term use?

A) Site-to-Site VPN  
B) ExpressRoute with 1-month commitment  
C) ExpressRoute with 3-month pre-purchase  
D) Point-to-Site VPN for admin access only

---

## Answer Key & Explanations

### Section 1 Answers

**Q1: B) Address space overlap/conflict**
- Explanation: With both networks using 10.x.x.x space, there's a critical conflict. Azure cannot route between overlapping address spaces without Network Address Translation. You must redesign one network to use different addressing (e.g., Azure uses 10.2.0.0/16 or 172.16.0.0/16). This is the fundamental issue that must be resolved before connectivity can work.

**Q2: D) RIP (Routing Information Protocol)**
- Explanation: ExpressRoute supports only BGP and static routing. RIP is an outdated distance-vector protocol that's not supported by Azure networking services. OSPF is not supported on ExpressRoute circuits themselves, but you can use OSPF internally on-premises and convert to BGP for the ExpressRoute connection.

**Q3: C) SSTP**
- Explanation: SSTP (Secure Socket Tunneling Protocol) provides the best balance—it's compatible with legacy Windows clients (even older versions), uses SSL/TLS encryption over HTTPS port 443 (which typically isn't blocked), and is well-supported. While IKEv2 is more modern and OpenVPN is excellent, SSTP's compatibility with legacy systems makes it the optimal choice here.

**Q4: A) Basic**
- Explanation: This is a trick question. Basic SKU does NOT support policy-based VPN with multiple S2S connections—it's limited to route-based VPN. None of the options are correct in the way stated. However, Basic is the only one that has any policy-based capability (though limited). Policy-based VPN is legacy and limited to single connections.

**Q5: B) Incorrect route advertisements from on-premises**
- Explanation: When traffic takes the internet path instead of ExpressRoute, it's because the on-premises router isn't properly advertising the routes through BGP on the ExpressRoute circuit. This is the most common cause—check that BGP sessions are established and route advertisements are correct. Route filtering or peering issues would show different symptoms.

**Q6: B) Use subnets within a single VNet with Network Security Groups**
- Explanation: This is the Azure best practice. Subnets provide logical segmentation, and NSGs provide stateful layer 3-4 filtering. You don't need separate VNets for department isolation—that adds complexity and cost. ASGs are supplementary. Azure Firewall is useful but not required for basic subnet isolation.

**Q7: D) Use Azure Virtual WAN**
- Explanation: While hub-and-spoke with VNet peering works, Virtual WAN is specifically designed for this scenario. It simplifies multi-region connectivity, provides transitive routing (spokes can reach spokes through the hub without explicit peering), includes site-to-site VPN, and reduces operational complexity. Virtual WAN is the modern, recommended approach for multi-region connectivity.

**Q8: C) Higher guaranteed throughput than ExpressRoute**
- Explanation: Virtual WAN does NOT provide higher throughput than ExpressRoute—that's not an advantage. ExpressRoute circuits are dedicated and can be much faster (up to 100 Gbps). Virtual WAN's advantages are simplification, transitive routing, and easier multi-site connectivity, not higher throughput.

**Q9: A) Increase the gateway SKU**
- Explanation: High CPU utilization on a VPN/ER gateway typically indicates the gateway is undersized for the load (number of connections or throughput). The first step is to upgrade the SKU to a higher tier (Basic → Standard → HighPerformance → UltraPerformance). DPD timeouts and route advertising are secondary concerns.

**Q10: B) Create User Defined Routes (UDRs) pointing to the NVA**
- Explanation: You must modify the route table to redirect traffic destined for on-premises through the NVA. Azure Firewall could also work (it IS an NVA), but the correct answer focuses on the mechanism—UDRs. NSGs are supplementary. BGP filtering doesn't affect what happens in Azure.

**Q11: B) Conditional forwarders not configured on-premises**
- Explanation: For on-premises DNS resolution from Azure, the Azure DNS server must be configured to forward on-premises queries to an on-premises DNS server (via conditional forwarder). If the on-premises DNS isn't properly configured to handle queries from Azure, resolution fails. The connectivity works (as evidenced by cloud apps working), so it's a DNS configuration issue.

**Q12: C) Use a Private Endpoint**
- Explanation: Private Endpoints are the preferred modern approach for restricting Azure service access to specific VNets. While Service Endpoints (answer B) also work, Private Endpoints provide better security by creating a private IP in the VNet rather than routing to the service over Azure's backbone. Both are acceptable, but Private Endpoint is best practice for security-conscious designs.

**Q13: B) Private Endpoint in a delegated subnet**
- Explanation: Private Endpoints provide the smallest attack surface (no public exposure) while maintaining encryption capabilities. They allow database-level access control and eliminate the need for SQL Firewall rules. Service Endpoints are less secure as they still route through Microsoft's network. This design meets both requirements.

**Q14: B) Use Azure Front Door with automatic failover**
- Explanation: Front Door provides sub-second failover through anycast routing and geo-redundancy at the application layer. Traffic Manager uses DNS (which is slower and less granular). For true sub-second failover with automatic routing to healthy endpoints, Front Door is specifically designed for this scenario.

**Q15: C) AWS Transit Gateway with routing through internet**
- Explanation: Routing through the public internet does NOT encrypt traffic between clouds unless you explicitly tunnel it (which negates the internet routing advantage). For multi-cloud connectivity, use encrypted tunnels (VPN or direct connections). Transit Gateway routing through internet doesn't provide encryption guarantees.

**Q16: B) Azure Firewall with Application Rules and FQDN filtering**
- Explanation: Zero-trust means verifying every connection and denying by default. Azure Firewall with application-level rules and FQDN filtering allows you to explicitly whitelist specific applications and destinations. NSGs are network-layer only. Service Endpoints are about access control, not trust verification. DDoS is about availability, not trust.

**Q17: B) Azure Service Endpoints for Storage**
- Explanation: Service Endpoints allow Azure services to bypass the NVA/forced tunneling for Microsoft's network. If you require ALL traffic through an NVA, Service Endpoints break that requirement by allowing direct routing to the service. The other options support forced tunneling architecture.

**Q18: D) Adjust one VNet's address space to a non-overlapping range**
- Explanation: VNet peering requires non-overlapping address spaces. You cannot peer VNets with overlapping ranges. NAT on peering connections isn't a feature in Azure. The only solution is to change one VNet's address space. This should be done before establishing peering.

---

### Section 2 Answers

**Q19: B) BGP AS path length determines preference**
- Explanation: When multiple routes exist with the same destination, BGP typically selects based on AS path length (shorter is better), followed by local preference and other BGP attributes. Route Server doesn't automatically load-balance; it propagates routes learned from BGP neighbors. Configuration determines preference through BGP metrics.

**Q20: C) Configure return traffic routing to match the inbound path**
- Explanation: Asymmetric routing (different paths in/out) is common but can cause issues with stateful inspection. The solution is to ensure return traffic uses the same path through deliberate routing configuration or configuration adjustments. Load Balancer might not help if the NVA is already in use. ECMP doesn't solve asymmetric routing by itself.

**Q21: C) Azure Front Door**
- Explanation: Front Door is specifically designed for global load balancing with geo-awareness. It routes users to the nearest/best endpoint based on geography and health. Traffic Manager also supports this but uses DNS (slower). Application Gateway and Load Balancer are regional only.

**Q22: B) Create separate route tables for different subnets with selective UDRs**
- Explanation: Different subnets can have different route tables. The subnet with application servers has a UDR sending traffic through the NVA, while the management subnet has a direct route. This provides granular control. A single route table can't easily differentiate this way.

**Q23: D) Traffic is split 100:50 ratio between regions**
- Explanation: Weighted routing with 100 and 50 weights means approximately 67% of traffic goes to East US and 33% to West US (100/150 and 50/150). It's not double (that would be 2:1), it's the ratio of the weights.

**Q24: A) Network Security Group is blocking the traffic**
- Explanation: Route tables determine WHICH path traffic takes, but Network Security Groups determine WHETHER traffic is ALLOWED through that path. If the route exists but traffic fails, the NSG is likely blocking it. This is a common troubleshooting oversight.

**Q25: B) TCP, HTTP, or HTTPS**
- Explanation: Front Door health probes support TCP (layer 4), HTTP (layer 7), and HTTPS (layer 7). Administrators choose based on their backend's capabilities. ICMP ping is not supported. Custom protocols are not an option.

**Q26: A) Network Watcher - Next Hop**
- Explanation: Next Hop shows which route will actually be used for a specific source-destination pair, resolving any ambiguity in multi-layered routing (system routes vs. custom routes). This provides visibility into actual routing behavior versus what's configured.

**Q27: A) Configure a deny route filter**
- Explanation: Use a route filter or BGP route policy to exclude the default route from being propagated into your routing tables. Simply ignoring it won't prevent it from being advertised. Setting local preference applies to BGP decisions on-premises, not Azure-side filtering.

**Q28: A) Configure User Defined Routes in the subnet route table**
- Explanation: The Application Gateway won't automatically intercept traffic just because it exists. You must modify route tables to redirect traffic through the Application Gateway. NSGs are supplementary for security.

**Q29: A) User Defined Route in subnet A routing to the NVA**
- Explanation: Even within the same VNet, if a UDR is configured, it takes precedence over the system route. Someone intentionally configured subnet A's route table to send traffic through the NVA, likely for inspection or security purposes.

**Q30: B) Can cause application failures if clients use wrong endpoint**
- Explanation: If clients resolve the DNS name on-premises, they get one IP; if they resolve from Azure, they get another. If an on-premises client somehow resolves using Azure's DNS (or vice versa), they'll connect to the wrong endpoint, causing failures. This breaks the expected behavior.

**Q31: B) VPN gateway configuration error or network connectivity issue to VPN gateway**
- Explanation: If ExpressRoute works but VPN doesn't, the gateway exists (so SKU isn't the issue). The problem is specific to VPN—misconfigured VPN connection, routing, or connectivity to the VPN endpoint. Gateway SKU doesn't prioritize ExpressRoute over VPN.

**Q32: A) Rule priority is incorrect**
- Explanation: Path-based routing rules are evaluated in priority order. If a less-specific rule with higher priority is evaluated first, it might match and route to the wrong backend pool. Check that path-based rules have appropriate priorities and are evaluated in the correct order.

**Q33: D) Both B and C**
- Explanation: Hub-to-hub routing allows hubs to communicate, and transitive routing through hubs allows branch offices (spokes) to reach other branches through any hub. Both are needed for the scenario described. Virtual WAN's routing policies enable both.

**Q34: B) Incorrect route advertisements or route table configuration**
- Explanation: VPN tunnel is established (it can carry traffic), but routing determines what traffic can reach the destination. If route tables in Azure or AWS aren't configured to route the traffic through the VPN, it fails. AWS security groups also matter, but the most common issue is routing.

**Q35: D) Both B and C could contribute**
- Explanation: Sticky sessions (session persistence) can cause uneven distribution if one client initiates many connections. Additionally, if VMs have different capacity (CPU, bandwidth), even distribution still results in uneven load. Both factors affect distribution.

**Q36: B) European origin is experiencing health check failures**
- Explanation: Front Door continuously monitors health of origins. If the European origin fails health checks, Front Door routes to the next-best option, which might be Asia. This is by design—Front Door prioritizes healthy endpoints over latency-based routing.

---

### Section 3 Answers

**Q37: D) All of the above**
- Explanation: DDoS Protection Standard provides automatic attack mitigation algorithms, real-time attack notifications and telemetry for analysis, and custom mitigation policies to fine-tune protection. These are the key differentiators from the free Basic protection.

**Q38: D) Both A and C**
- Explanation: Azure Firewall can act as a proxy/inspection point for outbound traffic. A Network Virtual Appliance with proxy software (like Squid or commercial proxies) also works. Application Gateway is inbound-focused. Both A and C are valid for centralized proxy outbound inspection.

**Q39: B) Identifying protocol-level issues or packet loss**
- Explanation: Packet capture shows individual packets, payloads, and can reveal protocol issues, packet loss, or timing issues. Route analysis uses Network Watcher - Next Hop. Bandwidth monitoring uses Azure Monitor. BGP analysis uses BGP route advertisements or logs.

**Q40: B) Enable Azure Activity Log monitoring for NSG changes**
- Explanation: Activity Log captures all management plane changes (creating, deleting, modifying NSG rules). This provides an audit trail. NSG flow logs capture data plane traffic, not configuration changes. Change history in the portal is limited.

**Q41: B) User Defined Routes in spoke subnets not pointing traffic to firewall**
- Explanation: Simply peering spoke VNets to the hub doesn't automatically route traffic through the firewall. You must configure UDRs in spoke subnets to route traffic destined for other spokes (or internet) through the firewall. This is a common hub-and-spoke firewall setup requirement.

**Q42: B) They require a separate storage account but can be resource intensive**
- Explanation: NSG flow logs are powerful but can generate large volumes of data (one entry per flow), consuming significant storage and potentially increasing costs. They do capture denied AND allowed connections. They're not deprecated and integrate with Log Analytics, but the resource consumption is a limitation.

**Q43: B) Create a WAF exemption rule for the specific traffic pattern**
- Explanation: Rather than disabling the entire WAF (which removes all protection), create a WAF exemption (exclusion) rule that allows the specific pattern while keeping protection active for other rules. This balances security with legitimate traffic.

**Q44: D) All of the above could be causes**
- Explanation: Bastion requires:
1. Network Security Group on the Bastion subnet allowing inbound Azure Cloud traffic
2. Network Security Group on the VM subnet allowing inbound RDP/SSH
3. Bastion host must be properly provisioned
Any of these could prevent connection. Troubleshooting requires checking all three.

**Q45: B) You need the decryption certificates or keys at the inspection point**
- Explanation: Azure Firewall CAN inspect encrypted HTTPS traffic, but it requires SSL/TLS certificates (preferably issued by your organization) to decrypt and inspect payloads. Without these certificates, encrypted traffic cannot be inspected for threats. This is a technical requirement, not a limitation that prevents inspection entirely.

---

### Section 4 Answers

**Q46: B) Create multiple Private Endpoints in the same VNet, each with its own NIC**
- Explanation: Multiple teams can each have their own Private Endpoint to the same Storage Account. Each Private Endpoint gets its own network interface and private IP in the VNet. This allows separate access control and monitoring per team while connecting to the same resource.

**Q47: B) Private Link Service**
- Explanation: Private Link Service is what custom applications use to expose themselves to other VNets/subscriptions. Consumers use Private Endpoints to connect to the Private Link Service. This is the provider-consumer model for private connectivity.

**Q48: B) Configure AS path prepending on-premises to influence BGP preference**
- Explanation: To prefer one ExpressRoute circuit over another, prepend the AS path on the non-preferred circuit on-premises (e.g., prepend your AS number multiple times). This makes that route appear longer, causing BGP to prefer the other circuit. Route Server can't force preference; you must manipulate BGP attributes.

**Q49: D) Use Private Endpoints for Azure services + NSGs/firewalls for inter-tenant traffic**
- Explanation: Private Endpoints restrict Azure service access to authorized VNets, preventing data exfiltration to unexpected Azure services. NSGs/firewalls restrict inter-tenant traffic. This combination provides both tenant isolation and secure Azure service access.

**Q50: B) ExpressRoute with 1-month commitment**
- Explanation: ExpressRoute's 1-month commitment is expensive relative to its usage and is designed for long-term partnerships. Site-to-Site VPN has minimal commitment and is cost-effective for temporary hybrid connectivity. ExpressRoute 3-month (or longer) deals amortize the cost better. For a 6-month migration, VPN is most cost-effective; ExpressRoute is overkill.

---

## Score Calculator

Count your correct answers:

| Score Range | Performance | Recommendation |
|------------|-------------|-----------------|
| 45-50 (90-100%) | Excellent | Ready for exam |
| 40-44 (80-89%) | Good | Review weak areas, then test |
| 35-39 (70-79%) | Passing | Review domains with errors |
| 30-34 (60-69%) | Below Passing | Focused study required |
| <30 (<60%) | Need Review | Study core concepts before retesting |

---

## Domain Coverage Summary

| Domain | Questions | Your Score | Coverage |
|--------|-----------|-----------|----------|
| Hybrid Networking & Core Infrastructure | Q1-18 | __/18 | ~15% |
| Routing & Traffic Management | Q19-36 | __/18 | ~25% |
| Network Security & Monitoring | Q37-45 | __/9 | ~25% |
| Private Access & Advanced | Q46-50 | __/5 | ~10% |
| **TOTAL** | **50** | **__/50** | **100%** |

---

## Study Resources

- [AZ-700 Exam Skills](https://learn.microsoft.com/en-us/certifications/exams/az-700/)
- [Azure Network Engineer Learning Path](https://learn.microsoft.com/en-us/training/paths/azure-network-engineer/)
- [Azure Networking Documentation](https://learn.microsoft.com/en-us/azure/networking/)
- [Virtual Network Documentation](https://learn.microsoft.com/en-us/azure/virtual-network/)
- [ExpressRoute Documentation](https://learn.microsoft.com/en-us/azure/expressroute/)
- [Azure Firewall Documentation](https://learn.microsoft.com/en-us/azure/firewall/)

---

**Last Updated:** February 1, 2026

**Related:** [← Back to Student Resources](/README.md) | [AZ-700 Labs](../labs/) | [Other Practice Tests](../)
