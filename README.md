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

## Configuración de Infraestructura

### 1. Inicialización del Servidor SIEM
Se confirma la ejecución correcta del Wazuh Manager v4.14.2 tras importar el entorno virtual OVA.
![Manager](./Img/1.Terminal%20de%20Wazuh.png)

### 2. Instalación del Agente
Uso de comandos PowerShell para registrar el endpoint Windows en el sistema de gestión de seguridad centralizado.
![Instalación](./Img/2.PowerShell%20instalando.png)

### 3. Verificación de Conectividad
Confirmación de que el servicio del agente está operando y enlazado al Manager.
![Panel](./Img/3.Panel%20lateral%20de%20Wazuh.png)

### 4. Inventario y Estado Activo
El dashboard de administración muestra el endpoint con estado **"Active"**, permitiendo la recolección de telemetría.
![Inventario](./Img/4.Pestaña%20de%20Inventory.png)

### 5. Clasificación Inicial de Logs
Primeros registros de eventos de seguridad procesados y categorizados por niveles de severidad.
![Ingesta](./Img/5.Ingesta%20de%20Eventos%20de%20Seguridad.png)

## 🕵️ Evaluación de Amenazas

### 6. Ejecución de Actividad Sospechosa
Se ejecutan comandos de enumeración de red y usuarios para validar la capacidad de respuesta del sensor.
![CMD](./Img/6.Simulación%20de%20Actividad%20Sospechosa.png)

### 7. Mapeo con Framework MITRE ATT&CK
Wazuh correlaciona los ataques detectados con tácticas y técnicas estándar de la industria.
![MITRE](./Img/7.Panel%20de%20MITRE%20ATT&CK%20en%20Wazuh.png)

### 10. Detección de Ataque Crítico (Fuerza Bruta)
**Alerta Nivel 10:** El SIEM identifica múltiples fallos de autenticación coordinados en un periodo corto de tiempo.
![Alerta 10](./Img/10.Alerta%20de%20nivel%2010.png)

## Gestión de Vulnerabilidades y refuerzo de seguridad

### 11. Escaneo de Vulnerabilidades (CVE)
Se detectan 22 fallos críticos que exponen la integridad del servidor.
![CVE](./Img/11.Dashboard%20con%2022%20Critical.png)

### 12. Auditoría CIS Benchmark (SCA)
Análisis de cumplimiento de configuración segura, obteniendo un puntaje inicial del 31%.
![SCA](./Img/12.Score%2031%.png)

### 13. Remediación: Política de Bloqueo
Configuración de la directiva de seguridad local para bloquear cuentas tras 5 intentos fallidos, mitigando la fuerza bruta detectada.
![GPO](./Img/13.GPO%20Bloqueo%20de%20cuenta.png)

### 14. Actualización Crítica del Sistema
Cierre del ciclo de seguridad mediante la aplicación de parches acumulativos en Windows Server.
![Update](./Img/14.Windows%20Update.png)

