# 🏴‍☠️ OPERACIÓN SHADOW SURGE — Red Team Full Lifecycle

![Mission Complete](https://img.shields.io/badge/STATUS-MISSION%20COMPLETE-success?style=for-the-badge)
![C2](https://img.shields.io/badge/C2-HAVOC%20v0.7-black?style=for-the-badge)
![Target](https://img.shields.io/badge/TARGET-WINDOWS%2010-blue?style=for-the-badge)
![Evasion](https://img.shields.io/badge/EVASION-DEFENDER%20BYPASS-red?style=for-the-badge)

> **Lead Operator:** `nico` | **Formación:** Full Stack Cybersecurity Bootcamp  
> **Objetivo:** Intrusión avanzada con evasión de EDR | **Entorno:** Proxmox (Debian 12 + Windows 10)

---

## 📋 Resumen Ejecutivo

Operación Red Team completa, desde el reconocimiento OSINT de una corporación real hasta la infección persistente de un Windows 10 con **Microsoft Defender activo**. Se desplegó **Havoc C2**, se inyectó shellcode en el proceso firmado `Discord.exe` y se mantuvo una sesión interactiva sin generar **ni una sola alerta de seguridad**.

---

## 🗺️ Arquitectura del Laboratorio

```mermaid
flowchart LR
    subgraph Proxmox
        Debian[Debian 12<br>C2 Server]
        Win10[Windows 10<br>Target]
    end
    Op[Mac M1] -->|RDP| Debian
    Op -->|RDP| Win10
    Win10 -->|SSH Reverse Tunnel| Debian
    Win10 <-->|HTTPS C2| Debian

⚔️ Fases de Ataque
1️⃣ OSINT — Reconocimiento Pasivo
Objetivo: PcComponentes (e‑commerce líder en España, Grupo YF Networks).

Mapeo de dominios, infraestructura (Cloudflare) y personal clave.

Hallazgo crítico: CEO y COO con correos corporativos filtrados en múltiples brechas, incluyendo contraseñas históricas. Viable credential stuffing y spear phishing.

Herramientas: whois, crt.sh, Shodan, Have I Been Pwned, theHarvester, LinkedIn.

📄 Informe OSINT completo

2️⃣ Infraestructura C2
Teamserver: Havoc v0.7 compilado desde fuente en Debian 12.

Túnel SSH inverso iniciado desde la víctima (ssh -R 1337) para atravesar el firewall.

Proxychains para enrutar herramientas ofensivas por el túnel.

Enumeración NTLM y movimiento lateral con Impacket + ntlm_challenger.

3️⃣ Infección Sigilosa — Bypass de Defender
Técnica: Inyección de shellcode en aplicación Electron legítima (Discord).

Cadena quirúrgica:

Extraer app.asar de Discord.
Generar payload Windows Shellcode (.bin) con Havoc.
Transformar shellcode a array JavaScript e inyectar en index.js.
Reempaquetar ASAR y sustituir el original.
Al abrir Discord, el código malicioso se ejecuta en memoria dentro del proceso firmado. Cero detecciones.

Sesión HTTPS establecida en Havoc bajo Discord.exe.

📄 Informe Técnico de Intrusión

✅ Verificación Final
Sesión activa en Havoc: DESKTOP-TV1TOU1\nico (miembro de Administrators).

Comando whoami /all ejecutado con éxito.

Windows Defender sin alertas.

🛡️ Contramedidas Recomendadas
Nivel	Medida
Red	Monitorizar conexiones salientes de apps legítimas a IPs no oficiales
Endpoint	EDR con inspección de memoria en procesos firmados
Sistema	AppLocker / WDAC para proteger carpetas de instalación
Integridad	Verificar hashes de archivos ASAR contra versiones oficiales
📂 Documentación
📊 Osint - Red - Team.pdf — Inteligencia y perfilado.

⚙️ Proyecto- Red-Team.pdf — C2, evasión e infección.

<p align="center"> <sub>👤 <b>nico</b> — Full Stack Cybersecurity Bootcamp | Abril 2026</sub><br/> <sub>⚠️ Uso exclusivamente académico</sub> </p> ```
