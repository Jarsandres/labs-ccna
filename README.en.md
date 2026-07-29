# 🌐 CCNA Networking & Infrastructure Portfolio

[🇬🇧 Read in English](./README.en.md) | [🇪🇸 Versión en Español](./README.md)

Welcome to my technical networking portfolio. This repository documents a structured collection of practical labs, network architectures, and real device configurations developed during my preparation and certification for **Cisco CCNA (200-301)**, simulating corporate design, switching, routing, and security environments.

---

## 🛠️ Demonstrated Technical Skills

* **Layer 2 Switching:** VLAN segmentation (802.1Q), Spanning Tree Protocol (STP / PVST+), Link Aggregation with EtherChannel (LACP), and access layer hardening with Port-Security.
* **Layer 3 Routing:** Multi-layer switching with SVIs (Cisco 3560), L3 routed interfaces (`/30`), Router-on-a-Stick, and dynamic routing with OSPFv2 (Single area).
* **Security & Egress (Layer 4 & WAN):** Extended Access Control Lists (Named ACLs), NAT/PAT Overload address translation, DHCP Relay, and secure SSHv2 administration.

---

## 📂 Projects & Laboratories

| Project | Primary Focus | Key Technologies | Status | Link |
| :--- | :--- | :--- | :--- | :--- |
| **Project 01: Multisite Corporate** | Multisite Hub-and-Spoke corporate network | OSPFv2, VLAN Trunking, ACLs, PPP, RoaS | ✅ Completed | [View Project](./project-01-multisite-corporate) |
| **Project 02: Secure Corporate Network** | High availability and LAN security | LACP, PVST+, DHCP Relay, Port Security, SSHv2 | ✅ Completed | [View Project](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP) |
| **Project 03: Enterprise Multi-Layer Network** | L3 Switch SVI, LACP, NAT/PAT, and ACL | SVI (Switch 3560), EtherChannel LACP, NAT/PAT, Extended ACL, DMZ | ✅ Completed | [View Project](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL) |

---

## 🗂️ Repository Structure

* [project-01-multisite-corporate/](./project-01-multisite-corporate): Hub-and-Spoke enterprise network with perimeter security for Data Center.
  * [configs/](./project-01-multisite-corporate/configs): Backup `startup-config` files.
  * [Topology.png](./project-01-multisite-corporate/Topology.png): Infrastructure logical diagram.
* [project-02-Secure Inter-VLAN Routing Architecture with LACP, PVST+ and DHCP/](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP): Redundant corporate network with L2 load balancing and access hardening.
  * [configs/](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP/configs): Backup `startup-config` files.
  * [Topology.png](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP/Topology.png): Network logical diagram.
* [project-03-Enterprise Multi-Layer Switching Architecture with SVI, LACP, NAT and ACL/](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL): Multi-layer network with L3 Switch, EtherChannel LACP, NAT/PAT, and extended ACL in DMZ.
  * [configs/](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL/configs): Backup `startup-config` files.
  * [Topology.png](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL/Topology.png): Official Packet Tracer topology screenshot.

---

*(Note: This repository is continuously updated as I build and validate new practical networking scenarios).*
