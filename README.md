# 🚩 Red Team Operations & OSINT Portfolio
> **Operador:** nico | **Bootcamp:** Full Stack Cybersecurity | **Fecha:** Abril 2026

Este repositorio contiene la documentación técnica y los artefactos de las operaciones realizadas durante la práctica final del módulo de Red Team. El proyecto se divide en dos fases críticas: **Inteligencia de Fuentes Abiertas (OSINT)** y **Explotación/C2 con Havoc Framework**.

---

## 📂 Contenido del Proyecto

### 1. 🔍 Fase OSINT: Reconocimiento de PcComponentes
Análisis pasivo de superficie de ataque sobre el e-commerce líder en tecnología.
* **Target:** `pccomponentes.com` (Grupo YF Networks).
* **Hallazgos Clave:** * Identificación de vectores de **Ingeniería Social** sobre personal clave (CEO/COO).
    * Detección de **brechas de credenciales históricas** afectando a directivos.
    * Mapeo de infraestructura tecnológica y filiales.
* **📄 [Ver Informe OSINT](./Osint-Red-Team.pdf)**

### 2. ⚡ Fase Red Team: Command & Control (Havoc C2)
Simulación de adversario avanzado contra un entorno Windows 10 con defensas activas.
* **Infraestructura:** Despliegue de servidor C2 en Debian (ARM) oculto tras túnel SSH reverso.
* **Técnica de Intrusión:** Inyección de shellcode (`Demon.exe`) en aplicaciones Electron firmadas (Discord).
* **Evasión:** Bypass de Windows Defender y persistencia mediante manipulación de archivos ASAR.
* **📄 [Ver Informe Técnico](./Proyecto-Red-Team.pdf)**

---

## 🛠️ Stack Tecnológico & Herramientas

| Fase | Herramientas Utilizadas |
| :--- | :--- |
| **OSINT** | `Censys`, `Shodan`, `Hunter.io`, `Have I Been Pwned`, `Google Dorks`, `LinkedIn` |
| **C2** | `Havoc Framework v0.7`, `Go-lang`, `SSH Reverse Tunneling` |
| **Pivoting** | `Proxychains`, `Impacket`, `SMBClient` |

---

## 🚀 Highlights de la Operación

### 🔘 Inyección en Memoria
Se logró la ejecución de un implante `Demon` de 64 bits dentro del proceso legítimo de Discord, evadiendo la detección por firmas al utilizar una aplicación firmada por un desarrollador de confianza como vector de carga.

### 🔘 Túneles de Comando
Configuración de una arquitectura de red donde el tráfico de C2 viajaba cifrado a través de un túnel SSH, permitiendo el control total de la máquina víctima (`DESKTOP-TV1TOU1`) desde una IP externa sin abrir puertos en el router del objetivo.

### 🔘 Ingeniería Social Basada en Datos
Cruce de datos de LinkedIn con bases de datos de filtraciones reales para construir perfiles de ataque dirigidos a la alta dirección, demostrando el riesgo real de la reutilización de contraseñas.

---

## ⚠️ Disclaimer
Todo el contenido de este repositorio ha sido generado exclusivamente con fines **académicos y docentes**. Las técnicas descritas se han ejecutado en entornos controlados de laboratorio. No se autoriza el uso de esta información para actividades ilícitas.

---
