# AZ-700 Revision Notes: Connect Remote Resources by Using Azure Virtual WANs

### 1. Overview of Azure Virtual WAN
* **Definition:** [Azure Virtual WAN](https://learn.microsoft.com/en-us/azure/virtual-wan/virtual-wan-about) is a comprehensive networking service that aggregates multiple networking, security, and routing functionalities into a single unified operational interface.
* **Core Advantage:** It allows distributed global organizations to easily manage regional connectivity and utilize the high-speed Microsoft backbone network for data routing.

### 2. Core Architectural Elements
To build an operational, end-to-end virtual WAN deployment, you create the following resources:
* **Virtual WAN:** The top-level resource that represents a virtual overlay of your network environment. It acts as a collection container for multiple hubs. *Note: Virtual WANs are isolated from one another and cannot share a common hub.*
* **Hub:** A virtual hub is a Microsoft-managed virtual network that contains various service endpoints to enable transitive connectivity.
* **Hub Virtual Network Connection:** The connection resource used to seamlessly bind a standard virtual network (spoke) to the managed virtual hub. A single VNet can only connect to one virtual hub.
* **Hub-to-Hub Connection:** In a multi-hub deployment, all virtual hubs are automatically interconnected to enable global routing.
* **Hub Route Table:** The configuration file where you can create and apply multiple virtual hub routes to dictate traffic flow.
* **Site (Optional):** A configuration resource used exclusively for establishing Site-to-Site (S2S) VPN links.

---

### 3. Choosing a Virtual WAN SKU
Virtual WAN is deployed in either a Basic or Standard SKU, which determines the features available within the managed hubs:

| Virtual WAN Type | Hub Type | Available Configurations & Features |
| :--- | :--- | :--- |
| **Basic** | Basic | Restricted to **Site-to-Site VPN connections only**. |
| **Standard** | Standard | Supports all connectivity methods: **ExpressRoute**, **User VPN (P2S)**, and **Site-to-Site (S2S) VPN**. <br><br> Enables inter-hub and VNet-to-VNet transiting directly through the hub. <br><br> Integrates advanced services like **Azure Firewall** and Network Virtual Appliances (NVAs). |

---

### 4. Check Your Knowledge

#### Question: What is an Azure Virtual WAN?
* **Correct Answer:** Azure Virtual WAN is a collection of connectivity resources like VPNs, which enables organizations to use the Microsoft backbone.
* **Key Concept:** Rather than just a loose collection of peered networks, it acts as a centrally managed, security-isolated overlay that provides unified transit across Microsoft's global infrastructure.
