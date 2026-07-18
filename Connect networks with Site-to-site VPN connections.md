# AZ-700 Revision Notes: Connect Networks with Site-to-Site VPN Connections

### 1. Overview of Site-to-Site (S2S) VPN
* **Definition:** A [Site-to-Site (S2S) VPN gateway](https://learn.microsoft.com/en-us/training/modules/design-implement-hybrid-networking/4-connect-networks-site-to-site-vpn-connections) allows you to establish a secure, encrypted connection to your Azure Virtual Network (VNet) from another virtual network or a physical on-premises network.
* **Connection Type:** It uses the public internet to establish a secure **IPsec VPN tunnel** between the two network locations.

### 2. Core Architectural Components
An Azure VPN gateway deployment consists of the following foundational elements working together:
* **Virtual Network Gateway:** The Azure infrastructure responsible for routing encrypted traffic.
* **Local Network Gateway:** The object in Azure that defines the configuration and public IP of your on-premises VPN device.
* **Connection:** The resource that establishes and maintains the actual IPsec tunnel parameters between gateways.
* **Gateway Subnet:** The dedicated subnet (`GatewaySubnet`) within the Azure VNet where the gateway infrastructure resides.
* **Internal Load Balancer:** Positioned at the front end within Azure to route incoming cloud traffic to the correct cloud-based resources or applications.

---

### 3. Benefits & Constraints

#### Benefits
* **Simplicity:** Streamlines network configuration and continuous management.
* **Security:** Ensures complete encryption of data and traffic passing between the on-premises gateway and the Azure gateway.
* **Scalability:** Easily accommodates changing and growing future network architecture requirements.

#### Constraints & Limitations
* **Public Internet Dependent:** The architecture relies entirely on your existing internet connection to bridge the two gateways.
* **Performance Risks:** Reusing existing internet infrastructure can introduce bandwidth constraints, which may cause latency or performance issues during high-volume periods.

---

### 4. Check Your Knowledge

#### Question: What is a site-to-site VPN Gateway connection?
* **Correct Answer:** A site-to-site VPN Gateway connection securely connects two networks.
* **Key Concept:** Unlike Point-to-Site (which links individual client computers to a network), an S2S gateway connects entire physical or virtual networks to one another.
