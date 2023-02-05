# LPIC-1 Examen 101 - Tópico 2

## Tópico 102: La instalación de Linux y la administración de los paquetes.

- [102.1 Diseño y análisis del disco duro](#1021-diseño-de-la-presentación-del-disco-duro)
- [102.2 Instalar un gestor de arranque](#1022-instalar-un-gestor-de-arranque)
- [102.3 Administrar bibliotecas compartidadas](#1023-administración-de-bibliotecas-compartidas)
- [102.4 Utilizar la gestión de paquetes Debian](#1024-utilice-la-administración-de-los-paquetes-debian)
- [102.5 Utilizar la administración de paquetes RPM y YUM](#1025-utilice-la-administración-del-paquete-rpm-y-yum)
- [102.6 Linux como invitado de virtualización](#1026-linux-as-virtualization-guest)

### 102.1 Diseño de la presentación del disco duro

#### Directorios que constituyen el sistema operativo Linux

- **Directorio `/bin/`**: Comandos Binarios Esenciales para los usuarios del sistema por ejemplo: `cp`,`rm`,`ls`,`pwd`,`mv`.

- **Directorio `/boot/`**: Directorio que contiene los ficheros de configuración de arranque del sistema por ejemplo: `initr`, `vmlinuz`. El núclero se ubica en `/boot` y es en sí un archivo comprimido. De esa manera, se reduce el espacio en disco. Podemos reconocer al kernel dentro de `/boot` por su nombre. Comienza con `vmlinuz` y lo sigue la versión correspondiente.

- **Directorio `/dev/`**: Directorio que contiene las configuraciones de los perifericos del sistema, ejemplo (Disco duro, Floppy, Memorias USB, Reproductores de Audio, etc).

- **Directorio `/etc/`**: Directorio que contiene los ficheros de configuración del sistema en general.

- **Directorio `/home/`**: Contiene los directorios de los usuarios del sistema excepto del superusuario administrador (root): contiene archivos guardados, ajustes personales, etc. Es el directorio de los usuarios estándar, y por lo tanto, el destinado a almacenar todos los archivos del usuario, como documentos, fotos, videos, música, plantillas, etc. También incluye archivos temporales de aplicaciones ejecutadas en modos usuarios, que sirven para guardar las configuraciones de programas, etc.

- **Directorio `/lib/`**: Contiene las librerías compartidas del sistema. Las librerías son archivos que contienen código que puede ser utilizado por otros programas. Por ejemplo, las librerías de audio, de video, de gráficos, etc. Estas librerías son necesarias para que los programas funcionen correctamente.

- **Directorio `/media/`**: Contiene los puntos de montaje de los dispositivos removibles de almacenamiento, como lectores de CD, DVD, memorias USB, etc.

- **Directorio `/mnt/`**: Sistema de archivos montados temporalmente. Sirve para montar discos duros y particiones de forma temporarl en el sistema.

- **Directorio `/opt/`**: Contiene los archivos de programas instalados por el usuario. Por ejemplo, si instalas un programa que no viene con el sistema operativo, como un editor de imágenes, un reproductor de música, etc., se instalará en este directorio.

- **Directorio `/sbin/`**: Sistema Binario. Contiene los archivos binarios de los comandos del sistema. Estos comandos son utilizados por el administrador del sistema, y no por los usuarios estándar. Por ejemplo, `fdisk`, `mkfs`, `reboot`, `shutdown`, etc.

- **Directorio `/srv/`**: Contiene los archivos de los servicios del sistema. Por ejemplo, los archivos de un servidor web, de un servidor de correo, etc.

- **Directorio `/tmp/`**: Contiene archivos temporales. Los archivos temporales son archivos que se crean para ser utilizados por un programa, y que luego son eliminados. Por ejemplo, los archivos temporales de un editor de texto, de un navegador web, etc.

- **Directorio `/usr/`**: Contiene los archivos de los programas del sistema. Por ejemplo, los archivos de los programas de ofimática, de los navegadores web, de los editores de texto, etc.

- **Directorio `/var/`**: Contiene los archivos de datos variables. Por ejemplo, los archivos de registro de los programas, los archivos de configuración de los programas, etc. Archivos variables, tales como logs, archivos spool, bases de datos, archivos de e-mail temporales, y archivos temporales en general. Contiene datos que cambian cuando el sistema se ejecuta normalmente. Es específico para cada sistema y por lo tanto no es compartido a través de la red con otras computadoras.

- Tiene algunos subdirectorios importentes:

  - `/var/lib/`: Contiene archivos que cambian mientras el sistema se ejecuta normalmente. Por ejemplo, los archivos de bases de datos, los archivos de configuración de los programas, etc.

  - `/var/log`: Archivos log, el cual registra todos los inicios y cierres de la sesión en el sistema y de `syslog` (`/var/log/messages`), en donde se almacenan todos los mensajes del núcleo.

- **Directorio `/root/`**: Contiene los archivos del superusuario administrador (root). Es también conocido como el `/home/` del root o superusuario del sistema. A diferencia de otros usuarios que se encuentran todos dentro de un `/home/`. El root tiene sus propias carpetas conectado directamente de la raíz del sistema.

**Comando `df`**: significa Disk Filesystem se usa para chequear el espacio en el disco. Mostrará el almacenamiento disponible y utilizado de los sistemas de archivos en tu máquina.

Al ejecutar el comando, se verán las siguientes columnas:

- `Filesystem`: Nombre del sistema de archivos.
- `Size`: Indica el tamaño total de cada sistema de archivos.
- `Used`: Muestra cuánto espacio está usando cada sistema de archivos.
- `Available`: Muestra cuánto espacio disponible queda en el sistema de archivos.
- `Use%`: Muestra el porcentaje del espacio que está siendo usado.
- `Mounted On`: Indica el punto de montaje de un sistema de archivos.

Añadiendo una serie de opciones al comando df, puedes comprobar el espacio en disco en Linux de forma más precisa. Estas son las opciones más populares:

- `df -h`: te mostrará el resultado en un formato legible por humanos.
- `df -m`: esta línea de comando se utiliza para mostrar la información del uso del sistema de archivos en MB.
- `df -k`: para mostrar el uso del sistema en KB.
- `df -T`: esta opción mostrará el tipo de sistema de archivos (aparecerá una nueva columna).
- `df –ht /home`: te permite ver información de un sistema de archivos específico en un formato legible (en este caso el sistema de archivos /home).
- `df –-help`: listará otros comandos útiles que puedes usar, con sus descripciones.
- `df -l`: limita el listado a los sistemas de archivos locales (particiones).

**Archivo `partitions`**: Es el archivo que contiene las particiones del disco duro. Como las lectoras, disco duro. Este archivo no se refresca automáticamente, para que se actualice debe reiniciarse la computadora.

```bash
cat /proc/partitions
major minor  blocks  name

   7        0     192312 loop0
   7        1     192412 loop1
   7        2          4 loop2
   7        3     119492 loop3
   7        4      56948 loop4
   7        5      56944 loop5
   7        6      64748 loop6
   7        7     119496 loop7
 259        0  500107608 nvme0n1
 259        1     524288 nvme0n1p1
 259        2  499581952 nvme0n1p2
   7        8      74660 loop8
   7        9      74652 loop9
   7       10     596944 loop10
   7       11      84044 loop11
   7       12     191652 loop12
   7       13     191652 loop13
   7       14     456996 loop14
```

Cada línea de este archivo contiene la siguiente información:

- `major`: número de dispositivo mayor.
- `minor`: número de dispositivo menor.
- `blocks`: número de bloques.
- `name`: nombre del dispositivo.

**Comando `mount`**: En Linux siempre necesitaremos acceder al contenido de un sistema de archivo deberemos montarlo (mount) en un directorio del VFS (Virtual File System) llamado "punto de montaje".

Esto resulta de suma utilidad cuando, por ejemplo, necesitamos realizar tareas de mantenimiento y recuperación de datos de un equipo. Podremos iniciar el mismo con GNU/Linux live-cd, y luego acceder a los datos previo montaje de los sistemas de archivos.

```bash
mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,noexec,relatime,size=5009540k,nr_inodes=1252385,mode=755,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,noexec,relatime,size=1012892k,mode=755,inode64)
/dev/nvme0n1p2 on / type ext4 (rw,relatime,errors=remount-ro)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,inode64)
tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k,inode64)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,size=4096k,nr_inodes=1024,mode=755,inode64)
cgroup2 on /sys/fs/cgroup/unified type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
efivarfs on /sys/firmware/efi/efivars type efivarfs (rw,nosuid,nodev,noexec,relatime)
```

Un punto de montaje genérico muy utilizado para este tipo de casos, es el directorio `/mnt` del VFS. Sabiendo el sistema de archivos de la partición, el nombre del dispositivo, y el punto de montaje, podremos montarlo y acceder a sus datos con el comando mount con los argumentos de la siguiente sintaxis:

```bash
mount -t [tipo de sistema de archivos] /dev/[nombre del dispositivo] [punto de montaje]
```

Ejemplo:

```bash
mount -t ext4 /dev/sda1 /mnt
```

**Fichero `/etc/fstab`**: Este fichero contiene la información de los sistemas de archivos que se montan automáticamente al iniciar el sistema. Este fichero se encuentra en el directorio `/etc` y tiene el siguiente formato:

```bash
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
/dev/mapper/centos-root /               xfs     defaults        0 0
UUID=3f3f3f3f-3f3f-3f3f-3f3f-3f3f3f3f3f3f /boot           xfs     defaults        0 0
UUID=3f3f3f3f-3f3f-3f3f-3f3f-3f3f3f3f3f3f swap            swap    defaults        0 0
```

Las particiones usadas en el sistema operativo GNU/Linux para añadirse en el directorio raíz y montar el arranque, son especificadas en el fichero /etc/fstab, donde se almacena la información acerca del montaje de estas particiones.

Si se quiere recargar el fichero FSTAB en Linux sin tener que recurrir al reinicio del sistema, solo debe ejecutarse el comando `mount -a`

### 102.2 Instalar un gestor de arranque.

#### Gestores de Arranque de Linux

Solo se trabajarán `LILO` y `GRUB`, dado que estos son los cargadores de arranque incluidos en la mayoría de las distribuciones de Linux. `LILO` tiene bastantes años de antigüedad, y es el cargador de arranque por defecto en las distribuciones de Linux basadas en Red Hat. `GRUB`, es más reciente, es el cargador de arranque por defecto en las distribuciones de Linux basadas en Debian. El `GRUB` original es ahora lo que se conoce como `GRUB Legacy`, y el `CRUB 2` continúa en proceso bajo el auspicio de la Fundación de Software Libre.

El proceso de instalación de su distribución probablemente le de la opción de elegir qué cargador de arranque instalar. Tanto `GRUB` como `LILO` trabajarán con los discos más modernos, aunque algunas distribuciones, principalmente Fedora, ya no vienen con `LILO`. Recuerde que la tecnología del disco ha avanzado rápidamente, por lo cual siempre debería asegurarse de elegir un cargador de arranque, una distribución de Linux (u otro sistema operativo), y un sistema BIOS, que funcione con su nuevo disco.

**`LILO` (LInux LOader)**: Es uno de los dos cargadores de arranque más comunes de Linux. LILO puede instalarse en el MBR de su unidad de arranque, o en el registro de partición de una partición.

**`GRUB` (GRand Unifood Boot)**: Es el otro de cargador de arranque más común de Linux. Al igual que LILO, GRUB puede instalarse en el MBR de su unidad de arranque, o en el registro de arranque de partición de una partición.

**`GRUB 2`**: Es la versión más reciente de GRUB. GRUB 2 es un cargador de arranque de código abierto, y es el cargador de arranque por defecto en las distribuciones de Linux basadas en Debian. Se volvió a escribir desde scratch (desde cero) para hacerlo mucho más portátil y con más módulos. Éste apunta a arquitecturas y métodos de arranque diferentes y posee muchas características nuevas.

```bash
dpkg -L grub-pc | grep "bin/"
/usr/sbin/upgrade-from-grub-legacy
/usr/bin/grub-ntldr-img
/usr/sbin/grub-bios-setup
```

### 102.3 Administración de bibliotecas compartidas.

** Comando `ldd`**: Con este comando `ldd` se puede ver las bibliotecas compartidas que utiliza un programa. Por ejemplo, para ver las bibliotecas compartidas que utiliza el programa `ls`:

```bash
ldd /bin/ls
linux-vdso.so.1 (0x00007ffe5ed8b000)
libselinux.so.1 => /lib/x86_64-linux-gnu/libselinux.so.1 (0x00007f3bb15e4000)
libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f3bb13f8000)
libpcre2-8.so.0 => /lib/x86_64-linux-gnu/libpcre2-8.so.0 (0x00007f3bb1361000)
libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007f3bb135a000)
/lib64/ld-linux-x86-64.so.2 (0x00007f3bb1658000)
libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f3bb1338000)
```

**Importante**: `.so` o `.o` son las extensiones de los archivos utilizados por los sistemas operativos Unix para almacenar código compartido. Los archivos `.so` son archivos compartidos de bibliotecas dinámicas, mientras que los archivos `.o` son archivos compartidos de bibliotecas estáticas.

**Comando `ldconfig`**: Actualiza las librerías utilizadas por el sistema, recomendable ejecutarlo cada vez que se instala un programa.

```bash
ldconfig
```

**Archivo `/etc/ld.so.conf`**: Se tiene la carga de librerías que necesita el programa.

```bash
cat /etc/ld.so.conf
include /etc/ld.so.conf.d/*.conf
```

**LD_LIBRARY_PATH**: Es la variable de entorno predefinida en Linux / Unix que establece la ruta a la que debe mirar el vinculador al vincular bibliotecas dinámicas / bibliotecas compartidas.

Contiene la lista de rutas separadas por dos puntos y el enlazador da prioridad a estas rutas sobre las rutas de biblioteca estándar `/lib` y `/usr/lib`. Se seguiran buscando las rutas estándar, pero solo después de que se haya agotado la lista de rutas en `LD_LIBRARY_PATH`.

```bash
echo $LD_LIBRARY_PATH
```

```bash
export LD_LIBRARY_PATH="/list/of/library/paths:/another/path" $ ./program
```

Inicialmente el kernel se subdivide en dos grandes sistemas operativos base:

- `REDHAT`
- `DEBIAN`

A su vez, cada uno de estos sistemas operativos base se divide en varias distribuciones, las cuales son:

- `REDHAT`:

  - `Fedora`
  - `CentOS`
  - `RHEL`
  - `Scientific Linux`
  - `Oracle Linux`

- `DEBIAN`:
  - `UBUNTU`
  - `LINUX MINT`
  - `KALI`

Cada derivado de `REDHAT` y `DEBIAN` tiene su propio administrador de paquetes, para el caso de `REDHAT`, trabaja con `rpm`, y para el caso de `DEBIAN`, el gestor de paquetes `apt`.

Existen dos problemas con los gestores de paquetes (Errores):

- Errores de dependencia: Cuando un paquete depende de otro paquete que no está instalado, está instala pero no está actualizado, está instalado pero no es la versión correcta o hay un conflicto entre dos paquetes.

- Errores de Conflicto de archivos: Cuando dos paquetes intentan instalar el mismo archivo, pero con diferentes contenidos.

**Nota**: Gestor de Versiones del Kernel [kernel.org](https://www.kernel.org/)

**Repositorio de archivos**: Es un conjunto de archivos que se encuentran en un servidor web, que se pueden descargar y utilizar en un sistema operativo. Los repositorios de archivos se utilizan para instalar programas en sistemas operativos basados en Linux.

**Nota**: Rutas donde estan almacenados los repositorios de archivos.

- **RedHat**: `/etc/yum.repos.d/`
- **Debian**: `/etc/apt/sources.list`

`Epel` es un repositorio de software libre y de código abierto para Red Hat Enterprise Linux, Fedora y derivados. El repositorio contiene software que no está disponible en los repositorios oficiales de Red Hat, Fedora o CentOS.

`RPM-Fusion` es un repositorio de software libre y de código abierto para Red Hat Enterprise Linux, Fedora y derivados. El repositorio contiene software que no está disponible en los repositorios oficiales de Red Hat, Fedora o CentOS.

Categorias de los repositorios:

- `Base`: Contiene los paquetes básicos para el funcionamiento del sistema operativo.
- `Updates`: Contiene los paquetes actualizados del sistema operativo.
- `Extras`: Contiene los paquetes adicionales para el sistema operativo.

**Nota**: Hay paquetes que a veces no se descargan con el oficial, por lo que se debe agregar un repositorio de terceros. como por ejemplo `lp-ppa` (Linux Uprising PPA)

```bash
sudo add-apt-repository ppa:linuxuprising/java
```

### 102.4 Utilice la Administración de los paquetes Debian

**Nota**: Revisar información de las distribuciones en [DistroWatch](https://distrowatch.com/)

Ubicaciones de los paquetes. El comando`apt-get` leyó una lista de paquetes de algún lado. Este lugar suele ser `/etc/apt/sources.list`. La lista le indica a `apt-get` donde buscar los paquetes (incluso en un CD-ROM en su sistema de archivos local o en una red). Usted tiene la posibilidad de agregar fuentes adicionales en el directorio `/etc/apt/sources.list.d/`.

```bash
cat /etc/apt/sources.list
# deb cdrom:[Kubuntu 21.04 _Hirsute Hippo_ - Release amd64 (20210420)]/ hirsute main multiverse restricted universe

# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb http://br.archive.ubuntu.com/ubuntu/ hirsute main restricted
# deb-src http://br.archive.ubuntu.com/ubuntu/ hirsute main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://br.archive.ubuntu.com/ubuntu/ hirsute-updates main restricted
# deb-src http://br.archive.ubuntu.com/ubuntu/ hirsute-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb http://br.archive.ubuntu.com/ubuntu/ hirsute universe
```

**Eliminación de paquetes Debian**: Para eliminar un paquete, se utiliza el comando `apt-get remove` seguido del nombre del paquete.

```bash
apt-get remove <nombre_paquete>
```

**Actualización de paquetes Debian**: Para actualizar un paquete, se utiliza el comando `apt-get update` seguido del nombre del paquete o utilizar la opción `apt-get install` nuevamente.

```bash
apt-get update <nombre_paquete>
or
apt-get install <nombre_paquete>
```

**Configuración de la `APT`. El archivo `apt.conf`**: Si usa el comando `apt-get` en repetidas ocaciones y las opciones predeterminadas que encuentra no son de su agrado, usted puede configurar nuevas opciones predeterminadas en `/etc/apt/apt.conf`. Un programa, `apt-config`, está disponible para que los scripts consulten el archivo `apt.conf`.

**Reconfiguración de paquete Debian**: La APT incluye una capacidad denominada `debconf`, que se usa para configurar paquetes luego de su instalación. Es posible reconfigurar los paquetes que usan esta capacidad (y no todos lo hacen) luego de su instalación. La forma más fácil de hacer esto usando el comando `dpkg-reconfigure` seguido del nombre del paquete.

```bash
dpkg-reconfigure <nombre_paquete>
```

**Estado del paquete con dpkg**: Otra herramienta que forma parte del sistema APT es dpkg. Se trata de una herramienta de gestión de paquetes de nivel medio que puede instalar y eliminar paquetes y visualizar la información de estado correspondiente `/etc/dpkg/dpkg.cfg` puede controlar la configuración de `dpkg`. Además, es posible que usted también tenga un archivo `dpkg.cfg` en su directorio principal para realizar una configuración más avanzada. La herramienta `dpkg` usa muchos archivos en el árbol `/var/lib/dpkg` en su sistema de archivos. En particular, el archivo `/var/lib/dpkg/status` incluye información sobre el estado de los paquetes que se encuentran en su sistema.

**Nota**: Para ver la lista de paquetes instalados en el sistema, se utiliza el comando `dpkg -l`.

```bash
dpkg -l <nombre_paquete>
```

**Uso de "aptitude"**: Es una interfaz de texto para el sistema de paquetes de Debian GNU/Linux. Permite al usuario ver la lista de paquetes y realizar tareas de gestión tales como instalar, actualizar o eliminar paquetes. Puede llevar a cabo las acciones con una interfaz gráfica o en la línea de órdenes.

```bash
aptitude [opciones...] {autoclean | clean | forget-new | keep-all | update}
```

**Nota**: Para ver la lista de paquetes instalados en el sistema, se utiliza el comando `aptitude search`.

```bash
aptitude search <nombre_paquete>
```

|           Opciones           | Se utiliza con las acciones | Descripción                                                                                                                                                                                                                       |
| :--------------------------: | :-------------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|         `--root=dir`         |            Todas            | Modifica el sistema Linux utilizando un directorio raíz que se encuentra en `dir`. Se puede utilizar para mantener una instalación de Linux independiente de otra, por ejemplo, durante la instalación del SO o un mantenimiento. |
| `-B` o `--auto-deconfigure`  |            `-r`             | Desactiva los paquetes que se basan en el que se está eliminando.                                                                                                                                                                 |
|       `--force-action`       |          Diversas           | Obliga a realizar acciones específicas. Consulte la página `man` de `dpkg` para ver el detalle de las cosas que hace esta opción.                                                                                                 |
|  `--ignore-depends=package`  |           `-i,-r`           | Ignora la información de dependencia para el paquete especificado.                                                                                                                                                                |
|          `--no-act`          |           `-i,-r`           | Verifica las dependencias, los conflictos y otros problemas sin instalar o eliminar realmente el paquete.                                                                                                                         |
|        `--recursive`         |            `-i`             | Instala todos los paquetes que coinciden con el comodín del nombre de paquete del directorio especificado y todos sus subdirectorios.                                                                                             |
|             `-G`             |            `-i`             | No instala el paquete si ya hay instalada una versión más reciente del mismo paquete.                                                                                                                                             |
| `-E` o `--skip-same-version` |            `-i`             | No instala el paquete si ya se encuentra instalada la misma versión de este.                                                                                                                                                      |

Funciones de los parámetros del comando `dpkg`:

|         Sintaxis         | Descripción                                                                                                              |            Ejemplo            |
| :----------------------: | ------------------------------------------------------------------------------------------------------------------------ | :---------------------------: |
| `dpkg -i {.deb paquete}  | Instala el paquete                                                                                                       | `dpkg -i zip_2.31-3_i386.deb` |
|   `dpkg -r {paquete}`    | Elimina el paquete                                                                                                       |         `dpkg -r zip`         |
|   `dpkg -P {paquete}`    | Elimina el paquete y sus archivos de configuración                                                                       |         `dpkg -P zip`         |
|        `dpkg -l`         | Muestra un listado de todos los paquetes instalados, así mismo muestra la versión del paquete y una pequeña descripción. |           `dpkg -l`           |
|   `dpkg -L {paquete}`    | Muestra los archivos que pertenecen al paquete                                                                           |         `dpkg -L zip`         |
| `dpkg -c {.Deb paquete}` | Muestra los archivos que contiene el paquete                                                                             | `dpkg -c zip_2.31-3_i386.deb` |

Obtiene la lista de paquetes del sistema

```bash
dpkg --get-selections
```

Un poco más amplio es el comando apt list, el cual nos muestra la lista de paquetes disponibles para instalar.

```bash
apt list | grep -i <nombre_paquete>
```

#### Colocar internet a la máquina virtual Ubuntu

1. Primero se debe pasar la maquina virtual a una máquina que tenga internet, modo dinámico.

Dispositivos > Red > Adaptador 1 > Conectado a > Red NAT.
Dispositivos > Red > Adaptador 1 > Modo Promiscuo > Permitir Todo.

2. Colocar la IP estática en la máquina virtual.

```bash
cd /etc/netplan
nano 00-installer-config.yaml
```

```yml
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: true
      addresses: [192.168.100.80/24]
      gateway4: 192.168.100.1
      nameservers:
        addresses: [192.168.100.50]
```

3. Reiniciar la máquina virtual.

```bash
reboot
```

4. Verificar la conexión a internet.

```bash
ping google.com
```

### 102.5 Utilice la administración del paquete `RPM` y `YUM`.

#### Introducción a la administración de paquetes

**Red Hat Package Manager (RPM)**, desarrollado por by Red Hat, y del **Yellowdog Updater, Modified (YUM)**, originalmente desarrollado para administrar los sistemas Red Hat Linux en el Departamento de Física de la Universidad Duke.

Al instalar un sistema Linux, por lo general usted puede instalar una gran variedad de paquetes. El set puede personalizarse según el uso que se quiera dar al sistema, como servidor, escritorio, o terminal de trabajo del desarrollador. Y en algún momento probablemente sea necesario instalar paquetes nuevos para obtener alguna otra funcionalidad, actualizar el paqeute que posee, o incluso borrar paquetes que ya no se necesitan o son obsoleto debido a la aparición de nuevos paquetes.

**RPM**: Red Hat lanzó RPM en 1995. Actualmente RPM es el sistema de gestión de paquetes usado para crear paquetes en Linux Standard Base (LBS). Las opciones del rpm están agrupadas en 3 grandes subgrupos según su uso:

- Consultar y verificar paquetes.
- Instalar, actualizar y eliminar paquetes.
- Realizar varias funciones

**YUM**: YUM agrega la actualización automática y la administración de paquetes, incluyendo la administración de la dependencia, a los sistemas RPM. Además de comprender los paquetes instalados un sistema, YUM, al igual que Debian Advanced empaquetado Tool (DAPT), trabaja con depósitos, los cuales son recopilaciones de paquetes, generalmentes accesibles mediante la conexión de red.

Comandos básicos de YUM

|                Sintaxis                 | Descripción                                                                                                                                                                                                                                                                                                       |                                                  Ejemplo                                                   |
| :-------------------------------------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------: | --- |
|         `yum install {paquete}`         | Instala la última versión del paquete indicado. Pide confirmación                                                                                                                                                                                                                                                 |                                             `yum install zip`                                              |
|       `yum -y install {paquete}`        | Instala la última versión del paquete indicado. No pide confirmación                                                                                                                                                                                                                                              |                                            `yum -y install zip`                                            |
| `yum -y install {paquete1} {paquete2}`  | Instala la última versión de los paquetes indicados. No pide confirmación                                                                                                                                                                                                                                         |                                         `yum -y install zip unzip`                                         |
|      `yum -y install paquete.arch`      | Instala la última versión del paquete indicado con la arquitectura indicada                                                                                                                                                                                                                                       |                                           `yum install mysql.i3`                                           |
|             `yum -y update`             | Actualiza todos los paquetes en el sistema.                                                                                                                                                                                                                                                                       |
|   `yum -y update --exclude={paquete}`   | Actualiza todos los paquetes en el sistema, excepto el indicado.                                                                                                                                                                                                                                                  |                                       `yum -y update --exclude=zip`                                        |
|        `yum -y update {paquete}`        | Actualiza el paquete indicado.                                                                                                                                                                                                                                                                                    |                                           `yum -y update httpd`                                            |
|  `yum -y update {paquete1} {paquete2}`  | Actualiza los paquetes indicados.                                                                                                                                                                                                                                                                                 |                                         `yum -y update httpd zip`                                          |
| `yum -y update --enablerepo=centosplus` | Actualiza todos los paquetes en el sistema, incluyendo los de centosplus.                                                                                                                                                                                                                                         |                                                                                                            |
|            `yum -y upgrade`             | Actualiza los paquetes indicados, pero tomando en cuenta paquetes obsoletos en el cálculo de la actualización. Esta opción es idéntica a `yum -y --obsoletes update` y solo es realmente útil cuando se actualizan paquetes a través de distintas versiones de la distribución, por ejemplo de centos4 a centos5. |                                                                                                            |
|           `yum check-update`            | Muestra una lista de paquetes que necesitan ser actualizados sin instalarlos                                                                                                                                                                                                                                      |                                                                                                            |
|          `yum info {paquete}`           | Muestra información sobre el paquete indicado.                                                                                                                                                                                                                                                                    |                                              `yum info httpd`                                              |
|            `yum info recent`            | Muestra información resumida de los últimos paquetes instalados o actualizados.                                                                                                                                                                                                                                   |                                                                                                            |
|          `yum info available`           | Muestra información resumida de los paquetes disponibles para instalar.                                                                                                                                                                                                                                           |                                                                                                            |
|               `yum list`                | Muestra una lista de todos los paquetes disponibles para instalar.                                                                                                                                                                                                                                                |                                                                                                            |
|                `yum list                | grep -i {palabra clave}`                                                                                                                                                                                                                                                                                          | Muestra una lista de todos los paquetes disponibles para instalar que contengan la palabra clave indicada. |     |
|          `yum list installed`           | Muestra una lista de todos los paquetes instalados.                                                                                                                                                                                                                                                               |                                                                                                            |

**Licencia GPL**: la Licencia Pública General de GNU o más conocida por su nombre en inglés GNU General Public License es una licencia de derecho de autor ampliamente usada en el mundo del software libre y código abierto, ​ y garantiza a los usuarios finales la libertad de usar, estudiar, compartir y modificar el software.

**Licencia LGPL**: LGPL (GNU Lesser General Public License en español Licencia Pública General Reducida de GNU) es una licencia de software libre publicada por la Free Software Foundation. LGPL es una alternativa más permisiva que la estricta licencia copyleft GPL.

Esto supone que cualquier trabajo que use un elemento con licencia GPL tiene la obligación de ser publicado bajo las mismas condiciones (libre de usar, compartir, estudiar, y modificar). Por otro lado, LGPL solo requiere que los componentes derivados del elemento bajo LGPL continuen con esta licencia, y no el programa al completo.

[Ver más al respecto](https://youtu.be/S1koh3QllQg)

**Directorio /etc/yum.repos.d**: es el directorio donde se almacenan los archivos de configuración de los repositorios de paquetes de CentOS.

```bash
yum repolist
```

**RPM2CPIO**: Es un comando que permite extraer los archivos de un paquete RPM. Si usted descarga un RPM y necesita examinar su contenido, en lugar de instalarlo, puede usar el comando `rpm2cpio` para convertir los contenidos de un archivo cpio y luego filtrarlo a través del comando cpio para extraer los archivos del paquetes de manera individual a todos los archivos juntos.

**Instalación**: `sudo apt-get install rpm2cpio -y`

```bash
rpm2cpio paquete.rpm | cpio -idmv
```

**Estructura de un paquete RPM**

`<paquete>-<version>-<release>.<arquitectura>.rpm`

#### Colocar internet a la máquina virtual CentOS

1. Primero se debe pasar la maquina virtual a una máquina que tenga internet, modo dinámico.

Dispositivos > Red > Adaptador 1 > Conectado a > Red NAT.
Dispositivos > Red > Adaptador 1 > Modo Promiscuo > Permitir Todo.

2. Colocar la IP estática en la máquina virtual.

```bash
cd /etc/sysconfig/network-scripts
nano ifcfg-enp0s3
```

```bash
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=static
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s3
UUID=3c7b0b5e-8b5e-4b5e-8b5e-4b5e8b5e4b5e
DEVICE=enp0s3
ONBOOT=yes
IPADDR=
NETMASK=
GATEWAY=
DNS1=
```

más información: https://serverspace.io/es/support/help/multiple-network-interfaces-centos-7/

### 102.6 Linux as virtualization guest

#### Descripción general de virtualización

La virtualización es una tecnología que permite que una plataforma de software, llamada hipervisor, ejecute processos que contienen un sistema informático completamente emulado. El hipervisor es responsable de administrar los recursos del hardware físico que pueden ser utilizados por máquinas virtuales individuales. Estas máquinas virtuales se llaman invitados del hipervisor. Una máquina virtual tiene muchos aspectos de una computadora física emulada en un software, como el BIOS del sistema y los controladores de disco del dusco duro. Una máquina virtual a menudo usará imágenes de disco duro que se almacenan como archivos individuales y tendrá acceso a la RAM y CPU de la máquina host a través del software del hipervisor. El hipervisor separa el acceso a los recursos de hardware del sistema host entre los invitados, lo que permite que múltiples sistemas operativos se ejecuten en un solo sistema host.

#### Los hipervisores de uso común para Linux incluyen:

- **XEN**: Xen es un hipervisor de tipo 1 de código abierto, lo que significa que no depende de un sistema operativo subyacente para funcionar. Un hipervisor de este tipo se conoce como un hipervisor de metal desnudo ya que la computadora puede arrancar directamente en el hipervisor.

- **KVM**: Kernel Virtual Machine es un subsistema de kernel de Linyx para virtualización. KVM es un hipervisor de tipo 2, ya qeu se basa en el sistema operativo Linux y se ejecuta para que se use este software. Las máquinas virtuales implementadas con KVM utilizan el libvirt demonio y las utilizades de software asociadas para crear y administrar máquinas virtuales.

- **VirtualBox**: VirtualBox es un hipervisor de tipo 2 que se ejecuta como un programa en el sistema operativo Linux. VirtualBox es un software de código abierto que se puede descargar y usar de forma gratuita. VirtualBox es compatible con Linux, Windows, Mac OS X, Solaris y OpenSolaris.

**Tipos de máquinas virtuales**

- **Totalmente virtualizado**: Todas las instrucciones que se espera que ejecute un sistema operativo invitado deben poder ejecutarse dentro de una instalación de sistema operativo totalmente virtualizada.

- **Paravirtualizado**: Es aquel en el que el sistema operativo invitado no es consciente de que se trata de una instancia de máquina virtual en ejecución.

Referencias:
https://www.ibm.com/mx-es/cloud/learn/hypervisors
https://kryptonsolid.com/cual-es-la-diferencia-entre-el-hipervisor-tipo-1-y-el-tipo-2/
https://www.redhat.com/es/topics/virtualization/what-is-a-hypervisor
https://es.wikipedia.org/wiki/Hipervisor
https://www.nutanix.com/mx/info/hypervisor
https://www.muycomputer.com/2020/03/27/hipervisor-virtualbox-vmware-hyperv/


#### SSH Host Key

En SSH, se utiliza un par de claves, llamadas claves de host, para identificar una computadora. El propósito del par de claves SSH es para autenticar computadoras. Las claves de host son únicas y se generan utilizando algoritmos de cifrado asimétrico como los algoritmos RSA, DSA o ECDSA. Las claves de host públicas se distribuyen a los clientes SSH y las claves privadas se almacenan en los servidores SSH.

Cuando un cliente SSH se conecta a un servidor SSH, la clave de host del servidor SSH se almacena en un archivo, denominado claves de host conocidas

En Unix/Linux OpenSSH, la colección de claves de host conocidas se almacena en `/etc/ssh/know_hosts` y en `.ssh/known_hosts` en el directorio del usuario.

`know_hosts` es un archivo fantasma, que es un archivo que no se puede editar directamente. El archivo `know_hosts` se crea automáticamente cuando se conecta por primera vez a un servidor SSH. El archivo `know_hosts` se puede editar utilizando el comando `ssh-keygen` o `ssh-keyscan`.

**Machine - ID**: El archivo `/etc/machine-id` contiene la ID de máquina única del sistema local que se configura durante la instalación o arranque. La ID de la máquina es una sola ID en minúsculsa, hexadecimal, de 32 caracteres y terminada en una nueva línea. Cuando se decodifica de hexadecimal, esto corresponde a un valor de 16 bytes/128 bits. Este ID puede no ser todos ceros.

Actividades complementarias:

- [Realizar el examen del tópico 2](https://www.goconqr.com/es/quiz/11854057/examen-101-lpi-chapter-2-managing-software)
- [Práctica de ejercicios del tópico 2](laboratorio-2.md)
