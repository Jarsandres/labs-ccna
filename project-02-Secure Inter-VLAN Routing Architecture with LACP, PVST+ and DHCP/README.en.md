# Project 02: Secure Inter-VLAN Routing Architecture with LACP, PVST+, and DHCP

[🇪🇸 Versión en Español](./README.md) | [🇬🇧 English Version](./README.en.md)

## 1. Project Summary

This document details the design, implementation, and security hardening of a high-availability corporate LAN infrastructure for a medium-sized company. The solution covers Layer 2 link aggregation and redundancy to address-allocation automation and access-level perimeter security on user ports.

The topology and reference configurations align with the practical and theoretical requirements of the **Cisco CCNA 200-301** certification.

---

## 2. Topology Architecture & WAN Design

The network is structured under Cisco's classic hierarchical design model, divided into the **Distribution** layer (conformance, switching, and redundant loop control) and the **Access** layer (endpoint connectivity and security policy enforcement).

### Logical Network Diagram

![Network Topology](Topology.png)

### WAN Design Note
* **Cable-Modem Bridge Mode:** The `Cable-Modem-0` device acts transparently as a Layer 2 bridge. This allows the `GigabitEthernet0/1` interface of the edge router `R1` to negotiate the public IP address directly with the ISP router, eliminating double-NAT overhead and ensuring clean perimeter routing.

---

## 3. Addressing Scheme & VLANs

The network has been segmented into different VLANs to reduce broadcast domains, optimize performance, and apply specific traffic control policies:

| VLAN ID | Name | Subnet | Gateway IP | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **VLAN 10** | Users | `192.168.10.0/24` | `192.168.10.1` | End clients (Operations VLAN) |
| **VLAN 20** | Servers | `192.168.20.0/24` | `192.168.20.1` | Internal services and corporate resources |
| **VLAN 99** | Management | `192.168.99.0/24` | `192.168.99.1` | SVI for Switches (Out-of-band management) |
| **WAN** | Link-to-ISP | `203.0.113.0/30` | `203.0.113.1` (ISP) | Outbound public Internet link |

### Device Management IPs (SVI VLAN 99)
- **DSW1:** `192.168.99.11`
- **DSW2:** `192.168.99.12`
- **ASW1:** `192.168.99.21`
- **ASW2:** `192.168.99.22`

---

## 4. Key Technologies Implemented

### A. EtherChannel (LACP)
Logical link aggregation using the industry-standard **LACP** (*Link Aggregation Control Protocol* - `active` mode) between `DSW1` and `DSW2`. It groups physical interfaces `Fa0/23` and `Fa0/24` into a single logical trunk link called `Port-Channel 1` to double the available trunk bandwidth and provide active/passive tolerance against physical cable disconnection.

### B. PVST+ (Per-VLAN Spanning Tree)
Deterministic Layer 2 loop mitigation using Spanning Tree per VLAN. The setup is:
- `DSW1` as the **primary Root Bridge** for VLANs 10 and 99.
- `DSW2` as the **primary Root Bridge** for VLAN 20.
This setup balances STP traffic loads (*STP Load Balancing*), avoiding idle link bandwidth wastage.

### C. DHCP Relay Agent (`ip helper-address`)
Configured on Router `R1` to forward broadcast *DHCP Discover* requests originating from VLAN 10 clients as unicast packets directly to the central DHCP server `Server-Internal` (`192.168.20.100`) on VLAN 20. This allows centralized corporate IP addressing.

### D. Port-Security (Access-level Security)
Perimeter hardening applied to the `Fa0/10` access interfaces on switches `ASW1` and `ASW2`:
- Access limit restricted to a **maximum of 1 MAC address** per port.
- Persistent dynamic MAC learning using **MAC Address Sticky**.
- Violation action set to **Shutdown**. If a device with an unregistered MAC address is connected, the port immediately shuts down and goes into *err-disable* status.

### E. Spanning-Tree PortFast and BPDU Guard
- **PortFast:** Enabled on user ports to bypass traditional STP listening and learning states, reducing convergence time from 30 to 0 seconds upon device connection.
- **BPDU Guard:** Safeguards the topology by shutting down the port immediately if any BPDU frame is received (preventing unauthorized switches from being plugged into access ports).

### F. Secure Remote Management (SSHv2)
- Cleartext management protocols like Telnet are fully disabled.
- Strong RSA crypto key generation.
- Exclusive use of **SSHv2** for secure management access across all devices.

---

## 5. Essential Configuration Commands

### R1 (Subinterfaces Trunking & DHCP Relay)
```ios
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 ip helper-address 192.168.20.100
!
interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
!
interface GigabitEthernet0/0.99
 encapsulation dot1Q 99 native
 ip address 192.168.99.1 255.255.255.0
```

### DSW1 (EtherChannel & STP Primary)
```ios
interface range FastEthernet 0/23 - 24
 channel-protocol lacp
 channel-group 1 mode active
!
interface Port-Channel 1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,99
!
spanning-tree mode pvst
spanning-tree vlan 10,99 root primary
spanning-tree vlan 20 root secondary
```

### ASW1 (Port-Security & Access Hardening)
```ios
interface FastEthernet0/10
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 switchport port-security mac-address sticky
 spanning-tree portfast
 spanning-tree bpduguard enable
```

---

## 6. Verification and Diagnostics

### EtherChannel Summary on DSW1
```text
DSW1# show etherchannel summary
Group  Port-channel  Protocol    Ports
------+-------------+-----------+-----------------------------------------------
1      Po1(SU)         LACP      Fa0/23(P)   Fa0/24(P)   
```
* **Validated Status:** Port-channel `Po1` is active in `SU` status (S: Layer2, U: In use) and member ports are in `P` (In Port-Channel) status, confirming correct LACP negotiation.

### Spanning Tree on DSW1 (VLAN 10)
```text
DSW1# show spanning-tree vlan 10
VLAN0010
  Spanning tree enabled protocol ieee
  Root ID    Priority    24586
             Address     00D0.FF0E.AA01
             This bridge is the root
```
* **Validated Status:** Confirmed Root Bridge role for VLAN 10 on DSW1, verifying deterministic Layer 2 packet routing.

### IP Address Verification on PC-User
```text
PC-User> ipconfig /all
Physical Address................: 00E0.F794.7C28
IP Address......................: 192.168.10.11
Subnet Mask.....................: 255.255.255.0
Default Gateway.................: 192.168.10.1
DHCP Server.....................: 192.168.20.100
```
* **Validated Status:** IP address `192.168.10.11` is dynamically assigned and the gateway points to `R1`'s subinterface, validating the DHCP Relay functionality.

### Port Security on ASW1
```text
ASW1# show port-security interface fa0/10
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Sticky MAC Addresses       : 1
Last Source Address:Vlan    : 00E0.F794.7C28:10
Security Violation Count   : 0
```
* **Validated Status:** Port operating in secure status (`Secure-up`), with the host's MAC registered as `Sticky` and zero violations.

---

## 📁 Repository Configuration Files

You can inspect the running configuration backups (`startup-config`) for each device:

* [R1 Config](./configs/R1_startup-config.txt)
* [DSW1 Config](./configs/DSW1_startup-config.txt)
* [DSW2 Config](./configs/DSW2_startup-config.txt)
* [ASW1 Config](./configs/ASW1_startup-config.txt)
* [ASW2 Config](./configs/ASW2_startup-config.txt)

---
*This lab demonstrates the practical application of robust, redundant, and highly secure design standards under the Cisco CCNA certification guidelines.*
