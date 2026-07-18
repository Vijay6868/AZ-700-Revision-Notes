# AZ-700 Revision Notes: Connect Devices to Networks with Point-to-Site VPN Connections

### 1. Overview of Point-to-Site (P2S) VPN
* **Definition:** A [Point-to-Site (P2S) VPN gateway](https://learn.microsoft.com/en-us/azure/vpn-gateway/point-to-site-about) connection allows you to establish a secure, encrypted connection to an Azure Virtual Network (VNet) from an individual client computer.
* **Initiation:** The connection is always explicitly started from the client computer.
* **Primary Use Cases:** 
  * Telecommuters working from home, a conference, or a remote location.
  * An efficient alternative to a Site-to-Site (S2S) VPN when only a few individual clients need connection to a VNet.

---

### 2. Supported Point-to-Site Protocols
Azure P2S VPN supports three core protocols, each with distinct platform compatibilities:

* **OpenVPN® Protocol:** An SSL/TLS-based VPN protocol. Because most firewalls leave TCP port 443 open outbound for standard web traffic, OpenVPN can easily penetrate strict firewalls. 
  * *Supported platforms:* Android, iOS (11.0+), Windows, Linux, and Mac (macOS 10.13+).
* **Secure Socket Tunneling Protocol (SSTP):** A proprietary TLS-based VPN protocol. Like OpenVPN, it uses TCP port 443 outbound to successfully traverse firewalls.
  * *Supported platforms:* Strictly Windows devices only (Windows 7 and later).
* **IKEv2 VPN:** A standards-based IPsec VPN solution.
  * *Supported platforms:* Mac devices (macOS 10.11+) and standard native clients.

---

### 3. P2S Authentication Methods
Users must be authenticated before Azure will accept a incoming P2S VPN connection. The two most common architectures are:

#### Native Microsoft Entra ID Authentication
* Users log in using their organizational Microsoft Entra ID cloud credentials.
* **Requirements:** Supported only with the OpenVPN protocol on Windows and requires the installation of the official Azure VPN Client.
* **Benefit:** Allows administrators to enforce advanced identity protections like conditional access and multifactor authentication (MFA).

#### Active Directory Domain Services (AD DS) Authentication
* Users connect using their traditional organization domain credentials.
* **Requirements:** Requires a RADIUS server (either deployed on-premises or within the Azure VNet) that integrates with the domain directory. 
* **Routing Caveat:** The Azure VPN Gateway must have a clear line of communication to the RADIUS server. If the server is located on-premises, a separate Site-to-Site (S2S) VPN connection is required between Azure and the office to route the authentication traffic.
