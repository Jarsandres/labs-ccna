# Portafolio de Redes CCNA (Cisco Certified Network Associate)

Bienvenido/a a mi portafolio de redes. Este repositorio está diseñado con el objetivo de recopilar y documentar una colección de laboratorios prácticos, topologías y configuraciones de dispositivos realizadas durante y después de mi preparación para la certificación **Cisco CCNA 200-301**, simulando entornos reales de diseño, configuración e implementación.

---

## 🛠️ Competencias Técnicas Demostradas

En este repositorio se documentan implementaciones en las siguientes áreas tecnológicas:

* **Conmutación en Capa 2 (Switching):** Segmentación mediante VLANs, enlaces troncales manuales (802.1Q), optimización y prevención de bucles mediante Spanning Tree Protocol (STP/RSTP) y seguridad de puertos (Port Security).
* **Enrutamiento en Capa 3 (Routing):** Enrutamiento Inter-VLAN (Router-on-a-Stick y SVI), enrutamiento estático y enrutamiento dinámico utilizando OSPFv2 (Área Única y Backbone).
* **Seguridad y Servicios IP (Capa 4 & Perímetro):** Endurecimiento de seguridad en routers y switches, control de acceso mediante ACLs Extendidas (Principio de Mínimo Privilegio), traducción de direcciones (NAT/PAT) y servicios de infraestructura (DHCP, SSH, Syslog).

---

## 📂 Proyectos y Laboratorios

| Nombre del Proyecto | Enfoque Principal | Tecnologías Clave | Estado | Enlace |
| :--- | :--- | :--- | :--- | :--- |
| **Proyecto 01: Multisite Corporate** | Red corporativa multisitio Hub-and-Spoke | OSPFv2, VLAN Trunking, ACLs, PPP, RoaS | ✅ Completado | [Ver Proyecto](./proyecto-01-multisite-corporate) |

*(Nota: Seguiré añadiendo más laboratorios y proyectos a medida que desarrolle nuevas topologías en Packet Tracer, GNS3 y EVE-NG).*

---

## 🗂️ Estructura del Repositorio

* [proyecto-01-multisite-corporate/](./proyecto-01-multisite-corporate): Red empresarial Hub-and-Spoke con seguridad perimetral para Data Center.
  * [configs/](./proyecto-01-multisite-corporate/configs): Respaldos de las configuraciones activas (`startup-config`) de todos los routers y switches.
  * [topologia.png](./proyecto-01-multisite-corporate/topologia.png): Diagrama lógico detallado de la infraestructura de red.


---
*Este repositorio será actualizado de forma continua para reflejar nuevos escenarios y optimizaciones de infraestructura.*
