# AZ-700 Revision Notes: Designing and Implementing Azure VPN Gateway

### 1. Overview & Core Infrastructure
* **Purpose:** Azure [VPN Gateway](https://learn.microsoft.com/en-us/training/modules/design-implement-hybrid-networking/2-design-implement-vpn-gateway) sends encrypted traffic between an Azure Virtual Network (VNet) and on-premises locations over the public Internet, or between multiple Azure VNets over the private Microsoft backbone network.
* **Underlying Architecture:** A virtual network gateway is made up of two or more specialized virtual machines deployed into a dedicated subnet called the `GatewaySubnet`. These VMs are fully managed by Azure, meaning they require no manual administrative attention.
* **Bandwidth Sharing:** If you configure multiple connections to the same gateway, all active VPN tunnels share the overall bandwidth allocated to that specific gateway SKU.

### 2. Pre-Deployment Planning Factors
When planning a gateway deployment, you must evaluate the following metrics and constraints:
* **Throughput:** Total required speed measured in Mbps or Gbps.
* **Backbone:** Deciding whether traffic moves over the public Internet (VPN) or a private connection (ExpressRoute).
* **IP Requirements:** Availability of a public static IP address.
* **Compatibility:** Ensuring the on-premises physical VPN appliance matches Azure requirements.
* **Architecture:** Deciding between a multi-client link (Point-to-Site) or a network-to-network connection (Site-to-Site).
* **Gateway Details:** Selecting the appropriate VPN Gateway Type and performance SKU.

---

### 3. VPN Gateway Types Comparison
When creating a virtual network gateway, you must specify a VPN type. **This choice cannot be changed once the gateway is created**.

| Feature / Metric | Policy-Based Gateways | Route-Based Gateways |
| :--- | :--- | :--- |
| **Legacy Name** | Previously called static routing gateways. | Previously called dynamic routing gateways. |
| **Routing Protocol** | Encrypts and routes packets through IPsec tunnels strictly based on defined IPsec policies (traffic selectors/access lists). | Uses standard routing tables or IP forwarding rules to direct packets into corresponding tunnel interfaces. |
| **Tunnel Limit** | Supports only **one** tunnel. | Supports multiple concurrent tunnels. |
| **SKU Restrictions** | Only works with IKEv1 protocols and is restricted to the **Basic Gateway SKU**. | Works with modern SKUs, supports dynamic routing protocols (like BGP), and handles advanced scenarios. |
| **Primary Use Case** | Limited strictly to Site-to-Site connections. | Standard choice for almost all modern VPN gateways, including Point-to-Site and inter-VNet routing. |

---

### 4. High Availability (HA) Options
Azure provides two primary high availability configurations to minimize connectivity downtime:

#### Active-Standby (Default Configuration)
* **How it works:** Deploys two gateway instances—one active and one standby. The standby instance remains idle until the active instance encounters a disruption.
* **Downtime & Disruption:** Failover causes a brief service disruption. 
    * For planned maintenance, connectivity is restored within seconds.
    * For unplanned infrastructure interruptions, restoration takes a few minutes.
    * Point-to-Site (P2S) client connections will drop and must manually reconnect.

#### Active-Active Configuration
* **How it works:** Both instances of the virtual network gateway are deployed in an active state simultaneously. Both instances establish independent, unique VPN tunnels to your physical on-premises VPN device.
* **Traffic Flow:** Traffic leaving your Azure VNet is load-balanced and routed through both tunnels at the same time. 
* **Resiliency:** If one instance or tunnel suffers an outage, Azure automatically and instantly routes all traffic through the remaining active tunnel, providing seamless failover without user impact.