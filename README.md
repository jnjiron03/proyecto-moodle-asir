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

#### Paso 1 — Verificar que el procesador soporta virtualización

Antes de instalar VMware compruebo que mi CPU tiene activada la virtualización por hardware desde el Administrador de tareas (`Ctrl + Shift + Esc`) → pestaña **Rendimiento → CPU**, donde debe aparecer **Virtualización: Habilitada**.

![Figura 1 — Virtualización habilitada en el procesador del equipo anfitrión](imagenes/reto-01/figura-01.png)  
*Figura 1 — Virtualización habilitada en el procesador del equipo anfitrión.*

#### Paso 2 — Instalar VMware Workstation 17 Pro

Descargo el instalador desde la web oficial de VMware/Broadcom y lo ejecuto como administrador. Sigo el asistente aceptando la licencia, dejando la ruta por defecto y activando el **Enhanced Keyboard Driver** para mejorar la compatibilidad con el teclado dentro de las VMs.

![Figura 2 — Instalación de VMware Workstation 17 Pro completada](imagenes/reto-01/figura-02.png)  
*Figura 2 — Instalación de VMware Workstation 17 Pro completada.*

#### Paso 3 — Verificar que VMware arranca correctamente

Abro VMware Workstation 17 Pro desde el escritorio y compruebo que se muestra la pantalla principal sin errores, con las opciones de creación y gestión de máquinas virtuales disponibles.

![Figura 3 — Pantalla principal del hipervisor VMware Workstation 17 Pro](imagenes/reto-01/figura-03.png)  
*Figura 3 — Pantalla principal del hipervisor VMware Workstation 17 Pro.*

#### Paso 4 — Explorar el menú de creación de máquinas virtuales

Accedo al asistente de creación de nueva VM (`Ctrl + N`) y observo las opciones disponibles: **Typical** para una configuración guiada simplificada y **Custom (Advanced)** para control total del hardware virtual.

![Figura 4 — Menú de creación de máquinas virtuales en VMware](imagenes/reto-01/figura-04.png)  
*Figura 4 — Menú de creación de máquinas virtuales en VMware.*

#### Paso 5 — Revisar las opciones de red virtual

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

> ⏳ *Pendiente de realización.*

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
