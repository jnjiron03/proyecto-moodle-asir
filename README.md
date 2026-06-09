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
| 02 | [Despliegue y configuración inicial del servidor Ubuntu Server](#reto-02--despliegue-y-configuración-inicial-del-servidor-ubuntu-server) | ✅ Completado |
| 03 | [Implementación de recurso compartido corporativo mediante Samba](#reto-03--implementación-de-recurso-compartido-corporativo-mediante-samba) | ✅ Completado |
| 04 | [Implantación del servidor web Apache](#reto-04--implantación-del-servidor-web-apache) | ✅ Completado |
| 05 | [Instalación del entorno PHP para la plataforma LMS](#reto-05--instalación-del-entorno-php-para-la-plataforma-lms) | ✅ Completado |
| 06 | [Implantación y securización inicial de MariaDB](#reto-06--implantación-y-securización-inicial-de-mariadb) |✅ Completado |
| 07 | [Creación y configuración de la base de datos corporativa del LMS](#reto-07--creación-y-configuración-de-la-base-de-datos-corporativa-del-lms) | ✅ Completado|
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

### Introducción

En este reto habilito un recurso compartido en red dentro del servidor Ubuntu Server utilizando Samba, un servicio que permite compartir carpetas entre sistemas Linux, Windows y macOS dentro de la misma red local. El recurso `codearts-share` servirá como punto de intercambio de archivos entre el servidor y el equipo anfitrión durante todo el proyecto.

### Objetivos

- Instalar y configurar el servicio Samba en Ubuntu Server.
- Crear la carpeta corporativa `/srv/codearts-share` con los permisos adecuados.
- Publicar el recurso compartido con el nombre `codearts-share`.
- Verificar que el servicio está activo y el recurso es accesible desde Windows.

### Material utilizado

| Elemento | Detalle |
|---|---|
| Servidor | Ubuntu Server 22.04 LTS |
| IP del servidor | 192.168.1.13 |
| Servicio | Samba |
| Carpeta compartida | `/srv/codearts-share` |
| Nombre del recurso | `codearts-share` |
| Acceso desde | Windows (equipo anfitrión) |

### Desarrollo

#### Actualización del sistema e instalación de Samba

Actualizo los repositorios del sistema antes de instalar cualquier servicio:

```bash
sudo apt update && sudo apt upgrade -y
```

Instalo el paquete de Samba:

```bash
sudo apt install samba -y
```

Verifico que la instalación se ha completado correctamente comprobando la versión del demonio instalado:

```bash
smbd --version
```

![Figura 1 — Instalación de Samba en Ubuntu Server](imagenes/reto-03/figura-01.png)

*Figura 1 — Instalación de Samba en Ubuntu Server.*

#### Creación de la carpeta compartida corporativa

Creo el directorio obligatorio del proyecto en la ruta indicada:

```bash
sudo mkdir -p /srv/codearts-share
```

Asigno el propietario y los permisos necesarios para que el usuario pueda leer y escribir dentro de la carpeta:

```bash
sudo chown -R jorge:jorge /srv/codearts-share
sudo chmod 777 /srv/codearts-share
```

Verifico que la carpeta existe con los permisos correctos:

```bash
ls -ld /srv/codearts-share
```

![Figura 2 — Creación de la carpeta /srv/codearts-share con permisos correctos](imagenes/reto-03/figura-02.png)

*Figura 2 — Creación de la carpeta `/srv/codearts-share` con permisos correctos.*

#### Configuración de Samba

Realizo una copia de seguridad del archivo de configuración original antes de modificarlo:

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
```

Edito el archivo de configuración y añado el bloque del recurso compartido al final:

```bash
sudo nano /etc/samba/smb.conf
```

```ini
[codearts-share]
   path = /srv/codearts-share
   browseable = yes
   read only = no
   guest ok = no
   valid users = jorge
   force user = jorge
   create mask = 0664
   directory mask = 0775
```

Verifico que la sintaxis del archivo es correcta:

```bash
testparm
```

![Figura 3 — Configuración del recurso compartido en smb.conf](imagenes/reto-03/figura-03.png)

*Figura 3 — Configuración del recurso compartido en `smb.conf`.*

#### Registro del usuario Samba y apertura del firewall

Registro el usuario `jorge` en el sistema de contraseñas de Samba y lo activo:

```bash
sudo smbpasswd -a jorge
sudo smbpasswd -e jorge
```

Permito el tráfico de Samba a través del firewall:

```bash
sudo ufw allow samba
sudo ufw status
```

#### Reinicio y verificación del servicio Samba

Reinicio los servicios de Samba para aplicar la configuración y compruebo que están activos:

```bash
sudo systemctl restart smbd nmbd
sudo systemctl status smbd
```

![Figura 4 — Servicio Samba activo y en ejecución](imagenes/reto-03/figura-04.png)

*Figura 4 — Servicio Samba activo y en ejecución.*

#### Acceso al recurso compartido desde Windows

Desde el equipo anfitrión Windows abro el Explorador de archivos e introduzco en la barra de direcciones:

```
\\192.168.1.13\codearts-share
```

Introduzco las credenciales del usuario Samba cuando se solicitan. La carpeta compartida se abre correctamente.

![Figura 5 — Acceso al recurso compartido desde el equipo anfitrión Windows](imagenes/reto-03/figura-05.png)

*Figura 5 — Acceso al recurso compartido desde el equipo anfitrión Windows.*

#### Prueba de escritura en el recurso compartido

Creo un archivo de prueba desde Windows dentro de la carpeta compartida y verifico desde el servidor que ha aparecido correctamente:

```bash
ls -l /srv/codearts-share
```

![Figura 6 — Archivo de prueba creado desde Windows visible en el servidor](imagenes/reto-03/figura-06.png)

*Figura 6 — Archivo de prueba creado desde Windows visible en el servidor.*

### Comprobaciones finales

- [x] Samba instalado correctamente en Ubuntu Server.
- [x] Carpeta `/srv/codearts-share` creada con propietario y permisos adecuados.
- [x] Bloque `[codearts-share]` añadido a `smb.conf` sin errores de sintaxis.
- [x] Usuario Samba registrado y activo.
- [x] Firewall permite tráfico Samba.
- [x] Servicio `smbd` activo y en ejecución.
- [x] Recurso accesible desde Windows mediante `\\192.168.1.13\codearts-share`.
- [x] Escritura de archivos verificada desde ambos extremos.

---

## Reto 04 — Implantación del servidor web Apache

### Introducción

En este reto instalo Apache en el servidor Ubuntu, que será el componente encargado de servir las páginas web del LMS Moodle a los usuarios de la red local. Antes de instalar Moodle o cualquier otro servicio, verifico que Apache responde correctamente a peticiones HTTP en el puerto 80 desde el equipo anfitrión, dejando así la base web de la infraestructura preparada para los retos siguientes.

### Objetivos

- Instalar el servidor web Apache2 en Ubuntu Server.
- Configurar el arranque automático del servicio.
- Abrir el puerto 80 en el firewall.
- Validar que Apache está activo y escuchando en el puerto 80.
- Comprobar el acceso HTTP desde el navegador del equipo anfitrión.

### Material utilizado

| Elemento | Detalle |
|---|---|
| Servidor | Ubuntu Server 22.04 LTS |
| IP del servidor | 192.168.1.13 |
| Servicio | Apache2 |
| Puerto | 80 (HTTP) |
| Acceso desde | Navegador del equipo anfitrión Windows |

### Desarrollo

#### Instalación de Apache2

Actualizo los repositorios e instalo Apache:

```bash
sudo apt update && sudo apt install apache2 -y
```

![Figura 1 — Instalación de Apache2 en Ubuntu Server](imagenes/reto-04/figura-01.png)

*Figura 1 — Instalación de Apache2 en Ubuntu Server.*

#### Habilitación del arranque automático y apertura del firewall

Configuro Apache para que se inicie automáticamente con el sistema:

```bash
sudo systemctl enable apache2
```

Permito el tráfico HTTP en el firewall:

```bash
sudo ufw allow 'Apache'
sudo ufw status
```

#### Verificación del estado del servicio

Compruebo que Apache está activo y en ejecución:

```bash
sudo systemctl status apache2
```

![Figura 2 — Servicio Apache2 activo y en ejecución](imagenes/reto-04/figura-02.png)

*Figura 2 — Servicio Apache2 activo y en ejecución.*

#### Validación del puerto 80 y respuesta local

Verifico que Apache está escuchando correctamente en el puerto 80 y que el servidor responde localmente:

```bash
sudo ss -tlnp | grep 80
curl -I http://localhost
```

La respuesta incluye `HTTP/1.1 200 OK`, confirmando que Apache devuelve contenido correctamente.

![Figura 3 — Validación del puerto 80 y respuesta HTTP del servidor](imagenes/reto-04/figura-03.png)

*Figura 3 — Validación del puerto 80 y respuesta HTTP del servidor.*

#### Acceso desde el navegador del equipo anfitrión

Desde el equipo anfitrión Windows accedo mediante el navegador a:

```
http://192.168.1.13
```

Se carga la página por defecto de Apache con el mensaje **"Apache2 Ubuntu Default Page"**, confirmando que el servidor web es accesible desde la red local.

![Figura 4 — Página por defecto de Apache2 accesible desde el equipo anfitrión](imagenes/reto-04/figura-04.png)

*Figura 4 — Página por defecto de Apache2 accesible desde el equipo anfitrión.*

### Comprobaciones finales

- [x] Apache2 instalado correctamente.
- [x] Servicio configurado para arranque automático con `systemctl enable`.
- [x] Puerto 80 abierto en el firewall UFW.
- [x] `systemctl status apache2` muestra **active (running)**.
- [x] Puerto 80 escuchando verificado con `ss -tlnp`.
- [x] Respuesta `200 OK` confirmada con `curl` desde el servidor.
- [x] Página por defecto de Apache visible desde el navegador del anfitrión.

---

## Reto 05 — Instalación del entorno PHP para la plataforma LMS

### Introducción

Moodle es una aplicación web desarrollada en PHP, por lo que el servidor necesita un intérprete PHP completamente funcional e integrado con Apache. En este reto instalo PHP junto con todas las extensiones que Moodle requiere para funcionar correctamente, y verifico que Apache es capaz de procesar archivos PHP mediante una página de prueba visible desde el navegador.

### Objetivos

- Instalar PHP y los módulos necesarios para Moodle en Ubuntu Server.
- Verificar la versión instalada de PHP.
- Confirmar la integración correcta entre Apache y PHP.
- Crear y validar un archivo de prueba `info.php` desde el navegador.

### Material utilizado

| Elemento | Detalle |
|---|---|
| Servidor | Ubuntu Server 22.04 LTS |
| IP del servidor | 192.168.1.13 |
| Lenguaje | PHP 8.x |
| Servidor web | Apache2 |
| Directorio web | `/var/www/html/` |

### Desarrollo

#### Instalación de PHP y módulos requeridos por Moodle

Actualizo los repositorios e instalo PHP junto con todas las extensiones que Moodle necesita. El módulo OPcache viene incluido dentro del paquete principal de PHP en Ubuntu y no requiere instalación separada:

```bash
sudo apt update && sudo apt install php libapache2-mod-php php-mysql php-xml php-mbstring php-curl php-zip php-gd php-intl php-soap php-cli -y
```

Estas extensiones cubren los requisitos de Moodle 4.x:

| Módulo | Función en Moodle |
|---|---|
| `libapache2-mod-php` | Integración de PHP con Apache |
| `php-mysql` | Conexión con la base de datos MariaDB |
| `php-xml` | Procesamiento de XML y RSS |
| `php-mbstring` | Soporte de caracteres multibyte y UTF-8 |
| `php-curl` | Peticiones HTTP externas |
| `php-zip` | Gestión de archivos comprimidos |
| `php-gd` | Procesamiento de imágenes |
| `php-intl` | Internacionalización y localización |
| `php-soap` | Servicios web SOAP |
| `OPcache` | Incluido en el paquete PHP base — caché de código para mejor rendimiento |

![Figura 1 — Instalación de PHP y módulos requeridos por Moodle](imagenes/reto-05/figura-01.png)

*Figura 1 — Instalación de PHP y módulos requeridos por Moodle.*

#### Verificación de la versión instalada de PHP

Compruebo que PHP se ha instalado correctamente y verifico la versión disponible:

```bash
php --version
```

Verifico también que OPcache está cargado correctamente:

```bash
php -m | grep -i opcache
```

![Figura 2 — Versión de PHP instalada en el servidor](imagenes/reto-05/figura-02.png)

*Figura 2 — Versión de PHP instalada en el servidor.*

#### Reinicio de Apache tras la integración con PHP

Reinicio Apache para que cargue el módulo PHP correctamente y compruebo que el servicio sigue activo:

```bash
sudo systemctl restart apache2
sudo systemctl status apache2
```

![Figura 3 — Estado de Apache2 tras la integración con PHP](imagenes/reto-05/figura-03.png)

*Figura 3 — Estado de Apache2 tras la integración con PHP.*

#### Creación del archivo de prueba phpinfo

Creo un archivo PHP dentro del directorio web de Apache para verificar que el servidor procesa PHP correctamente:

```bash
sudo nano /var/www/html/info.php
```

Contenido del archivo:

```php
<?php
phpinfo();
?>
```

![Figura 4 — Archivo de prueba info.php creado en el directorio web](imagenes/reto-05/figura-04.png)

*Figura 4 — Archivo de prueba `info.php` creado en el directorio web.*

#### Validación del entorno PHP desde el navegador

Desde el equipo anfitrión Windows accedo mediante el navegador a:

```
http://192.168.1.13/info.php
```

Se carga la página de información de PHP con todos los módulos instalados, la versión y la integración con Apache, confirmando que el servidor procesa correctamente archivos PHP. Una vez validado, elimino el archivo por seguridad ya que expone información sensible del servidor:

```bash
sudo rm /var/www/html/info.php
```

![Figura 5 — Página phpinfo() accesible desde el navegador del equipo anfitrión](imagenes/reto-05/figura-05.png)

*Figura 5 — Página phpinfo() accesible desde el navegador del equipo anfitrión.*

### Comprobaciones finales

- [x] PHP y todos los módulos requeridos por Moodle instalados.
- [x] OPcache activo verificado con `php -m | grep -i opcache`.
- [x] `php --version` muestra la versión instalada correctamente.
- [x] Apache reiniciado y activo tras la integración con PHP.
- [x] Archivo `info.php` creado en `/var/www/html/`.
- [x] Página `phpinfo()` accesible desde el navegador del anfitrión.
- [x] Archivo `info.php` eliminado tras la validación.

---

## Reto 06 — Implantación y securización inicial de MariaDB

### Introducción

MariaDB será el motor de base de datos que almacenará toda la información del LMS Moodle: usuarios, cursos, calificaciones y contenidos. En este reto instalo el servicio, lo configuro para que arranque automáticamente con el sistema y aplico la securización inicial básica para eliminar configuraciones inseguras por defecto que MariaDB trae al instalarse.

### Objetivos

- Instalar MariaDB en Ubuntu Server.
- Configurar el arranque automático del servicio.
- Ejecutar la securización inicial con `mariadb-secure-installation`.
- Verificar el acceso administrativo al motor de base de datos.

### Material utilizado

| Elemento | Detalle |
|---|---|
| Servidor | Ubuntu Server 22.04 LTS |
| IP del servidor | 192.168.1.13 |
| Motor de base de datos | MariaDB |
| Puerto | 3306 |

### Desarrollo

#### Instalación de MariaDB

Actualizo los repositorios e instalo el servidor MariaDB:

```bash
sudo apt update && sudo apt install mariadb-server -y
```

![Figura 1 — Instalación de MariaDB en Ubuntu Server](imagenes/reto-06/figura-01.png)

*Figura 1 — Instalación de MariaDB en Ubuntu Server.*

#### Habilitación del arranque automático y verificación del servicio

Configuro MariaDB para que se inicie automáticamente con el sistema y compruebo que está activo:

```bash
sudo systemctl enable mariadb
sudo systemctl status mariadb
```

![Figura 2 — Servicio MariaDB activo y configurado para arranque automático](imagenes/reto-06/figura-02.png)

*Figura 2 — Servicio MariaDB activo y configurado para arranque automático.*

#### Securización inicial del servidor MariaDB

Ejecuto el asistente de securización inicial. En versiones modernas de MariaDB el comando correcto es:

```bash
sudo mariadb-secure-installation
```

Durante el proceso aplico las siguientes medidas de seguridad:

| Pregunta | Respuesta aplicada |
|---|---|
| Enter current password for root | `Enter` (sin contraseña por defecto) |
| Switch to unix_socket authentication | `n` |
| Change the root password | `y` → contraseña segura configurada |
| Remove anonymous users | `y` |
| Disallow root login remotely | `y` |
| Remove test database and access to it | `y` |
| Reload privilege tables now | `y` |

![Figura 3 — Ejecución del proceso de securización inicial de MariaDB](imagenes/reto-06/figura-03.png)

*Figura 3 — Ejecución del proceso de securización inicial de MariaDB.*

#### Verificación del acceso administrativo

Accedo al motor de base de datos con el usuario root para confirmar que la autenticación funciona correctamente:

```bash
sudo mysql -u root -p
```

Una vez dentro, ejecuto una consulta básica para verificar el estado del sistema:

```sql
SHOW DATABASES;
```

La base de datos `test` no aparece en el listado, confirmando que la securización se aplicó correctamente. Salgo del entorno:

```sql
EXIT;
```

![Figura 4 — Acceso administrativo a MariaDB y verificación de bases de datos](imagenes/reto-06/figura-04.png)

*Figura 4 — Acceso administrativo a MariaDB y verificación de bases de datos.*

#### Validaciones adicionales del servicio

Verifico que MariaDB está escuchando en el puerto correcto y compruebo la versión instalada:

```bash
sudo ss -tlnp | grep 3306
mysql --version
```

![Figura 5 — Validación del puerto 3306 y versión de MariaDB instalada](imagenes/reto-06/figura-05.png)

*Figura 5 — Validación del puerto 3306 y versión de MariaDB instalada.*

### Comprobaciones finales

- [x] MariaDB instalado correctamente.
- [x] Servicio activo y configurado para arranque automático.
- [x] `mariadb-secure-installation` ejecutado con todas las medidas aplicadas.
- [x] Contraseña de root configurada.
- [x] Usuarios anónimos eliminados.
- [x] Acceso root remoto desactivado.
- [x] Base de datos `test` eliminada.
- [x] Acceso administrativo verificado con `SHOW DATABASES;`.
- [x] Puerto 3306 activo y escuchando correctamente.

---
## Reto 07 — Creación y configuración de la base de datos corporativa del LMS

### Introducción

Con MariaDB instalado y securizado, el siguiente paso es preparar la estructura SQL que utilizará Moodle. En lugar de usar la cuenta root para la aplicación, creo un usuario dedicado `moodle_user` con permisos únicamente sobre la base de datos `moodle_db`. Esta práctica sigue el principio de mínimo privilegio y es fundamental en cualquier entorno de administración profesional.

### Objetivos

- Crear la base de datos `moodle_db` en MariaDB.
- Crear el usuario `moodle_user` con contraseña segura.
- Asignar permisos exclusivos sobre `moodle_db`.
- Verificar que el usuario puede autenticarse y acceder correctamente.

### Material utilizado

| Elemento | Detalle |
|---|---|
| Servidor | Ubuntu Server 22.04 LTS |
| IP del servidor | 192.168.1.13 |
| Motor de base de datos | MariaDB |
| Base de datos | `moodle_db` |
| Usuario LMS | `moodle_user` |

### Desarrollo

#### Acceso al entorno de administración MariaDB

Accedo al motor de base de datos con el usuario root:

```bash
sudo mysql -u root -p
```

El prompt cambia a `MariaDB [(none)]>`, indicando que estoy dentro del entorno SQL.

![Figura 1 — Acceso al entorno de administración MariaDB](imagenes/reto-07/figura-01.png)

*Figura 1 — Acceso al entorno de administración MariaDB.*

#### Creación de la base de datos

Creo la base de datos con codificación UTF-8 para garantizar compatibilidad completa con Moodle y sus contenidos multilingües:

```sql
CREATE DATABASE moodle_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Verifico que se ha creado correctamente:

```sql
SHOW DATABASES;
```

![Figura 2 — Base de datos moodle_db creada correctamente](imagenes/reto-07/figura-02.png)

*Figura 2 — Base de datos `moodle_db` creada correctamente.*

#### Creación del usuario exclusivo del LMS y asignación de privilegios

Creo el usuario `moodle_user` con acceso únicamente desde localhost, siguiendo el principio de mínimo privilegio:

```sql
CREATE USER 'moodle_user'@'localhost' IDENTIFIED BY 'TuContraseñaSegura';
```

Asigno todos los permisos necesarios exclusivamente sobre `moodle_db` y actualizo la tabla de privilegios:

```sql
GRANT ALL PRIVILEGES ON moodle_db.* TO 'moodle_user'@'localhost';
FLUSH PRIVILEGES;
```

![Figura 3 — Creación de moodle_user y asignación de privilegios sobre moodle_db](imagenes/reto-07/figura-03.png)

*Figura 3 — Creación de `moodle_user` y asignación de privilegios sobre `moodle_db`.*

#### Verificación de permisos del usuario

Compruebo que los permisos se han asignado correctamente:

```sql
SHOW GRANTS FOR 'moodle_user'@'localhost';
```

La salida muestra `GRANT ALL PRIVILEGES ON moodle_db.*`, confirmando que el usuario solo tiene permisos sobre esa base de datos. Salgo del entorno root:

```sql
EXIT;
```

![Figura 4 — Verificación de privilegios del usuario moodle_user](imagenes/reto-07/figura-04.png)

*Figura 4 — Verificación de privilegios del usuario `moodle_user`.*

#### Verificación del acceso con el nuevo usuario

Accedo con las credenciales de `moodle_user` para confirmar que la autenticación funciona correctamente:

```bash
mysql -u moodle_user -p
```

Compruebo que solo tiene visibilidad sobre `moodle_db`:

```sql
SHOW DATABASES;
EXIT;
```

Solo aparecen `moodle_db` e `information_schema`, confirmando que el usuario no tiene acceso a otras bases de datos del sistema.

![Figura 5 — Acceso verificado con moodle_user y permisos limitados correctamente](imagenes/reto-07/figura-05.png)

*Figura 5 — Acceso verificado con `moodle_user` y permisos limitados correctamente.*

### Comprobaciones finales

- [x] Base de datos `moodle_db` creada con codificación `utf8mb4`.
- [x] Usuario `moodle_user` creado con acceso solo desde `localhost`.
- [x] Privilegios completos asignados exclusivamente sobre `moodle_db`.
- [x] `FLUSH PRIVILEGES` ejecutado correctamente.
- [x] `SHOW GRANTS` confirma permisos correctos.
- [x] Acceso verificado con `moodle_user` desde terminal.
- [x] `moodle_user` no tiene visibilidad sobre otras bases de datos del sistema.

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
