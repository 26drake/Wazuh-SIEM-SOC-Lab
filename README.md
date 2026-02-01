# Wazuh-SIEM-SOC-Lab
Implementación de SIEM, detección de amenazas y Hardening en Windows Server 2022.
Laboratorio de Seguridad: Wazuh SIEM

Este proyecto demuestra el monitoreo y endurecimiento (hardening) de un servidor Windows.

## Herramientas Utilizadas
| Herramienta | Función |
| :--- | :--- |
| **Wazuh** | Manager SIEM y análisis de eventos |
| **Windows Server 2022** | Endpoint objetivo (Objetivo de Ataque Controlado) |
| **VirtualBox** | Entorno de virtualización |


Para este proyecto, se diseñó un entorno virtualizado utilizando **Oracle VirtualBox**, optimizando los recursos para garantizar un monitoreo fluido

* **Wazuh Manager (Servidor de Seguridad):**
    * **SO:** Ubuntu 22.04 (Desplegado mediante OVA v4.14.2).
    * **Recursos:** 2 vCPU, 4 GB RAM, 20 GB SSD.
    * **Función:** Nodo central de análisis, decodificación de logs y generación de alertas.
* **Windows Server 2022 (Endpoint Monitoreado):**
    * **SO:** Standard Evaluation (Build 20348).
    * **Recursos:** 2 CPU, 4GB RAM, 50GB SSD.
    * **Función:** Servidor objetivo para auditoría de seguridad y detección de intrusiones.
* **Configuración de Red:**
    * Ambas máquinas residen en una red privada virtual (NAT/Red Interna).
    * **Comunicación:** Flujo de datos habilitado a través de los puertos **1514 (UDP/TCP)** para telemetría y **1515 (TCP)** para el registro de agentes.
