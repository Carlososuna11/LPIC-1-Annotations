# LPIC-1 Examen 101 - Tópico 4

## Tópico 103: Dispositivos, sistemas de archivos Linux, Estándar de jerarquía del sistema de archivos

Comprende los siguientes ítems:

- 104.1 Crear Particiones y Sistemas de Archivos.
- 104.2 Mantener la integridad de los sistemas de Archivos.
- 104.3 Control de Montaje y desmontaje de sistemas de archivos.
- 104.4 Administración de Archvios y Propiedad.
- 104.5 Crear y Cambiar enlaces duros y simbólicos.
- 104.6 Buscar Archivos del Sistema y Colocarlos en la ubicación correcta.

### 104.1 Crear Particiones y Sistemas de Archivos

- Un sistema de archivos es un conjunto de normas y procedimientos para almacenar la información. Todo sistema operativo tiene uno.

- Un archivo es un conjunto independiente de datos, como una foto o un texto. Hay diferentes tipos de archvio como veremos más adelante. Toda la información que hay en una computadora está agrupada en forma de archivos.

- Cada sistema operativo suele usar un sistema de archivos diferente. Pero todos comparten otro concepto: La carpeta. Una carpeta es una manera de agrupar libremente archivos. Las carpetas también se conocen como directorios.

| Sistema Operativo | Tipos de Sistemas de Archivos Admitidos                                      |
| ----------------- | ---------------------------------------------------------------------------- |
| DOS               | FAT16                                                                        |
| Windows 95        | FAT16                                                                        |
| Windows 95 OSR2   | FAT16, FAT32                                                                 |
| Windows 98        | FAT16, FAT32                                                                 |
| Windows NT4       | FAT, NTFS (Versión 4)                                                        |
| Windows 2000/XP   | FAT, FAT16, FAT32, NTFS (Veriones 4 y 5)                                     |
| Linux             | Ext2, Ext3, ReiserFS, Linux Swap (FAT16, FAT32, NTFS)                        |
| MacOS             | HFS (Sistema de Archivos Jerárquico), MFS ( Sistemas de Archivos Machintosh) |
| OS/2              | HPFS (Sistema de Archivos de Alto Rendimiento)                               |
| SGI IRIX          | XFS (Sistema de Archivos de Extensión)                                       |
| FreeBSD, OpenBSD  | UFS (Sistema de Archivos Unix)                                               |
| Sun Solaris       | UFS (Sistema de Archivos Unix)                                               |
| IBM AIX           | JFS (Sistema de Archivos de Java)                                            |

#### Comando Linux `mkfs`

- Se utiliza para dar formato a un dispositivo de almacenamiento de bloque con un determinado sistema de archivos.

- Un sistema de archivos es la estructura básica de todos los datos que se guarda, edita, borra o copia, etc... en la PC, siendo toda la información accedida a través de gestores de archivos en sus respectivos SO.

Sintaxis

```bash
mkfs [OPCIONES] [TIPO] [DISPOSITIVO] [TAMAÑO]
```

Ejemplos prácticos mkfs:

```bash
# Formatear un disco duro
mkfs /dev/sda
mkfs -t ext4 /dev/sdd1
mke2fs -t ext4 /dev/sdb
```

#### Comando `mkswap`

- Genera una zona swap (intercambio) en un dispositivo de almacenamiento de bloque. Opciones básicas:
  - `-c`: Hace un chequeo de la unidad para buscar bloques defectuosos antes de crear la zona swap.
  - `-L`: Label permite especificar un nombre a la zona

**`swapon -a`** Permite activar una zona swap
**`swapoff -a`** Permite desactivar una zona swap

### 104.2 Mantener la Integridad de los Sistemas Operativos

#### Comando `du`

El comando `du` (Abreviatura de uso de disco) es un comando útil que se utiliza para encontrar el uso del disco para archivos y directorios. `du` se utiliza con varias opciones proporcionando resultados en muchos formatos. Algunos de los ejemplos se mencionan a continuación:

- Para conocer el resumen del uso del disco para un directorio con todos sus subdirectorios:

```bash
du -sh /home
```

#### Comando `df`

El comando `df` (Abreviatura de sistema de archivos en disco) se utiliza para mostrar la utilización del disco para un sistema Linux. Algunos ejemplos se comparten a continuación. Para mostrar información del nombre del dispositivo, totales de espacio, total en disco, bloque de espacioo e disco usado y puntos de montaje.

#### Comando `fsck`

es una utilidad muy importante de Linux/Unix, se usa para verificar y reparar los errores en el sistema de archivos. Está disponible para sistemas operativos Linux, MacOS, FreeBSD.

FSCK significa Verificación de Consistencia del Sistema de Archivos y la mayoría de las veces, se ejecuta en el momento del arranque, pero también puede ser iniciado manualmente por un superusuario, si es necesario.

Puede ser utilizado con 3 modos de operación,

1. Comprobar si hay errores y dejeque el usuario decida qué se debe hacer con cada error,
2. Verificar errores y hacer reparaciones automáticamente.
3. Comprobar si hay errores y visualice el error, pero no realiza ninguna reparación.

Sintaxis para el uso de `fsck`

Podemos usar el comando `fsck` manualmente con la siguiente sintatix,

```bash
fsck [OPCIONES] [SISTEMA DE ARCHIVOS] [DISPOSITIVO]
```

Opciones:

- `-p`: Realiza una comprobación de la consistencia del sistema de archivos y la reparación de errores.
- `-n`: No hacer cambios en el sistema de archivos.
- `-y`: Asumen el `si` a todas las preguntas.
- `-c`: Comprueba si hay bloques defectuosos y los agrega a la lista de badblock.
- `-f`: Forzar la comprobación incluso si el sistema de archivos está marcado como limpio.
- `-v`: Ser verboso.
- `-b`: Superblock Utiliza superbloqueo alternativo.
- `-B`: Tamaño de bloque fuerza tamaño de bloque cuando se busca un superbloque.
- `-j`: external_journal. Establece la ubicación del archivo journal.
- `-l`: Lista de badblocks. Establece la ubicación de la lista de badblocks.
- `-t`: Tipo de sistema de archivos. Establece el tipo de sistema de archivos.

#### Comando `tune2fs`

Permite modificar los parámetros de los sistemas de ficheros `ext2/ext3/ext4`.

Ejemplos:

- `tune2fs -l /dev/hda1`: Muestra información de la partición igual que `dumpe2fs -h`.
- `tune2fs -c 50 /dev/hda1`: Cuando se haya montado 50 veces, realizará una comprobación `fsck`.
- `tune2fs -c -1 /dev/hda1`: Desactiva la comprobación `fsck` automática.
- `tune2fs -i 10[d|m|w] /dev/hda1`: Cuando se hayan pasado 10 [días|meses|semanas], realizará una comprobación `fsck`.
- `tune2fs -i 0 /dev/hda1`: Desactiva la comprobación `fsck` por tiempo.

#### Comando `xfs_repair`

Es una utilidad disponible en cualquier sistema que utilice `xfs` y que permite analizar y reparar estos sistemas de ficheros. La gran diferencia respecto a `fsck` es que esta utilidad no se tiene que utilizar durante el arranque del sistema, incluso si el sistema de ficheros no se ha desmontado de forma correcta previamente.

Ejemplo

```bash
xfs_repair -L /dev/sda1
```

### 104.3 Control de Montaje y Desmontaje de Sistemas de Archivos

El sistema de archivo

#### `/etc/fstab`

Este es el archivo de configuración de los sistemas operativos compatibles con UNIX donde se encuentra la configuración de los diferentes sistemas de archivo y particiones

|     Dispositivo     | Punto de Montaje | Tipo de Archivo de Sistema | Opciones de Montaje | Volcado             | Número enviado a `fsck` |
| :-----------------: | :--------------- | :------------------------- | :------------------ | :------------------ | :---------------------- | --- |
|     `/dev/sda1`     | `/`              | `ext2`                     | `exec,dev,suid,rw`  | `1`                 | `1`                     |
|       `none`        | `/proc`          | `proc`                     | `exec,dev,suid,rw`  | `1`                 | `1`                     |
|       `none`        | `/dev/pts`       | `devpts`                   | `gid=4, mode=320`   | `0`                 | `0`                     |
|     `/dev/sda2`     | `none`           | `swap`                     | `pri=1, rw,sw`      | `1`                 | `1`                     |
|     `/dev/sdb1`     | `none`           | `swap`                     | `pri=1, rw,sw`      | `1`                 | `1`                     |
|  `/dev/sysvg0/usr`  | `/usr`           | `ext3`                     | `exec,suid,rw`      | `1`                 | `2`                     |
|  `/dev/sysvg0/var`  | `/var`           | `ext3`                     | `noexec,rw`         | `1`                 | `2`                     |
|  `/dev/sysvg0/tmp`  | `/tmp`           | `ext3`                     | `noexec,rw`         | `1`                 | `2`                     |
| `/dev/mirror0/home` | `/home`          | `xfs`                      | `rw`                | `1`                 | `2`                     |
|    `/dev/mirror0    | ldap`            | `/var/ldap`                | `ext3`              | `noexec,noatime,rw` | `1`                     | `2` |

#### Comando `lsblk`

Nos muestra información de todos los dispositivos de bloque (Disco duros, SSD, memorias flash, CD-ROM, etc) que forman parte del hardware de nuestra PC.

Aqui tenemis su forma más sencilla de ejecución: El nombre del programa y sin necesidad de privilegios de root.

Ejemplo:

```bash
lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0         7:0    0 187.9M  1 loop /snap/alfacast/44
loop1         7:1    0 187.8M  1 loop /snap/alfacast/41
loop2         7:2    0   105M  1 loop /snap/android-file-transfer-linux/199
loop3         7:3    0 116.7M  1 loop /snap/core/14399
loop4         7:4    0 116.7M  1 loop /snap/core/14447
loop5         7:5    0     4K  1 loop /snap/bare/5
loop6         7:6    0  63.2M  1 loop /snap/core20/1738
loop7         7:7    0  55.6M  1 loop /snap/core18/2679
loop8         7:8    0  55.6M  1 loop /snap/core18/2667
loop9         7:9    0 246.6M  1 loop /snap/dotnet-sdk/191
loop10        7:10   0 246.6M  1 loop /snap/dotnet-sdk/190
```

#### Comando `/sbin/blkid`

Nos muestra una lista de particiones con información tal como:

- Nombre del dispositivo de bloque
- UUID (Universally Unique Identifier)
- Etiqueta
- Tipo de sistema de archivos

Esto es bastante util en nuevas distribuciones Linux que hacen referencia a un dispositivo de bloque por UUID o LABEL.

Bien aquí un ejemplo:

```bash
sudo blkid

/dev/sda1: LABEL="boot" UUID="f9f9-4b4b" TYPE="vfat" PARTUUID="f9f9-4b4b"
/dev/sda2: UUID="f9f9-4b4b" TYPE="swap" PARTUUID="f9f9-4b4b"
```

### 104.4 Administrar Permisos de Archivos y Propiedad

#### Comando `chmod`

Es un comando que nos permite cambiar los permisos de un archivo o directorio.

Chmod - Modo Octal

| Número | Binario | Lectura (r) | Escritura (w) | Ejecución (x) |
| :----- | :------ | :---------- | :------------ | :------------ |
| 0      | 000     |             |               |               |
| 1      | 001     |             |               | x             |
| 2      | 010     |             | w             |               |
| 3      | 011     |             | w             | x             |
| 4      | 100     | r           |               |               |
| 5      | 101     | r           |               | x             |
| 6      | 110     | r           | w             |               |
| 7      | 111     | r           | w             | x             |

propietario - grupo - otros

```bash
# Acceso total al propietario, lectura y escritura al grupo y otros
chmod 766 /home/usuario/archivo.txt
```

```bash
# Acceso total al propietario y al grupo y elimina todos los permisos a los demás usuarios
chmod 770 /home/usuario/archivo.txt
```

```bash
# Lectura y escritura al propietario, escritura y ejecución al grupo, y lectura y ejecución al resto
chmod 635 /home/usuario/archivo.txt
```

#### Cambiando Usuario y Grupo

Comandos

- `chown` (Change Owner) - Cambia el propietario de un archivo o directorio
- `chgrp` (Change Group) - Cambia el grupo de un archivo o directorio

```bash
# Cambia el propietario del archivo.txt al usuario usuario
chown usuario /home/usuario/archivo.txt
```

```bash

# Cambia el grupo del archivo.txt al grupo grupo
chgrp grupo /home/usuario/archivo.txt
```

Además al igual que con `chmod` podemos usar el comando `chown` y `chgrp` con el parámetro `-R` para aplicar los cambios de forma recursiva.

### 104.5 Crear y Cambiar Enlaces Duros y Simbólicos

<center><img src="https://imgur.com/JzKFhRq.png"></center>

#### Enlaces Duros

Para entender lo que es un enlace duro, lo primero que tenemos que saber es que en Linux cada fichero y cada carpeta del sistema operativo tienen asignado un número entero llamado `inodo`.

- Este inodo es único para cada uno de los archivos y cada una de las carpetas.
- La información que almacena cada uno de los inodos de los distintos archivos y carpetas es la siguiente:

  - Los permisos del archivo o carpeta.
  - El propietario del fichero y carpeta.
  - **La posición/ubicación del archivo** o de la carpeta de nuestro disco duro.
  - La fecha de creación del archivo o directorio.

Para comprender bien lo qeu es un enlace duro crearemos un archivo de texto ejecutando el siguiente comando en la terminal:

```bash
echo "Hola mundo" > archivo.txt
```

Una vez creado el archivo vamos a consultar su número de inodo ejecutando el siguiente comando de la terminal:

```bash
ls -li archivo.txt

131072 -rw-r--r-- 2 usuario usuario 11 nov  9 20:00 archivo.txt
```

Por lo tanto el inodo del archivo que acabamos de crear es el `131072`. También vemos que actualmente solo hay 1 `archivo/entrada` en el sistema que esté apuntando al mismo inodo.

Una vez creado el archivo crearemos un enlace duro hacia el archivo que acabamos de crear introduciendo el siguiente comando en la terminal:

```bash
ln archivo.txt enlace_duro.txt
```

#### ¿Cómo podemos crear un enlace simbólico o soft link?

Para comprender bien lo que es un enlace simbólico crearemos un archivo de texto ejecutando el siguiente comando en la terminal:

```bash
echo "Hola mundo" > archivo.txt
```

Una vez creado el archivo vamos a consultar su número de inodo ejecutando el siguiente comando de la terminal:

```bash
ls -li archivo.txt

131072 -rw-r--r-- 2 usuario usuario 11 nov  9 20:00 archivo.txt
```

Por lo tanto el inodo del archivo que acabamos de crear es el `131072`. También vemos que actualmente solo hay 1 `archivo/entrada` en el sistema que esté apuntando al mismo inodo.

Una vez creado el archivo crearemos un enlace simbólico hacia el archivo que acabamos de crear ejecutando el siguiente comando en la terminal:

```bash
ln -s archivo.txt enlace_simbolico.txt
```

### 104.6 Buscar archivos del sistema y colocarlos en la ubicación correcta.

#### Usando el comando `find` en Linux

Comencemos con el comando `find` y cómo usarlo en toda su capacidad.

**Sintaxis básica**

El comando más común utilizado para encontrar y filtrar archivos en Linux es a través del comando `find`. El diseño básico de este comando es el siguiente:

```bash
find [ruta] [opciones] [expresión]
```

- `ruta` - Es la ruta donde se va a buscar el archivo o directorio.
- `opciones` - Son las opciones que se pueden utilizar para filtrar la búsqueda.
- `expresión` - Es la expresión que se va a utilizar para filtrar la búsqueda.

Actividades complementarias:

- - [Realizar el examen del tópico 4](https://www.goconqr.com/es/quiz/11901930/examen-101-lpi-chapter-4-5-managing-files-31-de-50)
- [Práctica de ejercicios del tópico 1](laboratorio-4.md)
- [Simulacro del Examen 101](https://www.goconqr.com/es/quiz/37054907/examen-de-certificacion-lpic-101)