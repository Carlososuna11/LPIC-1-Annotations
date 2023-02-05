# LPIC-1 Examen 101 - Tópico 3

## Tópico 103: Comandos GNU y UNIX

Comprende los siguientes ítems:

– [103.1 Trabajar en la línea de comandos.](#1031-trabajar-en-la-línea-de-comandos)

– [103.2 Procesar las cadenas de texto utilizando filtros.](#1032-procesar-las-cadenas-de-texto-utilizando-filtros)

– [103.3 Realizar la administración del archivo y del directorio básicos.](#1033-realizar-la-administración-del-archivo-y-del-directorio-básicos)

– [103.4 Usar secuencias, tuberías y redirecciones.](#1034-usar-secuencias-tuberías-y-redirecciones)

– [103.5 Crear, monitorear y liquidar procesos.](#1035-crear-monitorear-y-liquidar-procesos)

– [103.6 Modificar las prioridades para la ejecución de los procesos.](#1036-modificar-las-prioridades-para-la-ejecución-de-procesos)

– [103.7 Buscar los archivos de texto utilizando expresiones normales.](#1037-buscar-los-archivos-de-texto-utilizando-expresiones-normales)

– [103.8 Realizar las operaciones básicas de edición de archivos utilizando vi.](#1038-realizar-las-operaciones-básicas-de-edición-de-archivos-utilizando-vi)

### 103.1 Trabajar en la línea de comandos.

**Shell Bash**: Es uno de los numerosos shells disponibles para Linux. También denominado Bourne-again Shell en honor a Bourne creador de Stephen Shell, sus iniciales (`/bin/sh`). Es básicamente compatible con `sh`, pero con proporción a varias mejoras.

- `bash`: Bourne Again Shell.
- `bsh`: Bourne Shell.
- `tcsh`: Basada en C Shell (csh).
- `csh`: Original C Shell.
- `ksh`: Korn Shell (Mejora las características Bourne Shell).
- `zsh`: Z Shell (Mejora las características de Korn Shell).

#### Comando Echo

`echo`: Imprime en pantalla el texto que se le pasa como argumento.

```bash
$ echo "Hola Mundo"
Hola Mundo
```

También se puede usar `echo` para imprimir variables de entorno.

```bash
msg="Hola Mundo"
echo $msg
Hola Mundo

echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
```

**`echo -e`**: Imprime caracteres especiales como `\n` (nueva línea) o `\t` (tabulador).

```bash
$ echo -e "Hola\nMundo"
Hola
Mundo
```

**Caracteres especiales**

- `\a`: Emite una señal de alarma.
- `\b`: Retrocede un carácter.
- `\c`: No imprime el carácter de nueva línea.
- `\e`: Imprime el carácter de escape.
- `\f`: Imprime un carácter de nueva página.
- `\n`: Imprime un carácter de nueva línea.
- `\r`: Imprime un carácter de retorno de carro.

**`echo "Logfile" > logfile.txt`**: Redirige la salida de `echo` al archivo `logfile.txt`.

Para concatenar la salida de `echo` al archivo `logfile.txt` se usa `>>`.

Para más opciones que ofrece el comando `echo`. Revisar el siguiente video de [Linode](https://youtu.be/Tj-9tahWvok)

#### Comando exit

El comando `exit` permite terminal la sesión actual de la terminal con el estatus de `N`.

```bash
$ exit N
```

si `N` no es especificado, el estatus de salida es el del último comando ejecutado.

#### Comando Env

Si `env` se ejecuta sin ninguna opción, imprime las variables del entorno actual. De lo contrario, `env` establece cada `NOMBRE` en `VALOR` y ejecuta `COMANDOS`

Sintaxis

```bash
$ env [OPCION]... [-] [NOMBRE=VALOR]... [COMANDO [ARG]...]
```

Opciones

- `-i`, `--ignore-environment`: Inicializa el entorno vacío.
- `-0`, `--null`: Termina cada nombre de variable con un carácter nulo.
- `-u`, `--unset=NAME`: Elimina la variable de entorno `NAME`.
- `--help`: Muestra la ayuda y termina.
- `--version`: Muestra la información de la versión y termina.
- `-`, `--`: Termina las opciones.

Ejemplos

```bash
$ env
HOME=/computerhope/public_html
PATH=/usr/local/bin:
LOGNAME=admin
HZ=100
TERM=vt100
TZ=MST7MDT
SHELL=/bin/csh
MAIL=/var/mail/computerhope
_INIT_UTS_PLATFORM=SUNW,SPARCstation-10
_INIT_UTS_RELEASE=5.7
_INIT_UTS_SYSNAME=SunOS
```

Algunas de las variables de entorno más comunes son:

- `HOME`: Directorio de inicio del usuario.
- `PATH`: Lista de directorios separados por dos puntos `:` donde el sistema buscará los comandos.
- `LOGNAME`: Nombre de usuario.
- `TERM`: Tipo de terminal.
- `TZ`: Zona horaria.
- `SHELL`: Shell que se está usando.
- `MAIL`: Ubicación del buzón de correo.
- `LANG`: Idioma del sistema.
- `MANPATH`: Ubicación de los manuales.
- `EDITOR`: Editor de texto por defecto.

#### Comandos Unset y Set

`set`: Permite definir y determinar los valores de las variables de entorno.

Sintaxis

```bash
$ set [-aefhkntuvx] [-o option] [arg ...]
```

Opciones

- `--`: Una opción de un guión doble (" -- ") significa el final de una lista de opciones. Esta opción es principalmente útil cuando los valores enumerados después de las opciones comienzan con un guión.

- `-a`: Las variables de entorno definidas en el entorno actual se exportan a los comandos ejecutados por el shell.

- `-mi`: Salga inmediatamente si un comando sale con un estado de salida distinto de cero.

- `-F`: Deshabilite la generación de nombres de archivo (globbing).

- `-h`: Ubique y recuerde los comandos de función a medida que se definen las funciones (los comandos de función normalmente se ubican cuando se ejecuta la función).

- `-k`: Todos los argumentos de palabras clave se colocan en el entorno de un comando, no solo los que preceden al nombre del comando.

- `-n`: Lee comandos, pero no los ejecuta.

- `-t`: Salida después de leer y ejecutar un comando.

- `-u`: Si un argumento es una variable de entorno que no está definida, se produce un error.

- `-v`: Imprime el nombre de cada comando antes de ejecutarlo.

- `-x`: Imprime el nombre de cada comando antes de ejecutarlo, y luego imprime cada argumento de comando después de la expansión.

Utilice el comando `unset` para eliminar las variables durante la ejecución del programa. Puede eliminar funciones y variables de shell. Usando el comando unset, puede desarmar valores y atributos de variables y funciones de shell.

Sintaxis

```bash
$ unset [-fv] [nombre ...]
```

Opciones

- `-f`: Elimina las funciones con los nombres especificados.

- `-v`: Elimina las variables con los nombres especificados.

#### Comando Exec

El comando `exec` reemplaza el proceso actual con un nuevo proceso. El comando `exec` es útil para ejecutar un comando en el contexto del proceso actual.

Sintaxis

```bash
$ exec [-cl] [-a name] [command [arguments ...]] [redirection ...]
```

Opciones

- `-a name`: Asigna el nombre `name` al comando que se ejecuta.

- `-c`: Ejecuta el comando con un entorno vacio.

- `-l`: Usado para pasar el guión como el argumento 0 del comando.

**Nota**: el comando `exec` no crea un nuevo proceso. Cuando ejecutamos el comando `exec` desde la terminal, el proceso de terminal en curso se reemplaza por el comando que se proporciona como argumento para el comando `exec`.

El comando `exec` se puede utilizar de dos modos:

1. **Ejecutar con un comando como argumento** : en el primer modo, el `exec` intenta ejecutarlo como un comando pasando los argumentos restantes, si los hay, a ese comando y administrando las redirecciones, si las hay.

Ejemplo

```bash
# El comando dado se ejecuta en un proceso diferente... y devuelve los resultados, luego el proceso original vuelve a tener el control
pbmac@pbmac-servidor $ exec wc -w < tmp
9
pbmac@pbmac-servidor $
```

2. **Ejecutar sin comando** : si no se proporciona ningún comando, las redirecciones se pueden usar para modificar el entorno de shell actual. Esto es útil ya que nos permite cambiar los descriptores de archivo del shell según nuestro deseo. El proceso continúa incluso después del comando `exec`, a diferencia del caso anterior, pero ahora la entrada, la salida y el error estándar se modifican de acuerdo con las redirecciones.

```bash
pbmac@pbmac-servidor $ bash

#Este ejecutivo crea un nuevo proceso que se superpone al shell bash iniciado por el comando anterior
pbmac@pbmac-servidor $ exec > tmp

#Ahora estamos en un proceso diferente... y todo esto está siendo dirigido a los nombres de archivo tmp por el comando anterior
pbmac@pbmac-servidor $ ls
pbmac@pbmac-server $ echo "Este mensaje no se mostrará"
pbmac@pbmac-servidor $ salir
salida

#El comando exit sale del otro proceso... y vuelve al contexto original
#Vemos todos los resultados que se enviaron al archivo llamado tmp
pbmac@pbmac-servidor $ cat tmp
prueba2.sh
prueba.sh
tmp
Este mensaje no se mostrará
```

#### Comando History

El comando `history` muestra el historial de comandos ejecutados en la sesión actual. El historial de comandos se almacena en el archivo `~/.bash_history` por defecto.

Sintaxis

```bash
$ history [-c] [-d offset] [n] or history -anrw [filename] or history -ps arg [arg...]
```

Opciones

- `-c`: Borra el historial de comandos.

- `-d offset`: Borra el comando en la posición especificada.

- `-a`: Añade el historial de comandos de la sesión actual al archivo `~/.bash_history`.

- `-n`: Lee el historial de comandos de la sesión actual desde el archivo `~/.bash_history`.

- `-r`: Lee el historial de comandos de la sesión actual desde el archivo `~/.bash_history` y lo ejecuta.

- `-w`: Escribe el historial de comandos de la sesión actual en el archivo `~/.bash_history`.

- `-p`: Imprime el historial de comandos de la sesión actual en el formato especificado.

- `-s`: Añade el comando especificado al historial de comandos de la sesión actual.

#### Comando Man

El comando `man` muestra la página de manual del comando especificado. El comando `man` es útil para obtener información sobre los comandos disponibles en el sistema.

Sintaxis

```bash
$ man [OPTION]... [COMMAND NAME]...
```

Ejemplos

manuel del comando printf

```bash
$ man printf
```

`Section-num` es el número de sección del manual. Por ejemplo, 1 para comandos de usuario, 2 para llamadas al sistema, 3 para funciones de biblioteca, 4 para dispositivos especiales, 5 para archivos de formato, 6 para juegos, 7 para convenciones y convenciones, 8 para comandos de administración y 9 para convenciones del kernel.

`-f option`: es posible que no pueda recordar las secciones en las que está presente un comando. Así que esta opción da la sección en la que está presente el comando dado.

`-a option`: Esta opción nos ayuda a mostrar todas las páginas de introducción disponibles en sucesión.

`-k option`: esta opción busca el comando dado como una expresión regular en todos los manuales y devuelve las páginas del manual con el número de sección en el que se encuentra.

`-w option`: esta opción devuelve la ubicación en la que está presente la página del manual de un comando determinado.

`-I option`: Considera el comando como sensible a mayúsculas y minúsculas.

#### Metacaracteres y operadores de control de Shell Bash

Bash posee varios metacaracteres, los cuales no se colocan entre comillas. También sirven para separar los datos de entrada en palabras. Estos son:

- `&`: Se utiliza para ejecutar un comando en segundo plano.

- `|`: Se utiliza para conectar la salida estándar de un comando con la entrada estándar de otro comando.

- `;`: Se utiliza para separar comandos.

- `(` y `)`: Se utiliza para agrupar comandos.

- `>`: Se utiliza para redireccionar la salida estándar de un comando a un archivo.

- `<`: Se utiliza para redireccionar la entrada estándar de un comando desde un archivo.

- `>>`: Se utiliza para redireccionar la salida estándar de un comando a un archivo, agregando el contenido al final del archivo.

- `||`: Se utiliza para ejecutar un comando si el comando anterior falla.

- `&&`: Se utiliza para ejecutar un comando si el comando anterior se ejecuta correctamente.

- `;;`: Se utiliza para separar las opciones de un comando case.

- `!`: Se utiliza para negar un comando.

- `~`: Se utiliza para representar el directorio home del usuario.

- `?`: Se utiliza para representar un carácter cualquiera.

- `1>`: Se utiliza para redireccionar la salida estándar de un comando a un archivo.

- `2>`: Se utiliza para redireccionar la salida de error de un comando a un archivo.

- `&>`: Se utiliza para redireccionar la salida estándar y la salida de error de un comando a un archivo.

- `1>>`: Se utiliza para redireccionar la salida estándar de un comando a un archivo, agregando el contenido al final del archivo.

- `2>>`: Se utiliza para redireccionar la salida de error de un comando a un archivo, agregando el contenido al final del archivo.

- `&>>`: Se utiliza para redireccionar la salida estándar y la salida de error de un comando a un archivo, agregando el contenido al final del archivo.

- `1>&2`: Se utiliza para redireccionar la salida estándar de un comando a la salida de error.

- `2>&1`: Se utiliza para redireccionar la salida de error de un comando a la salida estándar.

- `2>&-`: Se utiliza para cerrar la salida de error de un comando.

- `1>&-`: Se utiliza para cerrar la salida estándar de un comando.

- `<<`: Se utiliza para redireccionar la entrada estándar de un comando desde un archivo, hasta que se encuentre la palabra especificada.

- `<<<`: Se utiliza para redireccionar la entrada estándar de un comando desde una cadena de texto.

- `<<-`: Se utiliza para redireccionar la entrada estándar de un comando desde un archivo, hasta que se encuentre la palabra especificada, ignorando los espacios en blanco al inicio de la línea.

- `<<!`: Se utiliza para redireccionar la entrada estándar de un comando desde un archivo, hasta que se encuentre la palabra especificada, ignorando los espacios en blanco al inicio de la línea.

- `<<-!`: Se utiliza para redireccionar la entrada estándar de un comando desde un archivo, hasta que se encuentre la palabra especificada, ignorando los espacios en blanco al inicio de la línea.

#### Tipos de Rutas

1. Ruta Absoluta: Es la ruta completa desde la raíz del sistema de archivos hasta el archivo o directorio que se desea acceder. Por ejemplo, /home/usuario/archivo.txt

2. Ruta Relativa: Es la ruta desde el directorio actual hasta el archivo o directorio que se desea acceder. Por ejemplo, ../archivo.txt

3. Ruta Simbólica: Es la ruta desde el directorio actual hasta el archivo o directorio que se desea acceder. Por ejemplo, ~/archivo.txt

**Modificación del directorio de trabajo**: El comando `cd` debe ser una ruta absoluta o relativa a un directorio. En cuando a los comando, se puede utilizar `..`, `...`, `~`, y `~nombre` para referirse a directorios superiores, directorios superiores a los superiores, el directorio home del usuario actual, y el directorio home de un usuario específico, respectivamente. Si utiliza `cd` sin argumentos, se regresa al directorio home del usuario actual.

**Creación de directorios**: El comando `mkdir` crea un directorio. Si se especifica más de un nombre de directorio, se crean todos los directorios especificados. Si se especifica un nombre de directorio que ya existe, se muestra un mensaje de error.

**Eliminación de directorios**: El comando `rmdir` elimina un directorio. Si se especifica más de un nombre de directorio, se eliminan todos los directorios especificados. Si se especifica un nombre de directorio que no existe, se muestra un mensaje de error.

**Copia de archivos**: El comando `cp` copia un archivo. Si se especifica más de un nombre de archivo, se copian todos los archivos especificados. Si se especifica un nombre de archivo que no existe, se muestra un mensaje de error.

**Mover o renombrar archivos**: El comando `mv` mueve o renombra un archivo. Si se especifica más de un nombre de archivo, se mueven o renombran todos los archivos especificados. Si se especifica un nombre de archivo que no existe, se muestra un mensaje de error.

**Eliminación de archivos**: El comando `rm` elimina un archivo. Si se especifica más de un nombre de archivo, se eliminan todos los archivos especificados. Si se especifica un nombre de archivo que no existe, se muestra un mensaje de error.

**Creación de enlaces simbólicos**: El comando `ln` crea un enlace simbólico. Si se especifica más de un nombre de archivo, se crean todos los enlaces simbólicos especificados. Si se especifica un nombre de archivo que no existe, se muestra un mensaje de error.

### 103.2 Procesar las cadenas de texto utilizando filtros

#### Variables de Entorno

|  Variable  | Descripción                                                                                |
| :--------: | ------------------------------------------------------------------------------------------ |
|   `USER`   | Nombre de usuario                                                                          |
|   `UID`    | ID de usuario                                                                              |
|   `HOME`   | Directorio home                                                                            |
|   `PWD`    | Directorio actual                                                                          |
|   `PATH`   | Ruta de ejecución                                                                          |
|  `SHELL`   | Shell actual                                                                               |
|    `$`     | La id de proceso (o PID del proceso) de shell bash que se está ejecutando                  |
|   `PPID`   | La id de proceso del proceso que inició este proceso (ques es, la id del proceso primario) |
| `?` o `$?` | El código de salida del último comando ejecutado.                                          |

#### Flujos Estándar

- Todas las salidas se envían a la Salida Estándar (stdout).
- Todas las entradas vienen de la Entrada Estándar (stdin).
- Los mensajes de error se envían al Error Estándar (stderr).

<center><img src="https://imgur.com/pHO0KIw.png"></center>

#### Redirección de la Salida de un Comando

<center><img src="https://imgur.com/IGBbRas.png"></center>

```bash
$ ls -l

total 20
-rw-r--r-- 1 root root  0 May  1  2019 archivo1.txt
-rw-r--r-- 1 root root  0 May  1  2019 archivo2.txt
-rw-r--r-- 1 root root  0 May  1  2019 archivo3.txt
-rw-r--r-- 1 root root  0 May  1  2019 archivo4.txt
```

```bash
$ ls -l > lista.txt
```

#### Redirección de los mensajes de Error

- Los mensajes de error se envían directamente a la pantalla.
- Se pueden redireccionar utilizando el carácter `2>`.

```bash
$ ls -l /home/usuario/archivo.txt 2> error.txt
```

**Ejemplo**: Este comando envía el mensaje de error generado por un mal uso del comando who al archivo mensaje_error.

```bash
$ who -xyz

who: invalid option -- 'x'
Try 'who --help' for more information.
```

```bash
$ who -xyz 2> mensaje_error

$ cat mensaje_error

who: invalid option -- 'x'
```

#### Combinando la redirección de la salida

Tanto la salida estándar y el error estándar pueden ser redireccionados en la misma línea de comando:

```bash
comando 1> salida 2> error
```

```bash
comando > archivo_ambos 2>&1
```

`1>` Representa a la salida estándar.

`&1` Es igual al nombre del archivo de salida estándar.

#### Adicionando información a un archivo

<center><img src="https://imgur.com/p1OOgzz.png"></center>

```bash
# crea el archivo "listado" con el contenido generado por el comando "ls -l"
$ ls -l > listado

# Agrega al archivo "listado" el contenido generado por el comando "ls /ventas"
$ ls /ventas >> listado

# Si el archivo "control" no existe se crea el archivo "control" con el contenido generado por el comando "ls -l"
$ ls -l >> control
```

#### Concatenar Archivos

El comando cat fue originalmente creado para hacer que dos o más archivos se junten (concatenen) en un tercero.

<center><img src="https://imgur.com/UslioAb.png"></center>

```bash
$ cat archivo1 archivo2 > archivo3
```

#### Redirección de la entrada de un comando

<center><img src="https://imgur.com/mKl3UVH.png"></center>

- El programa mail envía un correo al usuario msalas, el contenido del correo proviene del archivo "reporte"

```bash
$ mail msalas < reporte
```

- El programa bc recibe un archivo que contiene instrucciones y sentencias que las ejecutará y mostrará el resultado de las mismas.

```bash
$ bc < prog1
3.456
```

#### Tubos (Pipe)

Los tubos (pipes) se utilizan para hacer que la salida estándar de un comando se convierte en la entrada estándar de otro, lo cual permite crear comandos muy potentes.

```bash
$ comando1 | comando2 | comando3
```

Ejemplos:

```bash
# muestra el contenido del directorio actual
$ ls -l

# El contenido generado por el comando "ls -l" es enviado al comando "more" y ésta lo muestra por páginas

$ ls -l | more
```

### 103.3 Realizar la Administración del Archivo y del Directorio Básicos

#### Listado de los ingresos al directorio

- Los nombres de los archivos y de los directorios son absolutos, es decir, comienzan con una `/`, o son _relativos_ al _directorio de trabajo actual_, es decir, no comienzan con una `/`. La vía absoluta de un archivo o directorio consiste en una `/` seguida de una serie de ceros o nombres de más directorios, cada uno seguido de otra `/` y luego un nombre final.

- El nombre de un archivo o de un directorio dado que sea relativo al actual directorio de trabajo, simplemente concatena el nombre en absoluto del directorio de trabajo, una `/`, y el nombre relativo.

#### Copia, traslado y eliminación de los archivos.

- `cp`: Es utilizado para hacer una copia de unos o más archivos o directorios. Usted debe dar uno (o más) nombres fuentes y un nombre destino. Los nombres fuente o destino pueden incluir la especificación de vía. Si el destino es un directorio existente, entonces todas las fuentes son copiadas en el destino. Si el destino es un directorio que no existe, entonces la (única) fuente también deberá ser un directorio y una copia del directorio fuente y de su contenido será realizada con el nombre destino como el nuevo nombre.

- `mv`: Es utilizado para mover o renombrar unos o más archivos o directorios. En general, los nombres que usted pueda ussar siguen las mismas normas que para copiar con `cp`. Puede renombrar un único archivo o mover un grupo de archivos a un nuevo directorio.

- `rm`: Es utilizado para eliminar uno o más archivos.

#### Opciones de `cp` y `mv`

- `-f` o `--force`: Si el archivo destino ya existe, entonces `cp` y `mv` no lo sobreescribirán. Con esta opción, `cp` y `mv` sobreescribirán el archivo destino.

- `-i` o `--interactive`: Pedirá confirmación antes de intentar reemplazar un archivo existente.

- `-b` o `--backup`: Realizara un backup de cualquier archivo que fuera reemplazado.

#### Creación de directorios

- `mkdir`: Es utilizado para crear uno o más directorios. Si el directorio ya existe, entonces no se creará.

- `rmdir`: Es utilizado para eliminar uno o más directorios. Si el directorio no está vacío, entonces no se eliminará.

#### Comodines y "globbing"

Con frecuencia usted puede necesitar realizar una única operación en muchos objetos del sistema de archivos, sin operar en todo el árbol como recién hicimos con las operaciones repetitivas. Aunque esto es fácil con nuestro pequeño directorio, es mucho más dificil en un sistema de archivos grande.

Para resolver este problema, utilice el soporte de comodín que esté incorporando en el bash shell. Este soporte, también denominado "globbing" (porque fue originalmente implementado como un programa denominado `/etc/glob`), le permite especificar múltiples archivos utilizando el patrón de comodines `*` y `?`.

Una secuenta que contenga cualquiera de los caracteres `?`, `*` o `[`, es un patrón de comodines. Globbing es el proceso por el cual shell (o posiblemente otro programa) expande estos patrones a una lista de nombres de rutas que concuerden con el patrón. La concordancia se realiza de la siguiente manera:

- `?` concuerda con cualquier carácter individual.
- `*` concuerda con cualquier secuencia de caracteres.
- `[` presenta una clase de caracteres. Una clase de caracteres es una cadena que no está vacía, terminada por un `]`. Una corcondancia significa la combinación de cualquier carácter único encerrado por corchetes. Existen unas pocas consideraciones especiales.

### 103.4 Usar Secuencias, Tuberías y Redirecciones

#### Redireccionar el IO Estándar

Un Shell de Linux, tal como un Bash, recibe la entrada y envía la salida como secuencias o series de caracteres. Cada carácter es independiente al anterior y del siguiente. Los caracteres no están organizados en registros estructurados o bloques de tamaño fijo. Se accede a las secuencias utilizando las técnicas del archivo IO (ya sea que la serie real de los caracteres venga desde o se dirija hacia un archivo), un teclado, una ventana en una pantalla, o algún otro dispositivo de IO. Los shells de Linux utilizan tres series estándar de I/O, cada una de ellas está asociada a un descriptor de archivos muy conocido:

- `stdout` Es la serie de salida estándar, que muestra la salida de los comandos. Cuenta con un descriptor de archivos 1.
- `stderr` Es la serie de error estándar, que muestra la salida de los errores desde los comandos. Cuenta con un descriptor de archivos 2.
- `stdin` Es la serie de entrada estándar, que proporciona la entrada a los comandos. Cuenta con un descriptor de archivos 0.

#### Redireccionar la salida

Existen dos modos de redireccionar la salida a un archivo:

- `n>`: Redireccione la salida desde el descriptor del archivo `n` a un archivo. Usted deberá tener autoridad para escribir al archivo. Si el archivo no existe, este es creado. Si ya existe, los contenios existentes generalmente se pierden sin previo aviso.

- `n>>`: También redirecciona la salida desde el descriptor del archivo `n` a un archivo. Nuevamente, deberá tener la autorización para escribir en el archivo. Si el archivo no existe, este es creado. Si existe, la salida se anexa al archivo existente.

#### Direccionar Stdout a Stdin

Usted utiliza el operador `|` (pipe) entre dos comando para dirigir el `stdout` del primero al `stdin` del segundo. Podrá construir un conducto más largo agregando más comandos y más operadores de conductos. Cualquiera de los comandos puede tener opciones o argumentos. Muchos utilizan un guión (-) en lugar de un nombre de archivo como argumento para indicar cuándo una entrada debería provenir de un stdin en lugar de hacerlo de un archivo. Verifique en las páginas del manual para estar seguro del comando. La construcción de los conductos largos de comandos de tal modo que cada uno tenga una capcidad limitada es una forma muy común que tiene Linux y UNIX ® para la realización de las tareas. En el conducto hipotético en el Listado 10, command2 y command3 ambos tienen un parámetro, muentras que command3 utiliza el - parámetro únicamente para indicar la entrada desde `stdin`.

Sintaxis: Salida del conducto a través de varios comandos

```bash
command1 | command2 parameter1 | command3 parameter1 -parameter2| command4
```

#### Usar el Comando Xargs

El comando `xargs` es utilizado para construir y ejecutar comandos a partir de la salida de otro comando. El comando `xargs` lee la entrada estándar y construye una línea de comando que es ejecutada. La línea de comando es construida de la siguiente manera:

```bash
xargs [options] [command [initial-arguments]]
```

Ejemplo:

```bash
$ cat text1
apple
pear
banana
```

```bash
$ xargs < text1

1 apple 2 pear 3 banana
```

#### 103.5 Crear, Monitorear y Liquidar Procesos

#### Procesos

- Un proceso es un programa en ejecución, utiliza recursos del sistema (procesador, memoria, hardware periférico) y está identificado con un PID.

- Todos los programas que corren bajo `GNU/LINUX` son procesos.

> Por ejemplo, el shell de un usuario, como bash, es un proceso que se ejecuta mientras está conectado al sistema.

#### Procesos: PID

- Cada proceso es identificado por un ID: `PID: Process Identification`

- Cada proceso tiene un proceso padre identificado por: `PPID: Parent Process Identification`

<center><img src="https://imgur.com/k9HQ8Mx.png"></center>

- Cuando un proceso es creado se le asigna un número (`PID`) y es añadido a la tabla de procesos y cuando el proceso concluye es retirado de la tabla.

- `GNU/Linux` mantiene en memoria una tabla de procesos, con información de los procesos activos.

<center><img src="https://imgur.com/gyaLySU.png"></center>

#### Genealogía de Procesos

- Un proceso que genera nuevos procesos es llamado padre.
- El nuevo proceso es llamado proceso hijo.

El proceso `mingetty` es hijo del proceso `init`

<center><img src="https://imgur.com/fdjOJ8I.png"></center>

#### Procesos Demonios

- Son procesos que el sistema inicia para realizar tareas básicas en forma periódica.

- Estos procesos no están asociados con un terminal (`tty`) en particular.

- Algunos procesos demonios conocidos son los siguientes:

`init (PID 1)`: Padre de todos los procesos.
`cron`: Tareas automática.
`lpd`: Demonio de Impresión LPR.

#### Proceso Init

- Es el proceso padre de todos los procesos del sistema.
- Permanece en ejecución mientras funciona el sistema.
- Hay varios niveles de ejecución, desde 0 hasta 6, las cuales se pueden invocar manualmente.

`# init <nivel_ejecucion>`

- El nivel 0 es el nivel de apagado.
- El nivel 1 es el nivel de recuperación.
- El nivel 2 es el nivel de ejecución de usuario.
- El nivel 3 es el nivel de ejecución de usuario con red.
- El nivel 4 es el nivel de ejecución de usuario con red y servicios de red.
- El nivel 5 es el nivel de ejecución de usuario con red y servicios de red y X Window.
- El nivel 6 es el nivel de apagado.

#### Carga de Servicios en Linux

En las versiones anteriores al `CentOS 7`, los servicios estaban alojados en la carpeta `/etc/init.d`, ahora en esta versión los servicios están alojados en la carpeta `/sbin`, previamente instalado con el comando `yum install systemd`.

`# cd /sbin`

Los servicios en Linux tienen los siguientes estados disponibles para ser utilizados

|         Comando         | Descripción                            |
| :---------------------: | -------------------------------------- |
|  `service named start`  | Inicia el servicio `named`             |
|  `service named stop`   | Detiene el servicio `named`            |
| `service named restart` | Reinicia el servicio `named`           |
| `service named reload`  | Recarga el servicio `named`            |
| `service named status`  | Muestra el estado del servicio `named` |

La utilizad de administración de las unit de `systemd` es `systemctl`, la cual combina las herramientas service y `chkconfig` de `SysV`, por lo tanto podremos arrancar, parar, recargar servicios, activar o desactivar servicios en el arranque, listar los estados de los servicios, etc.

|              Comando              | Descripción                  |
| :-------------------------------: | ---------------------------- |
| `systemctl restart named.service` | Reinicia el servicio `named` |
|  `systemctl stop named.service`   | Detiene el servicio `named`  |
|  `systemctl start named.service`  | Inicia el servicio `named`   |
| `systemctl reload named.service`  | Recarga el servicio `named`  |

#### Comando `ps`

Lista los procesos en ejecución.

`# ps [opciones]`

- Las opcioens más utilizadas son `ps -aux`, donde:

  - `a`: Muestra todos los procesos.
  - `u`: Muestra el usuario dueño del proceso.
  - `x`: Muestra los procesos sin terminal.

- El comando `ps` muestra la siguiente información:

  - `PID`: Identificador del proceso.
  - `TTY`: Terminal asociada al proceso.
  - `TIME`: Tiempo de ejecución del proceso.
  - `CMD`: Comando que ejecuta el proceso.

#### Comando `free`

Muestra la cantidad y uso de la memoria del sistema

`# free [opciones]`

Opciones

- `-b`: Muestra la memoria en bytes.
- `-k`: Muestra la memoria en kilobytes.
- `-m`: Muestra la memoria en megabytes.
- `-g`: Muestra la memoria en gigabytes.

#### Monitor del Sistema Gnome

Gnome System Monitor es una herramienta de monitoreo del sistema que permite visualizar información sobre el uso de la CPU, memoria, disco, red, procesos, etc.

<center><img src="https://imgur.com/utu7KDs.png"></center>

#### Comando `top`

Muestra la lista de procesos en ejecución.

`# top`

- `top` muestra la siguiente información:

  - `PID`: Identificador del proceso.
  - `USER`: Usuario dueño del proceso.
  - `PR`: Prioridad del proceso.
  - `NI`: Prioridad del proceso.
  - `VIRT`: Memoria virtual utilizada por el proceso.
  - `RES`: Memoria física utilizada por el proceso.
  - `SHR`: Memoria compartida utilizada por el proceso.
  - `S`: Estado del proceso.
  - `%CPU`: Porcentaje de uso de la CPU por el proceso.
  - `%MEM`: Porcentaje de uso de la memoria por el proceso.
  - `TIME+`: Tiempo de ejecución del proceso.
  - `COMMAND`: Comando que ejecuta el proceso.

### 103.6 Modificar las prioridades para la Ejecución de Procesos

#### Renice

Si uno o más procesos usan muchos recursos del sistema, Usted puede cambiar las prioridades de los mismo en vez de terminarlos. Para tales tareas se puede usar el comando renice. La sintaxis del mismo es la siguiente:

```bash
renice [prioridad] [[-p] [pid]...] [[-g] [gid]...] [[-u] [uid]...]
```

Resumiendo, las opciones soportadas por renice son:

- `-g`: Forzar que los parámetros de quién sean interpretados como ID's de grupo de proceso.
- `-u`: Forzar que los parámetros de quién sean interpretados como nombres de usuario.
- `-p`: Reinicia la interpretación de quién para que sea la de ID de proceso (por defecto).

Un sencillo ejemplo

Supongamos que un colega tiene corriendo un proceso con `PID 785` y dicho proceso realiza una operación cientifica compleja, y mientras el proceso está trabajando, el usuario desea jugar un juego (WoW, DOTA o lo que sea que se le antoje jugar en su `GNU/Linux`). En este ejemplo, como para el colega lo principal ahora es jugar y no le apura la operación compleja del proceso mencionado, para que lo no se parta la PC por la mitad, puede teclear: `renice +15 785` y el proceso se ejecutará con una prioridad más baja, permitiendo que el usuario juegue sin problemas.

#### Comando `nice`

Ahora que conocemos como cambiar la prioridad de los procesos ya ejecutados, probaremos a ejecutar un proceso con una prioridad predefinida por nosotros. Para esto, utilizaremos el comando nice.

En este caso debe especificar su comando como una opción para `nice`. De manera predeterminada `nice` ajusta una prioridad de `10`. El rango va desde `-20` (prioridad mayor) a `19` (prioridad menor). Por ejemplo, para ejecutar el comando `ls` con una prioridad de `5`, teclee:

```bash
nice -n 5 ls
```

Ejemplo

```bash
dd if=/dev/cdrom of=~/ubuntu-17.04-desktop-amd64.iso
```

En algunos sistemas con un CD-ROM común, el proceso de la copia de un volumen grande de información puede utilizar muchos recursos del sistema y olvidábamos que en ese momento el usuario está haciendo labores ofimáticas como por ejemplo trabajos con documentos de miles de hojas en `LibreOffice`, un verdadero tragón de recursos. El usuario puede hacer el respaldo del DVD sin afectar el rendimiento de `LibreOffice`. Para esto puede ejecutar el comando `dd` con una prioridad baja usando nice.

```bash
nice -n 19 dd if=/dev/cdrom of=~/ubuntu-17.04-desktop-amd64.iso
```

### 103.7 Buscar los archivos de Texto utilizando Expresiones Normales

#### Comando `grep`

- El comando `grep` perteneciente a la familia `Unix` es una de las herramientas más versátiles y útiles disponibles. Este busca un patrón que definamos en un archivo de texto. En otras palabras, con grep puedes buscar una palabra o patrón y se imprimirán la línea o líneas que la contengan.

- A primera vista, puede parecer un comando poco útil, sin embargo, los administradores de sistemas que manejas muchos servicios con varios archivos de configuración, lo usan para consultar o buscar líneas específicas dentro de estos archivos.

La sintaxis del comando grep al buscar un solo archivo es así

```bash
grep [opciones] [patrón] [archivo]
```

Donde

- `grep`: Es el comando.
- `[opciones]`: Son las opciones que se pueden utilizar.
- `[patrón]`: Es el patrón que se desea buscar.
- `[archivo]`: Es el archivo donde se desea buscar el patrón.

1. **Encontrar una palabra en un archivo de texto**: Para buscar una palabra en un archivo de texto, simplemente escribe el comando:

```bash
grep [consulta] [archivo]
```

Donde `[consulta]` es la palabra que se desea buscar y `[archivo]` es el archivo donde se desea buscar la palabra.

Encontrar una palabra sin tener en cuenta las mayúsculas y minúsculas, para hacer esto, se utiliza la opción `-i`:

```bash
grep -i [consulta] [archivo]
```

2. **Conteo de palabras que coinciden con la búsqueda**: Usando el comando `grep` puedes saber cuantas veces se usa una palabra en el archivo de texto. Simplemente agrega la opción `-c` al comando:

```bash
grep -c [consulta] [archivo]
```

3. **Buscar múltiples palabras clave**: Para buscar múltiples palabras clave, se utiliza la opción `-e`:

```bash
grep -e [consulta1] -e [consulta2] [archivo]
```

También se puede utilizar la opción `-f` para buscar múltiples palabras clave, pero en este caso, se debe crear un archivo de texto con las palabras clave que se desean buscar:

```bash
grep -f [archivo] [archivo]
```

También se puede utilizar el meta-carácter `|` para buscar múltiples palabras clave:

```bash
grep [consulta1] [archivo] | grep [consulta2] [archivo]
```

#### Comando `sed`

El comando sed es un editor de texto no interactivo. El comando sed de Linux edita datos basado en las reglas que tú le proporciones, puedes utilizarlo de la siguiente forma

```bash
$ sed options file
```

Además, no tienes la limitación de utilizar sed solo para manipular archivos, también puedes aplicarlo directamente al `stdin` de la siguiente forma

```bash
$ echo "Welcome to LinuxHint" | sed 's/Linux/Unix/'
```

El comando sed reemplaza el primer patrón de texto con el segundo. En este caso, la cadena de texto "Linux" se reemplaza con "Unix".

Archivo cuyo contenido es "This is another test". Para ejecutar múltiples comandos sed, puedes utilizar la opción `-e` de la siguiente forma:

```bash
$ sed -e 's/This/That/' -e 's/test/example/' file
```

Los resultados son impresos en la pantalla instantáneamente, no tienes que esperar que se procese el archivo para terminar.

### 103.8 Realizar las operaciones básicas de edición de archivos utilizando `vi`.

#### Iniciar `vi`

- El editor de texto `vi` es un editor de texto que se encuentra en la mayoría de las distribuciones de Linux. Es un editor de texto muy poderoso y versátil, que puede ser utilizado para editar archivos de texto, archivos de configuración, archivos de código fuente, etc.

Comandos básicos de `vi`

<center><img src="https://media.cheatography.com/storage/thumb/zoltan_basic-vim.750.jpg" width="500"></center>

El editor vi tiene dos modos de operación:

- **Modo de Comando**: En este modo, se pueden ejecutar comandos para moverse por el archivo, borrar, copiar, pegar, etc. Para entrar en este modo, presiona la tecla `ESC`.

- **Modo de Inserción**: En este modo, se puede escribir texto. Para entrar en este modo, presiona la tecla `i`.

Actividades complementarias:

- [Realizar el examen del tópico 3](https://www.goconqr.com/es/quiz/11868178/examen-101-lpi-chapter-3-configuring-hardware)
- [Práctica de ejercicios del tópico 3](laboratorio-3.md)