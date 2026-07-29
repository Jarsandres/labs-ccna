# 🌐 Portafolio de Redes & Infraestructura CCNA

[🇬🇧 Read in English](./README.en.md) | [🇪🇸 Versión en Español](./README.md)

Bienvenido/a a mi portafolio técnico de redes. Este repositorio documenta una colección estructurada de laboratorios prácticos, arquitecturas de red y configuraciones reales desarrolladas durante mi preparación y certificación **Cisco CCNA (200-301)**, simulando entornos corporativos de diseño, conmutación, enrutamiento y seguridad.

---

## 🛠️ Competencias Técnicas Demostradas

* **Conmutación en Capa 2 (Switching):** Segmentación VLAN (802.1Q), Spanning Tree Protocol (STP / PVST+), agregación de enlaces con EtherChannel (LACP) y hardening de acceso con Port-Security.
* **Enrutamiento en Capa 3 (Routing):** Switching Multicapa con SVIs (Cisco 3560), interfaces enrutadas L3 (`/30`), Router-on-a-Stick y enrutamiento dinámico con OSPFv2 (Área única).
* **Seguridad & Perímetro (Capa 4 & WAN):** Listas de Control de Acceso Extendidas (ACLs Nombradas), traducción de direcciones NAT/PAT Overload, DHCP Relay y administración segura por SSHv2.

---

## 📂 Proyectos y Laboratorios

| Proyecto | Enfoque Principal | Tecnologías Clave | Estado | Enlace |
| :--- | :--- | :--- | :--- | :--- |
| **Proyecto 01: Multisite Corporate** | Red corporativa multisitio Hub-and-Spoke | OSPFv2, VLAN Trunking, ACLs, PPP, RoaS | ✅ Completado | [Ver Proyecto](./project-01-multisite-corporate) |
| **Proyecto 02: Red Corporativa Segura** | Alta disponibilidad y seguridad en LAN | LACP, PVST+, DHCP Relay, Port Security, SSHv2 | ✅ Completado | [Ver Proyecto](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP) |
| **Proyecto 03: Red Multicapa Empresarial** | Switching L3 SVI, LACP, NAT/PAT y ACL | SVI (Switch 3560), EtherChannel LACP, NAT/PAT, Extended ACL, DMZ | ✅ Completado | [Ver Proyecto](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL) |

---

## 🗂️ Estructura del Repositorio

* [project-01-multisite-corporate/](./project-01-multisite-corporate): Red empresarial Hub-and-Spoke con seguridad perimetral para Data Center.
  * [configs/](./project-01-multisite-corporate/configs): Respaldos de configuración `startup-config`.
  * [Topology.png](./project-01-multisite-corporate/Topology.png): Diagrama lógico de infraestructura.
* [project-02-Secure Inter-VLAN Routing Architecture with LACP, PVST+ and DHCP/](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP): Red corporativa redundante con balanceo L2 y hardening de acceso.
  * [configs/](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP/configs): Respaldos de configuración `startup-config`.
  * [Topology.png](./project-02-Secure%20Inter-VLAN%20Routing%20Architecture%20with%20LACP,%20PVST+%20and%20DHCP/Topology.png): Diagrama lógico de la red.
* [project-03-Enterprise Multi-Layer Switching Architecture with SVI, LACP, NAT and ACL/](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL): Red multicapa con Switch L3, EtherChannel LACP, NAT/PAT y ACL extendida en DMZ.
  * [configs/](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL/configs): Respaldos de configuración `startup-config`.
  * [Topology.png](./project-03-Enterprise%20Multi-Layer%20Switching%20Architecture%20with%20SVI,%20LACP,%20NAT%20and%20ACL/Topology.png): Captura oficial de la topología en Packet Tracer.

---

*(Nota: Este repositorio se actualiza continuamente a medida que desarrollo y valido nuevos escenarios prácticos de redes).*
