# ⚡ OPERATION: NANO BANANA | RED TEAM & OSINT PORTFOLIO
> **Lead Operator:** [nico] | **Target:** PcComponentes (Corporate Infrastructure) | **Status:** Success

---

## 📑 Resumen de la Misión
Este repositorio centraliza la documentación técnica de una intrusión simulada de extremo a extremo. Desde la fase inicial de inteligencia (OSINT) hasta el compromiso total del host mediante técnicas de persistencia en aplicaciones Electron y Command & Control (C2) avanzado.

---

## 📂 Informes de la Operación (Documentación Oficial)

| Fase | Documento Técnico | Descripción |
| :--- | :--- | :--- |
| **01 | RECON** | [📄 Ver Informe OSINT](./Osint%20-%20Red%20-%20Team.pdf) | Auditoría pasiva, brechas de datos y perfiles de directivos. |
| **02 | EXPLOIT** | [📄 Ver Informe Técnico C2](./Proyecto-%20Red-Team.pdf) | Inyección en memoria, bypass de EDR y persistencia C2. |

---

## 🛠️ Stack Tecnológico (Arsenal)

### **Inteligencia y Reconocimiento (OSINT)**
* **Footprinting:** `Censys`, `Shodan`, `Whois`
* **Harvesting:** `Hunter.io`, `theHarvester`, `LinkedIn`
* **Leaked Credentials:** `Have I Been Pwned`, `Dehashed` (Simulado)

### **Post-Explotación y C2**
* **Command & Control:** `Havoc C2 Framework (v0.7)`
* **Agent:** `Demon.exe` (x64 Payload)
* **Transport:** `SSH Reverse Tunneling` (Debian ARM Gateway)
* **Pivoting:** `Proxychains`, `Impacket`, `SMBClient`

---

## 🎯 Hitos Técnicos Destacados

### 🟢 Fase de Inteligencia: PcComponentes
Se realizó un perfilado completo de la directiva, identificando brechas de seguridad críticas.
* **Credential Stuffing:** Confirmación de exposición de correos corporativos en múltiples filtraciones públicas (6 breaches detectados en objetivos clave).
* **Targeting:** Desarrollo de vectores de *Spear Phishing* basados en patrones de comportamiento profesional en redes.

### 🔴 Compromiso del Host: Inyección "Demon"
Simulación de ataque contra un entorno **Windows 10 con defensas activas**.
* **Evasión de EDR:** Inyección de shellcode en aplicaciones Electron firmadas (Discord), aprovechando la confianza del sistema en procesos legítimos.
* **Arquitectura de Red:** Despliegue de un servidor C2 en una instancia Debian remota, comunicándose con el implante a través de un túnel cifrado para evadir inspección de tráfico en el gateway.

---

🛡️ Disclaimer
Este proyecto ha sido desarrollado exclusivamente con fines académicos y éticos dentro del marco del Full Stack Cybersecurity Bootcamp. Toda la actividad se ha realizado en laboratorios controlados y sobre información de fuentes públicas. No se autoriza su uso para actividades maliciosas.
<p align="center">
<b>Clasificación: CONFIDENCIAL // USO DOCENTE</b>

Abril 2026 - Modulo Red Team
</p>


