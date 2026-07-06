# CCNA Network Portfolio (Cisco Certified Network Associate)

[🇪🇸 Versión en Español](./README.md) | [🇬🇧 English Version](./README.en.md)

Welcome to my networking portfolio. This repository is designed to compile and document a collection of practical labs, topologies, and device configurations performed during and after my preparation for the **Cisco CCNA 200-301** certification, simulating real-world design, configuration, and deployment environments.

---

## 🛠️ Demonstrated Technical Competencies

Implementations in the following technological areas are documented in this repository:

* **Layer 2 Switching:** Segmentation via VLANs, manual trunk links (802.1Q), loop prevention and optimization using Spanning Tree Protocol (STP/RSTP), and port security (Port Security).
* **Layer 3 Routing:** Inter-VLAN Routing (Router-on-a-Stick and SVI), static routing, and dynamic routing using OSPFv2 (Single-Area and Backbone).
* **Security & IP Services (Layer 4 & Perimeter):** Device hardening on routers and switches, access control using Extended ACLs (Principle of Least Privilege), Network Address Translation (NAT/PAT), and infrastructure services (DHCP, SSH, Syslog).

---

## 📂 Projects and Labs

| Project Name | Main Focus | Key Technologies | Status | Link |
| :--- | :--- | :--- | :--- | :--- |
| **Project 01: Multisite Corporate** | Hub-and-Spoke multisite enterprise network | OSPFv2, VLAN Trunking, ACLs, PPP, RoaS | ✅ Completed | [View Project](./project-01-multisite-corporate/README.en.md) |
| **Project 02: Secure and Resilient Corporate Network** | High availability and security in LAN | LACP, PVST+, DHCP Relay, Port Security, SSHv2 | ✅ Completed | [View Project](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP/README.en.md) |

*(Note: I will continue to add more labs and projects as I develop new topologies in Packet Tracer, GNS3, and EVE-NG).*

---

## 🗂️ Repository Structure

* [project-01-multisite-corporate/](./project-01-multisite-corporate): Enterprise Hub-and-Spoke network with perimeter security for the Data Center.
  * [configs/](./project-01-multisite-corporate/configs): Backups of running configurations (`startup-config`) for all routers and switches.
  * [Topology.png](./project-01-multisite-corporate/Topology.png): Logical diagram of the headquarters and branch offices network infrastructure.
* [project-02-Secure Inter-VLAN Routing Architecture with LACP, PVST+ and DHCP/](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP): Redundant corporate network with Layer 2 load balancing and access hardening.
  * [configs/](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP/configs): Backups of running configurations (`startup-config`) for routers and switches.
  * [Topology.png](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP/Topology.png): Logical diagram of the hierarchical LAN model with double redundant links.

---
*This repository will be continuously updated to reflect new scenarios and infrastructure optimizations.*
