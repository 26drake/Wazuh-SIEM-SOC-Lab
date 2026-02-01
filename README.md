# Wazuh-SIEM-SOC-Lab
## Implementación de SIEM, detección de amenazas y refuerzo de seguridad en Windows Server 2022.


Este repositorio recoge el diseño,despliegue y validación de un laboratorio de ciberseguridad, centrado en detectar amenazas, monitorear de forma activa y fortalecer un servidor Windows Server 2022 con Wazuh como plataforma SIEM.Aquí,el laboratorio reproduce un entorno empresarial realista.Permite analizar eventos de seguridad,relacionarlos con el framework MITRE ATT&CK,evaluar la postura de seguridad del sistema y aplicar medidas correctivas siguiendo buenas prácticas.

## Objetivos del Laboratorio

* **Configurar un SIEM funcional con Wazuh Manager**
* **Integrar y monitorear un endpoint Windows Server 2022**  
* **Detecta actividades sospechosas y ataques de fuerza bruta**  
* **Clasifica los eventos de seguridad usando MITRE ATT&CK**  
* **Evalúa vulnerabilidades y revisa si las configuraciones cumplen con los estándares CIS**  
* **Aplicar refuerzo de seguridad y comprueba el impacto real de esas medidas en la seguridad**

## Herramientas Utilizadas

| Herramienta | Función |
| :--- | :--- |
| **Wazuh** | Manager SIEM y análisis de eventos |
| **Windows Server 2022** | Endpoint objetivo (Objetivo de Ataque Controlado) |
| **VirtualBox** | Entorno de virtualización |


Esta topología fue seleccionada para simular un entorno aislado y controlado, similar a infraestructuras internas corporativas.

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
Desplegamos el servidor Wazuh sin problemas y lo configuramos como nodo central de monitoreo. Quedó listo enseguida para recibir telemetría de los endpoints.
![Manager](./img/1.Terminal%20de%20Wazuh.png)

### 2. Instalación del Agente
Instalamos el agente Wazuh usando PowerShell, asegurando que se conectara correctamente con el manager. Así, empezamos a recolectar los logs del sistema sin contratiempos.
![Instalación](./img/2.PowerShell%20instalando.png)

### 3. Verificación de Conectividad
Desde la consola de Wazuh, comprobamos que el agente y el manager se comunican bien, validando que los eventos llegan como deben.
![Panel](./img/3.Panel%20lateral%20de%20Wazuh.png)

### 4. Inventario y Estado Activo
El sistema Windows se registró bajo el identificador `WIN-9KDIN1VGVST`. Con esto, activamos los módulos de inventario, monitoreo y análisis.
![Inventario](./img/4.Pestaña%20de%20Inventory.png)

### 5. Clasificación Inicial de Logs
El dashboard de Wazuh empezó a procesar eventos de autenticación, procesos y toda la actividad del sistema operativo en tiempo real.
![Ingesta](./img/5.Ingesta%20de%20Eventos%20de%20Seguridad.png)

## Evaluación de Amenazas

### 6. Ejecución de Actividad Sospechosa
Lanzamos varios comandos de reconocimiento desde CMD para generar eventos anómalos y poner a prueba las capacidades de detección del SIEM. Estos eventos incluyeron ejecuciones de comandos y accesos que ayudan a evaluar técnicas de reconocimiento reales.
![CMD](./img/6.Simulación%20de%20Actividad%20Sospechosa.png)

### 7. Mapeo con Framework MITRE ATT&CK
Wazuh clasificó automáticamente los eventos detectados según las tácticas y técnicas del framework MITRE ATT&CK, lo que facilitó el análisis del comportamiento del atacante.
![MITRE](./img/7.Panel%20de%20MITRE%20ATT%26CK%20en%20Wazuh..png)

### 8. Detección de Ataque Crítico (Fuerza Bruta)
**Alerta Nivel 10:** Wazuh lanzó una alerta crítica de nivel 10 por varios intentos fallidos de inicio de sesión en poco tiempo. Este patrón indica un ataque de fuerza bruta dirigido a cuentas locales y exige respuesta inmediata.
![Alerta 10](./img/10.Alerta%20de%20nivel%2010.png)

## Gestión de Vulnerabilidades y refuerzo de seguridad

### 9. Escaneo de Vulnerabilidades (CVE)
Encontramos 22 vulnerabilidades críticas en el sistema. Esto nos ayudó a definir prioridades claras para la mitigación.
![CVE](./img/11.Dashboard%20con%2022%20Critical.png)

### 10. Auditoría CIS Benchmark (SCA)
El análisis de configuración segura con CIS Benchmarks mostró un puntaje inicial del 31%. El resultado deja ver fallas importantes en la configuración del sistema.
![SCA](./img/12.Score%2031%25.png)

### 11. Remediación: Política de Bloqueo
Aplicamos una política que bloquea la cuenta después de cinco intentos fallidos. Así, reducimos el riesgo de ataques de fuerza bruta.
![GPO](./img/13.GPO%20Bloqueo%20de%20cuenta.png)

### 12. Actualización Crítica del Sistema
También completamos un ciclo de actualización del sistema con Windows Update, lo que permitió mitigar vulnerabilidades conocidas.
![Update](./img/14.Windows%20Update.png)

## Análisis y Resultados

* **Wazuh detectó sin problema los intentos de autenticación sospechosos.**
* **El mapeo MITRE ayudó a entender claramente cómo actúa el atacante.**
* **El refuerzo de seguridad que aplicamos elevó de verdad la seguridad del sistema.** 
* **La conexión directa entre detección y remediación muestra un enfoque defensivo sólido y bien integrado.**

## Recursos utilizados

 * **Wazuh – Virtual Machine Deployment (OVA)**  
 https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html 
 
 * **Wazuh – Installation & Agents Documentation**  
 https://documentation.wazuh.com/current/installation-guide/index.html 
 
 * **Microsoft – Windows Server 2022 Evaluation Center**  
 https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022
 
 * **MITRE ATT&CK Framework**  
 https://attack.mitre.org/ 
 
 * **CIS Benchmarks – Windows Server**  
 https://www.cisecurity.org/cis-benchmarks

## Reconocimientos Especiales
Quiero expresar mi gratitud a los siguientes proyectos y desarrolladores, cuya documentación y herramientas en GitHub permitieron la realización de este laboratorio:

* **@Wazuh (GitHub)**
  
  https://github.com/wazuh

* **@SocFortress (GitHub)**
  
  https://github.com/socfortress

* **@OpenCyber-IO (GitHub)**
  
  https://github.com/opencyber-io
  
* **Sintaxis básica de escritura y formato**
  
   https://docs.github.com/es/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax

Estos recursos me ayudaron a entender cómo funciona la arquitectura SIEM, cómo detectar amenazas y qué prácticas realmente fortalecen la seguridad en entornos empresariales. Sin ellos, montar este laboratorio no habría sido posible.
  
> [!CAUTION]
> **AVISO LEGAL:** Este proyecto y el laboratorio documentado tienen fines exclusivamente **educativos y de referencia técnica**. El uso de las herramientas y tácticas descritas debe realizarse siempre en entornos controlados y con la debida autorización. El autor no se hace responsable del mal uso de la información contenida en este repositorio.
