# Project 03: Multi-Layer Network with L3 Switch (SVI), EtherChannel LACP, NAT/PAT & Extended ACL

[🇬🇧 Read in English](./README.en.md) | [🇪🇸 Versión en Español](./README.md)

---

## 📋 Project Summary

This project implements a corporate network using a **Layer 3 Switch (Cisco 3560)** for Inter-VLAN routing via **Switch Virtual Interfaces (SVIs)**.

The main goal is to connect different departments (**Sales** and **Engineering**) with a server zone (**DMZ**), ensuring high availability using **EtherChannel LACP**, Internet access using **NAT/PAT Overload** on a border router (`R1`), and network security via **extended ACLs** and **Port Security**.

---

## 📦 Packet Tracer File (.pkt)

* 📥 **[Download Packet Tracer Topology (.pkt)](./project-03-enterprise-multilayer-switching.pkt)** — *Download the complete file ready to open in Cisco Packet Tracer 8.x / 9.x.*

---

## 📐 Network Topology & WAN Design

The infrastructure uses a hierarchical design with a main **Layer 3 Switch** (`SW-Core`) and an **Access Switch** (`SW1`), connected to a border router (`R1`) for Internet access.

### Logical Network Diagram

![Network Topology](Topology.png)

### Architecture Notes

* **Layer 3 Switching (SVI):** Inter-VLAN routing across VLANs 10, 20, and 30 is handled directly by `SW-Core` using `ip routing`, achieving faster wire-speed routing and offloading the router.
* **`/30` Transit Link:** The connection between `SW-Core` and router `R1` uses a Layer 3 routed interface (`GigabitEthernet0/1` with `no switchport`) under the `10.0.0.0/30` subnet.

---

## 📊 Addressing & VLAN Scheme

The network is divided into independent subnets to isolate department and service traffic:

| VLAN / Link | Name | Subnet | Gateway IP / SVI | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **VLAN 10** | Ventas | `192.168.10.0/24` | `192.168.10.1` | Sales Department Workstations |
| **VLAN 20** | Ingenieria | `192.168.20.0/24` | `192.168.20.1` | Engineering Department Workstations |
| **VLAN 30** | DMZ | `192.168.30.0/24` | `192.168.30.1` | Server Zone (`Server-DMZ` `192.168.30.10`) |
| **L3 Transit** | SW-Core ↔ R1 | `10.0.0.0/30` | `10.0.0.1` (R1) / `10.0.0.2` (SW-Core) | Internal link to border router |
| **Public WAN** | ISP Link | `200.100.50.0/24` | `200.100.50.254` (R1 WAN) | Internet Egress (ISP Server `200.100.50.1`) |

---

## ⚙️ Key Technologies Implemented

### A. Inter-VLAN Routing with SVIs (L3 Switch)
Configured `ip routing` on the `SW-Core` switch to handle traffic between VLANs 10, 20, and 30 through their respective SVIs (`Vlan10`, `Vlan20`, and `Vlan30`).

### B. Dynamic EtherChannel (LACP 802.3ad)
Bundled physical ports `Fa0/23` and `Fa0/24` into a single logical trunk link (**`Port-Channel 1`**) between `SW1` and `SW-Core` using LACP in `active` mode, doubling bandwidth to 200 Mbps and adding redundancy.

### C. Demilitarized Zone (DMZ / VLAN 30)
Created an isolated server subnet (`Server-DMZ` `192.168.30.10/24`) for corporate services, preventing unauthorized direct access from user devices.

### D. Internet Access with NAT/PAT Overload
Configured NAT on router `R1` (`ip nat inside` / `outside` and `NAT-ACL`) to translate internal private IP addresses (`192.168.0.0/16`) to a single public IP, enabling secure outbound internet access to `Server-ISP`.

### E. Security via Extended Named Access Control List (`DMZ-SECURITY-POLICY`)
Applied an extended ACL on `interface Vlan10` inbound (`in`):
* **Web Traffic to DMZ:** Allows HTTP (`port 80`) and HTTPS (`port 443`) to `Server-DMZ`.
* **Inter-VLAN Block:** Blocks direct IP traffic from Sales (`192.168.10.0/24`) to Engineering (`192.168.20.0/24`).
* **Internet Access:** Allows remaining traffic (`permit ip any any`) to access the Internet through NAT.

### F. Access Layer Port-Security
Hardening applied on access ports of `SW1` (`Fa0/1` and `Fa0/2`):
* Maximum limit of **1 MAC address** per port.
* MAC learning set to **`sticky`**.
* Violation action set to **`restrict`** to block unauthorized devices.

---

## 💻 Essential Configuration Commands

### SW-Core (Multi-Layer Cisco 3560 Switch)

```ios
! Enable L3 Routing and VLANs
ip routing
vlan 10
 name Ventas
vlan 20
 name Ingenieria
vlan 30
 name DMZ

! Configure LACP Port-Channel
interface range FastEthernet0/23 - 24
 switchport mode trunk
 channel-group 1 mode active
!
interface Port-channel 1
 switchport mode trunk

! Routed Port to R1
interface GigabitEthernet0/1
 no switchport
 ip address 10.0.0.2 255.255.255.252
 no shutdown

! SVIs and ACL Binding
interface Vlan10
 ip address 192.168.10.1 255.255.255.0
 ip access-group DMZ-SECURITY-POLICY in
 no shutdown

interface Vlan20
 ip address 192.168.20.1 255.255.255.0
 no shutdown

interface Vlan30
 ip address 192.168.30.1 255.255.255.0
 no shutdown

! Extended DMZ ACL and Default Route
ip access-list extended DMZ-SECURITY-POLICY
 permit tcp 192.168.0.0 0.0.255.255 host 192.168.30.10 eq www
 permit tcp 192.168.0.0 0.0.255.255 host 192.168.30.10 eq 443
 deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
 permit ip any any

ip route 0.0.0.0 0.0.0.0 10.0.0.1
```

### R1 (Border Router & NAT/PAT)

```ios
! LAN and WAN Interfaces
interface GigabitEthernet0/0
 ip address 10.0.0.1 255.255.255.252
 ip nat inside
 no shutdown

interface GigabitEthernet0/1
 ip address 200.100.50.254 255.255.255.0
 ip nat outside
 no shutdown

! NAT Overload Setup (PAT)
ip access-list standard NAT-ACL
 permit 192.168.0.0 0.0.255.255

ip nat inside source list NAT-ACL interface GigabitEthernet0/1 overload
ip route 192.168.0.0 255.255.0.0 10.0.0.2
```

---

## 🔍 Verification and Diagnostics

### A. EtherChannel LACP State on SW-Core

```text
SW-Core# show etherchannel summary
Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Fa0/23(P)   Fa0/24(P)   
```
* **Verification:** Channel `Po1` is active (`SU`) and both physical ports are bundled (`P`).

### B. Extended Access List State on SW-Core

```text
SW-CORE# show access-lists
Extended IP access list DMZ-SECURITY-POLICY
    10 permit tcp 192.168.0.0 0.0.255.255 host 192.168.30.10 eq www
    20 permit tcp 192.168.0.0 0.0.255.255 host 192.168.30.10 eq 443
    30 deny ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
    40 permit ip any any
```
* **Verification:** ACL is ordered properly and bound to `interface Vlan10`.

### C. Connectivity Tests (Ping)

* **Isolation between Sales and Engineering (`PC-Ventas1` ➔ `PC-Ingenieria1` `192.168.20.11`):**
  ```text
  PC-Ventas1> ping 192.168.20.11
  Request timed out. (100% Loss - Correctly blocked by ACL)
  ```
* **WAN Internet Access (`PC-Ventas1` ➔ `Server-ISP` `200.100.50.1`):**
  ```text
  PC-Ventas1> ping 200.100.50.1
  Reply from 200.100.50.1: bytes=32 time<1ms TTL=126 (0% Loss - Translated via NAT/PAT)
  ```

---

## 📁 Repository Configuration Files

Startup configuration files (`startup-config`) extracted from each device:

* [SW-Core Config](./configs/SW-Core-config.txt)
* [SW1 Config](./configs/SW1-config.txt)
* [R1 Config](./configs/R1-config.txt)
