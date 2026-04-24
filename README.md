# 🏴‍☠️ OPERACIÓN SHADOW SURGE

![Mission](https://img.shields.io/badge/STATUS-COMPLETE-success?style=flat-square)
![C2](https://img.shields.io/badge/C2-HAVOC_v0.7-black?style=flat-square)
![Target](https://img.shields.io/badge/TARGET-Windows_10-blue?style=flat-square)
![Evasion](https://img.shields.io/badge/EVASION-Defender_Bypass-red?style=flat-square)

**Operador:** `nico` | **Formación:** Full Stack Cybersecurity Bootcamp  
**Objetivo:** Simulación realista de intrusión con evasión de EDR  
**Entorno:** Proxmox VE — Debian 12 (C2) + Windows 10 (víctima)

---

## 📋 Resumen

Operación Red Team completa: desde OSINT sobre una corporación real hasta la infección de un Windows 10 con **Microsoft Defender activo**. Se usó **Havoc C2** y se inyectó shellcode en el proceso firmado `Discord.exe`.  
**Resultado:** sesión interactiva con **cero alertas de seguridad**.

---

## 🗺️ Arquitectura

┌──────────────┐ SSH Reverse Tunnel ┌──────────────┐
│ Windows 10 │ ───────────────────────────► │ Debian 12 │
│ (Víctima) │ ◄─────── HTTPS C2 ───────── │ (Atacante) │
└──────────────┘ └──────────────┘
▲ ▲
│ Mac M1 (Operador) │
└────────────────── RDP ─────────────────────┘


---

## ⚔️ Fases del Ataque

### 1. OSINT — Reconocimiento Pasivo
- **Objetivo:** PcComponentes (mayor e-commerce tecnológico de España).
- Mapeo de dominios, infraestructura (Cloudflare) y personal clave.
- **Hallazgo:** CEO y COO con correos corporativos expuestos en brechas, incluyendo contraseñas históricas.
- Vector viable: *credential stuffing* y *spear phishing*.
- 📄 [Informe OSINT completo](./Osint%20-%20Red%20-%20Team.pdf)

### 2. Infraestructura C2
- **Havoc v0.7** compilado desde código fuente.
- Túnel SSH inverso iniciado desde la víctima para saltar el firewall.
- **Proxychains** para enrutar herramientas (Impacket, ntlm_challenger) a través del túnel.
- Enumeración NTLM y movimiento lateral exitoso.

### 3. Infección Sigilosa (Defender Bypass)
- **Técnica:** Inyección de shellcode en aplicación Electron legítima (Discord).
- Se extrae el contenedor `app.asar`, se incrusta la shellcode en `index.js` y se reempaqueta.
- Al abrir Discord, el código se ejecuta **en memoria** dentro de un proceso firmado.
- 📄 [Informe Técnico de Intrusión](./Proyecto-%20Red-Team.pdf)

---

## ✅ Verificación Final

- Sesión activa en Havoc: `DESKTOP-TV1TOU1\nico` (Administradores).
- Comando `whoami /all` ejecutado con éxito.
- **Windows Defender sin alertas.**

---

## 🛡️ Contramedidas

| Nivel | Medida |
| :--- | :--- |
| **Red** | Monitorizar conexiones salientes de apps legítimas a IPs no oficiales |
| **Endpoint** | EDR con inspección de memoria en procesos firmados |
| **Sistema** | AppLocker / WDAC para proteger carpetas de instalación |
| **Integridad** | Verificar hashes de archivos ASAR contra versiones oficiales |

---

## 📂 Documentos

- 📊 [**Osint - Red - Team.pdf**](./Osint%20-%20Red%20-%20Team.pdf)
- ⚙️ [**Proyecto- Red-Team.pdf**](./Proyecto-%20Red-Team.pdf)

---

<p align="center">
  <sub>👤 <b>nico</b> — Full Stack Cybersecurity Bootcamp | Abril 2026</sub><br/>
  <sub>⚠️ Uso exclusivamente académico</sub>
</p>
