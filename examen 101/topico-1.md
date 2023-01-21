# LPIC-1 Examen 101 - Tópico 1

## Tópico 101: Arquitectura del Sistema

Comprende los siguientes ítems:

- [101.1: Determinar y configurar los ajustes de hardware](#101.1-determinar-y-configurar-los-ajustes-de-hardware)
- [101.2: Arrancar del sistema](#101.2-arrancar-del-sistema)
- [101.3: Cambiar niveles de ejecución/destinos de arranque y apagar o reiniciar el sistema](#cambiar-niveles-de-ejecucióndestinos-de-arranque-y-apagar-o-reiniciar-el-sistema)

### 101.1: Determinar y configurar los ajustes de hardware

**Kernel de Linux**: Es el núcleo del sistema operativo Linux. Es el encargado de gestionar los recursos del sistema, como la memoria, los dispositivos de entrada/salida, los procesos, etc. El kernel de Linux es un programa que se ejecuta en modo privilegiado, es decir, con todos los privilegios del sistema. El kernel de Linux tiene dos funciones primarias: controlar el acceso a los dispositivos físicos del ordenador y establecer cúando y cómo los procesos interactuarán con estos dispositivos.

**Directorio `/proc`**: También llamado sistema de archivos `proc` - contiene una jerarquía de archivos especiales que representan el estado actual del kernel - permitiendo a las aplicaciones y usuarios mirar detenidamente en la vista del kernel del sistema.

Visualización de archivos virtuales en el directorio `/proc`:

- `/proc/cpuinfo`: Información sobre el procesador.
- `/proc/meminfo`: Información sobre la memoria.
- `/proc/partitions`: Información sobre las particiones.
- `/proc/version`: Información sobre la versión del kernel.
- `/proc/modules`: Información sobre los módulos cargados.
- `/proc/interrupts`: Información sobre las interrupciones.
- `/proc/ioports`: Información sobre los puertos de E/S.
- `/proc/pci`: Información sobre los dispositivos PCI.
- `/proc/scsi`: Información sobre los dispositivos SCSI.
- `/proc/ide`: Información sobre los dispositivos IDE.
- `/proc/usb`: Información sobre los dispositivos USB.
- `/proc/locks`: Información sobre los bloqueos de archivos.
- `/proc/mounts`: Información sobre los puntos de montaje.
- `/proc/net`: Información sobre la red.
- `/proc/sys`: Información sobre el sistema.
- `/proc/sysrq-trigger`: Información sobre el sistema.
- `/proc/tty`: Información sobre los terminales.
- `/proc/uptime`: Información sobre el tiempo de actividad del sistema.
- `/proc/vmstat`: Información sobre la memoria virtual.
- `/proc/zoneinfo`: Información sobre las zonas de memoria.

- **Directorio `/sys`**: En este información variada sobre directorio encontramos dispositivos. Entre estos datos podemos ver el estado de los mismos (en funcionamiento o no), el fabricante, el modelo y el bus a que estań conectados. Al igual que el `/proc` proveen información del kernel relativa a eventos del sistema operativo.

- **Directorio `/dev`**: Es una parte del árbol de directorios Linux compuesta por un sistema de archivos virtual, llamados `devfs`, que dinámicamente crea directorios y archivos para presentar una estructura jerarquizada de accesos a diversas características del sistema.

Algunos de los archivos que podemos encontrar en el directorio `/dev` son:

- `/dev/fd0`: Unidad de disquete.
- `/dev/sda`: primer disco duro (sin considerar particiones).
- `/dev/sda1`: primera partición del primer disco duro.
- `/dev/sdb`: segundo disco duro (sin considerar particiones).
- `/dev/sdb1`: primera partición del segundo disco duro.
- `/dev/sdc`: disco USB (se utiliza emulación SCSI, se usa el primer nombre del dispositivo libre `sdb`, o `sdc`, o `sdd`, etc.).
- `/dev/sdc1`: primera partición del disco USB.
- `/dev/tty1`: primer terminal de consola.
- `/dev/tty2`: segundo terminal de consola.
- `/dev/lp0`: primer puerto paralelo (impresora).
- `/dev/null`: archivo especial que descarta todo lo que se le envía.
- `/dev/zero`: archivo especial que contiene ceros.
- `/dev/full`: archivo especial que devuelve código de error `ENOSPC`

**Directorio `/dev/null`**: Leer desde `/dev/null` devuelve siempre error de fin de archivo (EOF). Escribir en `/dev/null` descarta todo lo que se le envía (se realiza el proces de lectura desde la fuente, pero no se realiza ningún proceso de escritura).

Ejemplo: `dd if=/dev/cdrom of=/dev/null` copia el contenido del CD-ROM al directorio `/dev/null` (descartando el contenido del CD-ROM).

**Directorio `/dev/zero`**: Este archivo es similar a `/dev/null`, pero con la diferencia de que `/dev/zero` contiene un número infinito de caracteres ASCII 0. Leer desde `/dev/zero` devuelve siempre un carácter ASCII 0 (el nulo o 0x00, no el número cero). Escribir en `/dev/zero` descarta todo lo que se le envía (se realiza el proces de lectura desde la fuente, pero no se realiza ningún proceso de escritura).

Ejemplo: `dd if=/dev/zero of=/dev/sda` copia el contenido del directorio `/dev/zero` al disco duro `/dev/sda` (descartando el contenido del disco duro).

**Directorio `/dev/full`**: Es un archivo de dispositivo especial que devuelve el código de error `ENOSPC`, —que significa que no hay espacio libre en el dispositivo— al intentar escribir en él, y proporciona un número infinito de bytes cero a cualquier proceso que lea de él, como `/dev/zero`. Este dispositivo se usa generalmente cuando se prueba el comportamiento de un programa cuando encuentra un disco lleno.

Ejemplo:

```bash
$ echo "Hola mundo" > /dev/full
bash: /dev/full: No space left on device
```

**Comando `lsmod`**: Es una herramienta en línea de comando que muestra información sobre los módulos del kernel linux. El kernel de Linux tiene un diseño modular. Cada módulo del núcleo es un fragmento de código que amplía las funciones del núcleo, que como norma general se compilan como módulos cargables.

La herramienta lsmod no admite opciones, su única misión es leer el contenido de `/proc/modules` e imprimir un listado formateado en pantalla. Las tres columnas que se muestran son:

- `Module`: Nombre del módulo.
- `Size`: Tamaño del módulo en bytes.
- `Used by`: Módulos que dependen de este módulo. Arroja un valor numérico que indica cuántas instancias del módulo se estan usando. Si el valor es 0, significa que el módulo no está en uso. Lo siguiente al número indica lo que está utilizando el módulo.

Ejemplo:

```bash
$ lsmod
Module                  Size  Used by
xt_recent              24576  0
ip_set                 53248  0
ip_vs_sh               16384  0
ip_vs_wrr              16384  0
ip_vs_rr               16384  0
ip_vs                 163840  6 ip_vs_rr,ip_vs_sh,ip_vs_wrr
xt_mark                16384  12
...
```

**Comando lspci**: Es una herramienta que muestra la información acerca de las ranuras PCI (Peripheral Component Interconnect) en el sistema. La información que muestra es la siguiente:

- `Bus`: Número de bus PCI.
- `Device`: Número de dispositivo PCI.
- `Function`: Número de función PCI.
- `Vendor`: Identificador del fabricante.
- `Device`: Identificador del dispositivo.
- `SVendor`: Identificador del fabricante del sub-sistema.
- `SDevice`: Identificador del sub-sistema.
- `Class`: Clase del dispositivo.
- `Driver`: Nombre del controlador del dispositivo.

La opción `-m` o `-mm` permite mostrar la información en un formato de legado que puede ser interpretado por equipos y otros programas.

El parámtetro `-t` permite mostrar un diagrama que incluye a todas las ranuras PCI, puentes, dispositivos y conexiones, entre otros.

Ejemplo:

```bash
$ lspci
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Root Complex
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 IOMMU
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-1fh) PCIe Dummy Host Bridge
00:01.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.3 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:01.7 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 PCIe GPP Bridge [6:0]
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-1fh) PCIe Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Raven/Raven2 Internal PCIe GPP Bridge 0 to Bus A
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 61)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 51)
```

**Comando `lsusb`**: Es una herramienta que muestra la lista de ranuras USB y los dispositivos conectados a ellas. La información que muestra es la siguiente:

- `Bus`: Número de bus USB.
- `Device`: Número de dispositivo USB.
- `ID`: Identificador del dispositivo.
- `Class`: Clase del dispositivo.
- `Driver`: Nombre del controlador del dispositivo.

El parámetro `-t` permite ver la lista de ranuras USB y los dispositivos conectados con un diagrama jerárquico.

Ejemplo:

```bash
$ lsusb
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 003: ID 0bda:b023 Realtek Semiconductor Corp. RTL8822BE Bluetooth 4.2 Adapter
Bus 003 Device 002: ID 04f3:245a Elan Microelectronics Corp. Touchscreen
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 085: ID 13d3:56b2 IMC Networks Integrated Camera
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

### 101.2 Arrancar del sistema

**Comando `dmesg`**: Es usado con el fin de escribir los mensajes del kernerl en Linux y otros sistemas operativos similares a Unix en una salida estándar de forma mucho más organizada. Obtiene los datos leyendo el buffer del anillo del kernel. Para recordar, un buffer es una parte de la memoria del equipo que se reserva como un lugar temporal para los datos que son enviados o recibidos desde un dispositivo externo, como por ejemplo: una unidad de disco, un teclado.

El comando `dmesg` es usado para ver los mensajes del kernel que se han almacenado en el buffer del anillo del kernel. El buffer del anillo del kernel es un buffer circular que almacena los mensajes del kernel. El tamaño del buffer del anillo del kernel se puede configurar en el archivo `/proc/sys/kernel/printk` y se puede ver el tamaño actual del buffer del anillo del kernel con el comando `dmesg -s`.

Ejemplo:

```bash
$ dmesg
[30827.416698] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=45 ID=0 PROTO=TCP SPT=443 DPT=36652 WINDOW=0 RES=0x00 RST URGP=0
[30842.380082] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=45 ID=0 PROTO=TCP SPT=443 DPT=36810 WINDOW=0 RES=0x00 RST URGP=0
[30866.097196] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=45 ID=0 PROTO=TCP SPT=443 DPT=37064 WINDOW=0 RES=0x00 RST URGP=0
[30889.495273] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=46 ID=0 PROTO=TCP SPT=443 DPT=37322 WINDOW=0 RES=0x00 RST URGP=0
[30903.202690] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=46 ID=0 PROTO=TCP SPT=443 DPT=37464 WINDOW=0 RES=0x00 RST URGP=0
[30932.984781] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=46 ID=0 PROTO=TCP SPT=443 DPT=37772 WINDOW=0 RES=0x00 RST URGP=0
[30950.986375] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=45 ID=0 PROTO=TCP SPT=443 DPT=37950 WINDOW=0 RES=0x00 RST URGP=0
[30974.463674] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=45 ID=0 PROTO=TCP SPT=443 DPT=38184 WINDOW=0 RES=0x00 RST URGP=0
[30993.296072] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=45 ID=0 PROTO=TCP SPT=443 DPT=38366 WINDOW=0 RES=0x00 RST URGP=0
[31011.933256] [UFW BLOCK] IN=wlp2s0 OUT= MAC=30:c9:ab:98:9e:f1:46:fe:30:f1:89:64:08:00 SRC=140.82.114.21 DST=172.20.10.3 LEN=40 TOS=0x00 PREC=0x00 TTL=46 ID=0 PROTO=TCP SPT=443 DPT=38552 WINDOW=0 RES=0x00 RST URGP=0
[31044.001302] rtw_8822be 0000:02:00.0: firmware failed to leave lps state
[31047.960655] rtw_8822be 0000:02:00.0: firmware failed to leave lps state
[31102.992388] rtw_8822be 0000:02:00.0: firmware failed to leave lps state
[31342.986038] perf: interrupt took too long (3968 > 3933), lowering kernel.perf_event_max_sample_rate to 50250
[31408.915932] rtw_8822be 0000:02:00.0: firmware failed to leave lps state
[31463.956444] rtw_8822be 0000:02:00.0: firmware failed to leave lps state
[31504.918189] rtw_8822be 0000:02:00.0: firmware failed to leave lps state
```

**`SystemD`**: Es el administrador de servicios y sistemas en Linux, y la estandarización de la mayoría de distribuciones de Debian y Red Hat. SystemD fue desarrollado con el objetivo de encargarse de arrancar todo lo que está por debajo del Kernel, permitiendo ejecutar varios procesos de manera simultánea. Además, permite un seguimiento de procesos a través del uso de grupos de control del sistema operativo Linux.

**Comando `journalctl`**: Con la llegada de systemd, el comando `journalctl` se ha convertido en el comando por defecto para ver los logs del sistema. Es un comando muy potente que nos permite filtrar los logs por fecha, por tipo de mensaje, por usuario, por servicio, etc. Además, nos permite ver los logs en tiempo real, es decir, ver los logs que se van generando en tiempo real. Por ejemplo, si queremos ver los logs en tiempo real, podemos ejecutar el siguiente comando:

```bash
journalctl -f
```

El comando `journalctl` es la herramienta más usada para acceder a los registros del sistema y en esta entrada.

```bash
$ journalctl
-- Journal begins at Fri 2022-12-02 01:17:14 -04, ends at Sat 2023-01-21 11:04:02 -04. --
Dec 02 01:17:14 carlos-osuna kernel: Linux version 5.11.0-49-generic (buildd@lcy02-amd64-054) (gcc (Ubuntu 10.3.0-1ubuntu1) 10.3.0, GNU ld (GNU Binutils for Ubuntu) 2.36.1) #55-Ubuntu SMP Wed Jan 12 17:36:34 UTC 2022 (Ubuntu 5.11.0-49.5>
Dec 02 01:17:14 carlos-osuna kernel: Command line: BOOT_IMAGE=/boot/vmlinuz-5.xx.x-xx-generic root=UUID=5826b62d-xxxx-xxxx-xxxx-7c3fc2335aec ro quiet splash vt.handoff=7
Dec 02 01:17:14 carlos-osuna kernel: KERNEL supported cpus:
Dec 02 01:17:14 carlos-osuna kernel:   Intel GenuineIntel
Dec 02 01:17:14 carlos-osuna kernel:   AMD AuthenticAMD
Dec 02 01:17:14 carlos-osuna kernel:   Hygon HygonGenuine
Dec 02 01:17:14 carlos-osuna kernel:   Centaur CentaurHauls
Dec 02 01:17:14 carlos-osuna kernel:   zhaoxin   Shanghai
Dec 02 01:17:14 carlos-osuna kernel: x86/fpu: Supporting XSAVE feature 0x001: 'x87 floating point registers'
Dec 02 01:17:14 carlos-osuna kernel: x86/fpu: Supporting XSAVE feature 0x002: 'SSE registers'
Dec 02 01:17:14 carlos-osuna kernel: x86/fpu: Supporting XSAVE feature 0x004: 'AVX registers'
Dec 02 01:17:14 carlos-osuna kernel: x86/fpu: xstate_offset[2]:  576, xstate_sizes[2]:  256
Dec 02 01:17:14 carlos-osuna kernel: x86/fpu: Enabled xstate features 0x7, context size is 832 bytes, using 'compacted' format.
Dec 02 01:17:14 carlos-osuna kernel: BIOS-provided physical RAM map:
```

#### BIOS vs UEFI

**BIOS**: Es el acrónimo de Basic Input/Output System, es un firmware que se encuentra en la placa base de un ordenador y que se encarga de realizar las funciones de arranque del sistema operativo. El BIOS es el encargado de realizar la comprobación de los dispositivos de hardware, de cargar el sistema operativo y de realizar la comprobación de la memoria RAM. El BIOS es un firmware que se encuentra en la placa base de un ordenador y que se encarga de realizar las funciones de arranque del sistema operativo. El BIOS es el encargado de realizar la comprobación de los dispositivos de hardware, de cargar el sistema operativo y de realizar la comprobación de la memoria RAM.

**UEFI**: Es el acrónimo de Unified Extensible Firmware Interface, es un estándar que se utiliza para reemplazar al BIOS. El UEFI es un firmware que se encuentra en la placa base de un ordenador y que se encarga de realizar las funciones de arranque del sistema operativo. El UEFI es el encargado de realizar la comprobación de los dispositivos de hardware, de cargar el sistema operativo y de realizar la comprobación de la memoria RAM. El UEFI es un firmware que se encuentra en la placa base de un ordenador y que se encarga de realizar las funciones de arranque del sistema operativo. El UEFI es el encargado de realizar la comprobación de los dispositivos de hardware, de cargar el sistema operativo y de realizar la comprobación de la memoria RAM.

**Proceso de Arranque antiguo**: El proceso de arranque antiguo se basa en el uso del BIOS, el cual se encarga de realizar las siguientes funciones:

1. BIOS: Sistema de Entrada/Salida Básico
2. MBR (Master Boot Record): Es el primer sector del disco duro, y es el encargado de realizar la comprobación de la tabla de particiones y de cargar el sistema operativo.
3. Boot Loader: Es el encargado de cargar el sistema operativo.
4. Kernel: Es el encargado de cargar los servicios del sistema operativo.

**Proceso de Arranque UEFI**: El proceso de arranque UEFI se basa en el uso del UEFI, el cual se encarga de realizar las siguientes funciones:

1. UEFI: Sistema de Entrada/Salida Unificado Extensible.
2. EFI Boot Loader: Es el encargado de cargar el sistema operativo.
3. Kernel: Es el encargado de cargar los servicios del sistema operativo.

#### Gestores de arranque

**GRUB (Grand Unified Bootloader)**: Es el acrónimo de Grand Unified Bootloader, es un gestor de arranque que se encarga de cargar el sistema operativo. El GRUB es el encargado de realizar la comprobación de los dispositivos de hardware, de cargar el sistema operativo y de realizar la comprobación de la memoria RAM. Permite tener diferentes sitemas operativos y diferentes versiones de ellos, en el mismo disco duro.

**Lilo (Linux Loader)**: Es un gestor de arranque que permite elegir, entre los sistemas operativos Linux y otras plataformas, con cual se ha de trabajar al momento de iniciar un equipo con más de un sistema operativo disponible.

**NTLDR (NT Loader)**: Es un gestor de arranque que se encarga de cargar el sistema operativo. El NTLDR es el encargado de realizar la comprobación de los dispositivos de hardware, de cargar el sistema operativo y de realizar la comprobación de la memoria RAM. Permite tener diferentes sitemas operativos y diferentes versiones de ellos, en el mismo disco duro. Es el archivo que es ejecutado por el sector de arranque y muestra un menú de arranque para los usuarios seleccionar su sistema de destino.

**Sistema de Arranque BOOTMGR**: El bootmgr (BOOT ManaGer) es el gestor de arranque de Windows Vista/7 que sustituye al NTLDR (NTLoaDer) del Windows XP y anteriores sistemas NT.

**Initramfs**: Es un sistema de archivos ram de inicio basado en `tmfs` (un sistema de ficheros de tamaño flexible y ligero que se carga en memoria) que no utiliza un dispositivo de bloque aparte (por lo que no se realiza ningún tipo de almacenamiento en caché y por tanto desaparece toda la carga mencionada anteriormente).

El contenido del sistema de archivos `initramfs` se obtiene creando un fichero `cpio`. `cpio` es una solución antigua (pero probada) para archivar ficheros (y a los ficheros resultantes se les llama ficheros `cpio`). `cpio` es definitivamente comparable al archivador `tar`. La elección aquí de `cpio` ha sido porque era más sencilla de implementar (desde el punto de vista del código) y soportado (anterior) por dispotivios de fichero que `tar` no soportaria.

**Sysvinit**: El paquete `Sysvinit`, conocido como `SysV` contiene programas para controlar el arranque, ejecución y descarga de todos los demás programas.

El primer proceso que inicia el kernel es `init`, y se mantiene activo mientras la máquina siga en funcionamiento, es el proceso principal.

La gran mayoría de distros Linux utilizaban `SysV`, y aunque se crearon otras alternativas como `Service Management`, `Upstart`, etc, ninguna llegó a implantarse en masa. Hasta que llegó Systemd y fue adoptada por la gran mayoría de distros, debemos reconocer que el `SysVinit` actual es una herramienta en desuso.

**Systemd**: Es un gestor del sistema y de los servicios para Linux, compatible con los initscript SysV y LSB. systemd proporciona una notable capacidad de paralelización, utiliza la activación de socket y D- Bus para iniciar los servicios, permite el inicio de los demonios bajo demanda, realiza un seguimiento de los procesos con el uso de los grupos de control de Linux, apoya snapshotting y la restauración del estado del sistema, mantiene los puntos montaje y servicios de montaje automático e implementa un elaborado sistema de gestión de dependencias basado en un control lógico de los servicios.

Entre las características más importante podemos destacar:

- Paralelización de Procesos (poder ejecutar 2 o más procesos en simultáneo) lo cual se traduce en un inicio más rápido del sistema.

- Optimiza el uso de recursos utilizando `cgroups` (control de grupos) y `namespaces` (espacios de nombres).

- Soporta `snapshotting` (instantáneas) y `restore` (restauración) del estado del sistema.

- Administra puntos de montaje y montaje de unidades de almacenamiento.

### 101.3 Cambiar niveles de ejecución/destinos de arranque y apagar o reiniciar el sistema

**Archivo `/etc/inittab`**: Es el archivo de configuración utilizado por el sistema de inicialización `System V (SysV)` en Linux. Este archivo define tres elementos para el **proceso de inicio**:

- El **nivel de ejecución** por defecto.
- Qué procesos iniciar, supervisar y reiniciar si terminan.
- Qué acciones tomar cuando el sistema ingresa a un nuevo nivel de ejecución.

Una vez que se ejecutan todas las entradas en `/etc/inittab/` para su nivel de ejecución, se completa el proceso de arranque y puede iniciar sesión. Cada línea en el archivo `inittab` consta de cuatro campos delimitados por dos puntos:

`id:runlevels:action:process`

- **`id` (código de identificación)**: Consiste en una secuencia de uno a cuatro caracteres que identifica la entrada.

- **`runlevels` (niveles de ejecución)**: Enumera los niveles de ejecución a los que se aplica esta entrada.

- **`action`**: Los códigos específicos en este campo le dicen a init cómo tratar el proceso. Los valores posibles incluyen: `initdefault`, `sysinit`, `boot`, `bootwait`, `wait`, y `respawn`.

- **`process`**: Es el comando que se ejecuta cuando se inicia el sistema.

**Script de Inicio**: Es un script que se ejecuta al inicio del sistema. Los scripts bajo `/etc/init.d` se dividen en dos categorías:

- **Scripts llamados directamente por init**: Esto solo sucede en el caso del arranque, así como también en caso de un apagado instantáneo.

- **Scripts llamados indirectamente por init**: Esto ocurre en el caso de un cambio de nivel de ejecución.

Todos los scripts se encuentran bajo `/etc/init.d`. Los que se usan para el cambio de nivel de ejecución, se encuentran también en ese directorio, pero son ejecutados siempre como un enlace simbólico desde uno de los subdirectorios `/etc/init.d/rc0` hasta `/etc/init.d/rc6`.

**Comandos para ejecutar servicios**

| Descripción                                                            |           `SysVinit`            |             `Systemd`             |
| ---------------------------------------------------------------------- | :-----------------------------: | :-------------------------------: |
| Iniciar un servicio                                                    |    `service <nombre> start`     |    `systemctl start <nombre>`     |
| Detener un servicio                                                    |     `service <nombre> stop`     |     `systemctl stop <nombre>`     |
| Reiniciar un servicio                                                  |   `service <nombre> restart`    |   `systemctl restart <nombre>`    |
| Forzar el reinicio de un servicio                                      | `service <nombre> force-reload` | `systemctl force-reload <nombre>` |
| Reiniciar un servicio si sigue corrieendo                              | `service <nombre> condrestart`  | `systemctl condrestart <nombre>`  |
| Recargar la configuración de un servicio                               |    `service <nombre> reload`    |    `systemctl reload <nombre>`    |
| Ver el estado de un servicio                                           |    `service <nombre> status`    |    `systemctl status <nombre>`    |
| Habilitar un servicio para que se inicie en el arranque                |     `chkconfig <nombre> on`     |    `systemctl enable <nombre>`    |
| Deshabilitar un servicio para que no se inicie en el arranque          |    `chkconfig <nombre> off`     |   `systemctl disable <nombre>`    |
| Ver el estado de un servicio                                           |   `chkconfig <nombre> --list`   |    `systemctl list-unit-files`    |
| Ver si un servicio está habilitado para el arranque                    |      `chkconfig <nombre>`       |  `systemctl is-enabled <nombre>`  |
| Crear un nuevo archivo de configuración para un servicio o modificarlo |   `chkconfig <nombre> --add`    |     `systemctl daemon-reload`     |

**Proceso Init**: Es el padre de todos los procesos. Su papel primario es crear procesos a partir de un guión guardado en el fichero `/etc/inittab`. Este fichero normalmente tiene entradas que harán que se levante `gettys` en cada ínea que los usuarios puedan conectarse. También controla procesos autónomos requeridos por un sistema particular.

**Nivel de ejecución**: Es un conjunto de servicios que se ejecutan en un sistema operativo. Los niveles de ejecución son:

  * **Nivel 0**: Apagado instantáneo del sistema.
  * **Nivel 1**: Modo de recuperación del sistema.
  * **Nivel 2**: Modo de recuperación del sistema.
  * **Nivel 3**: Modo de consola.
  * **Nivel 4**: Modo de consola.
  * **Nivel 5**: Modo gráfico.
  * **Nivel 6**: Apagado del sistema.

Los procesos levantados por init en cada uno de estos niveles se definen en el fichero `/etc/inittab`.

**Escribir archivos de unidad**: La sintaxis de los archivos de unidad de systemd esta inspirada en los archivos `.desktop` de la especificación de entrada del escritorio `XDG` que a su vez están inspirados en los archivos `.ini` de Windows.

Estos archivos se cargan desde varias ubicaciones, pero los principales son:

- `/usr/lib/systemd/system/`: Unidades proporcionadas por los paquetes instalados.
- `/etc/systemd/system/`: Unidades instaladas por el administrador del sistema.

**Fin del Tópico 1**

Actividades complementarias:
- [Realizar el examen del tópico 1]()
- [Práctica de ejercicios del tópico 1]()
- [Leer Libros digitales del capítulo tratado]()