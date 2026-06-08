# Proyecto Implantación y Administración de un LMS Corporativo

**Alumno:** Jorge Noguera Jirón  
**Empresa:** CodeArts Solutions    
**Plataforma LMS:** Moodle  
**Servidor:** Ubuntu Server  
**Hipervisor:** VMware Workstation 17 Pro  

---

## Descripción del proyecto

Este proyecto consiste en el despliegue completo de una infraestructura LMS corporativa basada en Moodle, realizado íntegramente de forma manual sobre Ubuntu Server virtualizado con VMware Workstation 17 Pro.

El objetivo principal no es únicamente instalar Moodle, sino comprender cómo se despliega, organiza, administra y protege una infraestructura real basada en servicios Linux dentro de un entorno corporativo.

---

## Índice de retos

| Nº | Reto | Estado |
|---|---|---|
| 01 | [Preparación del entorno de virtualización corporativo](#reto-01--preparación-del-entorno-de-virtualización-corporativo) | ✅ Completado |
| 02 | [Despliegue y configuración inicial del servidor Ubuntu Server](#reto-02--despliegue-y-configuración-inicial-del-servidor-ubuntu-server) | ⏳ Pendiente |
| 03 | [Implementación de recurso compartido corporativo mediante Samba](#reto-03--implementación-de-recurso-compartido-corporativo-mediante-samba) | ⏳ Pendiente |
| 04 | [Implantación del servidor web Apache](#reto-04--implantación-del-servidor-web-apache) | ⏳ Pendiente |
| 05 | [Instalación del entorno PHP para la plataforma LMS](#reto-05--instalación-del-entorno-php-para-la-plataforma-lms) | ⏳ Pendiente |
| 06 | [Implantación y securización inicial de MariaDB](#reto-06--implantación-y-securización-inicial-de-mariadb) | ⏳ Pendiente |
| 07 | [Creación y configuración de la base de datos corporativa del LMS](#reto-07--creación-y-configuración-de-la-base-de-datos-corporativa-del-lms) | ⏳ Pendiente |
| 08 | [Configuración de resolución de nombres local para el LMS corporativo](#reto-08--configuración-de-resolución-de-nombres-local-para-el-lms-corporativo) | ⏳ Pendiente |
| 09 | [Despliegue y preparación de la estructura del LMS corporativo](#reto-09--despliegue-y-preparación-de-la-estructura-del-lms-corporativo) | ⏳ Pendiente |
| 10 | [Instalación lógica y configuración inicial de Moodle](#reto-10--instalación-lógica-y-configuración-inicial-de-moodle) | ⏳ Pendiente |
| 11 | [Administración inicial y configuración corporativa del LMS](#reto-11--administración-inicial-y-configuración-corporativa-del-lms) | ⏳ Pendiente |
| 12 | [Gestión corporativa de usuarios, roles y permisos en Moodle](#reto-12--gestión-corporativa-de-usuarios-roles-y-permisos-en-moodle) | ⏳ Pendiente |
| 13 | [Creación y organización del entorno formativo corporativo](#reto-13--creación-y-organización-del-entorno-formativo-corporativo) | ⏳ Pendiente |
| 14 | [Hardening y buenas prácticas básicas de seguridad del servidor LMS](#reto-14--hardening-y-buenas-prácticas-básicas-de-seguridad-del-servidor-lms) | ⏳ Pendiente |
| 15 | [Implementación de estrategia básica de copias de seguridad del LMS corporativo](#reto-15--implementación-de-estrategia-básica-de-copias-de-seguridad-del-lms-corporativo) | ⏳ Pendiente |

---

## Reto 01 — Preparación del entorno de virtualización corporativo

### Introducción

En este primer reto preparo el entorno de virtualización que utilizaré durante todo el proyecto. VMware Workstation 17 Pro actúa como hipervisor de tipo 2 sobre el equipo anfitrión, permitiéndome crear y gestionar la máquina virtual donde desplegaré el servidor Ubuntu que alojará Moodle. Antes de crear ninguna VM, verifico que el sistema es capaz de virtualizar y que el hipervisor está correctamente instalado.

### Objetivos

- Instalar VMware Workstation 17 Pro en el equipo anfitrión.
- Confirmar que el procesador soporta virtualización por hardware.
- Verificar que el hipervisor arranca y funciona correctamente.
- Reconocer las opciones principales del entorno: creación de VMs, hardware virtual, instantáneas, redes y almacenamiento.
- Definir los recursos que necesitará la VM del servidor Moodle.

### Material utilizado

| Elemento | Detalle |
|---|---|
| Equipo anfitrión | PC con Windows 10/11 (64 bits) |
| Software | VMware Workstation 17 Pro |
| Requisitos mínimos | CPU con VT-x/AMD-V, 8 GB RAM recomendados, 50 GB libres en disco |

### Desarrollo

#### Verificar que el procesador soporta virtualización

Antes de instalar VMware compruebo que mi CPU tiene activada la virtualización por hardware desde el Administrador de tareas (`Ctrl + Shift + Esc`) → pestaña **Rendimiento → CPU**, donde debe aparecer **Virtualización: Habilitada**.

![Figura 1 — Virtualización habilitada en el procesador del equipo anfitrión](imagenes/reto-01/figura-01.png)  
*Figura 1 — Virtualización habilitada en el procesador del equipo anfitrión.*

#### Instalar VMware Workstation 17 Pro

Descargo el instalador desde la web oficial de VMware/Broadcom y lo ejecuto como administrador. Sigo el asistente aceptando la licencia, dejando la ruta por defecto y activando el **Enhanced Keyboard Driver** para mejorar la compatibilidad con el teclado dentro de las VMs.

![Figura 2 — Instalación de VMware Workstation 17 Pro completada](imagenes/reto-01/figura-02.png)  
*Figura 2 — Instalación de VMware Workstation 17 Pro completada.*

#### Verificar que VMware arranca correctamente

Abro VMware Workstation 17 Pro desde el escritorio y compruebo que se muestra la pantalla principal sin errores, con las opciones de creación y gestión de máquinas virtuales disponibles.

![Figura 3 — Pantalla principal del hipervisor VMware Workstation 17 Pro](imagenes/reto-01/figura-03.png)  
*Figura 3 — Pantalla principal del hipervisor VMware Workstation 17 Pro.*

#### Explorar el menú de creación de máquinas virtuales

Accedo al asistente de creación de nueva VM (`Ctrl + N`) y observo las opciones disponibles: **Typical** para una configuración guiada simplificada y **Custom (Advanced)** para control total del hardware virtual.

![Figura 4 — Menú de creación de máquinas virtuales en VMware](imagenes/reto-01/figura-04.png)  
*Figura 4 — Menú de creación de máquinas virtuales en VMware.*

#### Revisar las opciones de red virtual

Accedo a **Edit → Virtual Network Editor** y reviso los tres tipos de red disponibles:

| Tipo | Nombre | Función |
|---|---|---|
| Bridged | VMnet0 | La VM se conecta directamente a la red física del host |
| NAT | VMnet8 | La VM accede a Internet usando la IP del host |
| Host-only | VMnet1 | La VM solo se comunica con el host, sin acceso externo |

Para el servidor Moodle utilizaré **NAT** durante la instalación para tener acceso a Internet y descargar paquetes.

![Figura 5 — Opciones de red virtual disponibles en VMware](imagenes/reto-01/figura-05.png)  
*Figura 5 — Opciones de red virtual disponibles en VMware.*

### Explicación técnica

**Función de la virtualización en el proyecto:**  
VMware Workstation actúa como hipervisor de tipo 2, ejecutándose sobre el sistema operativo del equipo anfitrión. Su función es crear una máquina virtual aislada donde instalaré Ubuntu Server, que a su vez alojará todos los servicios del LMS Moodle (Apache, PHP, MariaDB). Gracias a la virtualización, simulo un servidor real completo sin necesidad de hardware dedicado, manteniendo el entorno del proyecto separado del sistema operativo principal.

**Por qué es útil usar máquinas virtuales en administración de sistemas:**  
Las máquinas virtuales permiten desplegar y destruir entornos de prueba rápidamente sin afectar al equipo físico. Las instantáneas permiten guardar el estado del servidor antes de realizar cambios críticos, facilitando revertir errores. El aislamiento entre host y VM mejora la seguridad, y la portabilidad de los archivos `.vmdk` permite mover o clonar el servidor completo fácilmente.

### Comprobaciones finales

- [x] VMware 17 Pro instalado y abre sin errores.
- [x] Administrador de tareas muestra **Virtualización: Habilitada**.
- [x] Pantalla principal del hipervisor visible.
- [x] Asistente de creación de VM explorado.
- [x] Virtual Network Editor abierto y tipos de red identificados.

---

## Reto 02 — Despliegue y configuración inicial del servidor Ubuntu Server

## Reto 02 — Despliegue y configuración inicial del servidor Ubuntu Server

### Introducción

En este reto creo y configuro la máquina virtual que actuará como servidor base de todo el proyecto. Sobre ella instalo Ubuntu Server, establezco una IP estática mediante Netplan y habilito el acceso remoto por SSH. Al finalizar, el servidor queda completamente operativo y listo para recibir los servicios de Moodle en los retos siguientes.

### Objetivos

- Crear la VM en VMware con los recursos adecuados para un LMS pequeño.
- Instalar Ubuntu Server configurando hostname, usuario y red.
- Asignar una IP estática al servidor mediante Netplan.
- Habilitar y verificar el acceso remoto por SSH.
- Confirmar conectividad desde el equipo anfitrión.

### Material utilizado

| Elemento | Detalle |
|---|---|
| Hipervisor | VMware Workstation 17 Pro |
| SO invitado | Ubuntu Server 22.04 LTS |
| RAM | 4 GB |
| CPU | 2 núcleos |
| Disco | 40 GB |
| Red | Adaptador puente (Bridge) |
| Equipo anfitrión | Windows 10/11 |

### Desarrollo

#### Descarga de la ISO de Ubuntu Server

Accedo a [https://ubuntu.com/download/server](https://ubuntu.com/download/server) y descargo la imagen **Ubuntu Server 22.04 LTS**. La guardo en una ubicación accesible desde el equipo anfitrión.

#### Creación de la máquina virtual en VMware

En VMware creo una nueva VM en modo **Custom (Advanced)** con los siguientes recursos:

| Recurso | Configuración |
|---|---|
| RAM | 4096 MB (4 GB) |
| CPU | 2 núcleos |
| Disco | 40 GB (SCSI) |
| Red | Bridged (adaptador puente) |

Asigno el nombre `moodle-server` a la VM, asocio la ISO de Ubuntu Server descargada y arranco la instalación.

![Figura 1 — Configuración de hardware de la máquina virtual](imagenes/reto-02/figura-01.png)
*Figura 1 — Configuración de hardware de la máquina virtual.*

#### Instalación de Ubuntu Server

Durante el proceso de instalación realizo las siguientes configuraciones:

- **Idioma y teclado** según la región.
- **Tipo de instalación:** Ubuntu Server estándar.
- **Hostname:** `moodle-server`.
- **Usuario administrador:** nombre de usuario y contraseña definidos para el proyecto.
- **OpenSSH:** marcada la casilla de instalación automática ✅.
- **Snaps adicionales:** ninguno — los servicios se instalan manualmente en retos posteriores.

![Figura 2 — Configuración del hostname durante la instalación](imagenes/reto-02/figura-02.png)
*Figura 2 — Configuración del hostname durante la instalación.*

![Figura 3 — Ubuntu Server instalado y primer acceso por consola](imagenes/reto-02/figura-03.png)
*Figura 3 — Ubuntu Server instalado y primer acceso por consola.*

#### Configuración de IP estática con Netplan

Ubuntu Server gestiona la red mediante **Netplan**. Identifico primero el nombre de la interfaz con `ip a` y edito el archivo de configuración:

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      routes:
        - to: default
          via: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

Aplico la configuración:

```bash
sudo netplan apply
```

![Figura 4 — Configuración de IP estática mediante Netplan](imagenes/reto-02/figura-04.png)
*Figura 4 — Configuración de IP estática mediante Netplan.*

#### Verificación de la IP estática

Compruebo que la IP estática ha sido aplicada correctamente:

```bash
ip a
```

![Figura 5 — IP estática configurada y visible con ip a](imagenes/reto-02/figura-05.png)
*Figura 5 — IP estática configurada y visible con `ip a`.*

#### Verificación de conectividad a Internet

Desde el servidor compruebo conectividad al exterior y resolución de nombres:

```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
```

![Figura 6 — Prueba de conectividad a Internet desde el servidor](imagenes/reto-02/figura-06.png)
*Figura 6 — Prueba de conectividad a Internet desde el servidor.*

#### Acceso remoto por SSH desde el equipo anfitrión

Desde PowerShell en el equipo anfitrión me conecto al servidor:

```bash
ssh jorge@192.168.1.100
```

La conexión se establece correctamente, confirmando que OpenSSH está operativo y el servidor es administrable de forma remota.

![Figura 7 — Acceso remoto al servidor mediante SSH desde el equipo anfitrión](imagenes/reto-02/figura-07.png)
*Figura 7 — Acceso remoto al servidor mediante SSH desde el equipo anfitrión.*

### Comprobaciones finales

- [x] VM creada con 4 GB RAM, 2 núcleos, 40 GB disco y red Bridge.
- [x] Ubuntu Server instalado con hostname `moodle-server`.
- [x] Usuario administrador creado.
- [x] IP estática configurada y visible con `ip a`.
- [x] Ping al exterior responde correctamente.
- [x] OpenSSH operativo y acceso remoto verificado desde el host.

---

## Reto 03 — Implementación de recurso compartido corporativo mediante Samba

> ⏳ *Pendiente de realización.*

---

## Reto 04 — Implantación del servidor web Apache

> ⏳ *Pendiente de realización.*

---

## Reto 05 — Instalación del entorno PHP para la plataforma LMS

> ⏳ *Pendiente de realización.*

---

## Reto 06 — Implantación y securización inicial de MariaDB

> ⏳ *Pendiente de realización.*

---

## Reto 07 — Creación y configuración de la base de datos corporativa del LMS

> ⏳ *Pendiente de realización.*

---

## Reto 08 — Configuración de resolución de nombres local para el LMS corporativo

> ⏳ *Pendiente de realización.*

---

## Reto 09 — Despliegue y preparación de la estructura del LMS corporativo

> ⏳ *Pendiente de realización.*

---

## Reto 10 — Instalación lógica y configuración inicial de Moodle

> ⏳ *Pendiente de realización.*

---

## Reto 11 — Administración inicial y configuración corporativa del LMS

> ⏳ *Pendiente de realización.*

---

## Reto 12 — Gestión corporativa de usuarios, roles y permisos en Moodle

> ⏳ *Pendiente de realización.*

---

## Reto 13 — Creación y organización del entorno formativo corporativo

> ⏳ *Pendiente de realización.*

---

## Reto 14 — Hardening y buenas prácticas básicas de seguridad del servidor LMS

> ⏳ *Pendiente de realización.*

---

## Reto 15 — Implementación de estrategia básica de copias de seguridad del LMS corporativo

> ⏳ *Pendiente de realización.*
