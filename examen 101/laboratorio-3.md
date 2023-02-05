# Laboratorio 3 - Tópico 3 - Examen 101

1. A continuación se muestran los primeros comandos con los que Ud. deberá estar familiarizado:          

- `date`: Muestra la fecha y la hora del sistema.
- `w`: Muestra usuarios conectados y qué están ejecutando.
- `who`: Muestra quienes están usando el sistema.

**Nota**: Utilice el manual (`man`) o la ayuda (`--help`) para ver las opciones y argumentos que soportan los comandos utilizados en el laboratorio.

Veamos otro comando:

```bash
who

root      tty3      2011-02-23 09:16
root      :0         2010-02-23 09:16
```

- ¿Qué función cumple dicho comando? ¿Qué información muestra?

- ¿Qué diferencia hay entre utilizar el comando `who` y `w`?

- ¿Qué diferencia hay entre utilizar el comando `man` y `help`?

2. **ESTRUCTURA DEL SISTEMA**

- Ejecute el comando `df` y complete la información de lo enmarcado:

    - ¿Qué tipo de disco duro tiene? SATA o IDE
    
    - Ubicándonos en la raíz y visualizando la estructura de directorios:
        
        ```bash
        cd /
        ls -l
        ``` 

    ¿Qué es lo que observa cuando ejecuta esta operación?

3. **OPERACIONES CON COMANDOS**

Realizaremos operaciones con comandos. Con apoyo de su texto pruebe los comandos `ls`, `cd`, `cp`, `rm`, `mkdir`.

- En una consola o terminal:

    - Listando directorio donde está ubicado: `ls`

    - Listando directorios específico: `ls /etc`, `ls /`

    - Distinguir entre directorio y archivos. Los directorios finalizan con `/`. Ejemplo: `ls -l /etc/`

    - Para mostrar los archivos ocultos. Los archivos ocultos empiezan con un punto, al crear un archivo con un nombre que empieza por punto automáticamente es oculto. Ejemplo: `ls  -a  /root`.

4. **DESPLAZAMIENTO**

En una consola o terminal:

- Ubicándose en un directorio `/etc`: `cd /etc`

**Nota:** Observe que para tener un punto de referencia para desplazarme uso la raíz que es simbolizado por “/” seguido luego a la ubicación donde quiero ubicarme.

**Nota**: Nota: Si está dentro de un directorio y quiere desplazarse a un subdirectorio,  puede obviar la referencia raíz `/` e indicar el nombre del subdirectorio únicamente. Ejemplo para el directorio “sysconfig”:

```bash
# (En Centos)
cd  /etc 
ls –l  sysconfig
# Para ingresar al subdirectorio “sysconfig” :
cd  sysconfig
```

- Para salir de un directorio: `cd ..`

5. **MANIPULACIÓN DE ARCHIVOS Y DIRECTORIOS (CREAR)**

En una consola o terminal:

**Nota**: Usando los comandos de creación de directorios y archivos se generará la estructura mostrada

- Ubicándose en la raíz `/` y generando el directorio `data`

```bash
cd /
mkdir data
```

- Ubíquese en el directorio `data` y genere los archivos `docu1` y `docu2`:

```bash
cd data
# echo “Linux Lima”  >  docu1
# echo “Linux Tacna”  > docu2
```

**Nota:** El comando “touch” también genera un archivo pero en blanco: `touch docu1`.

Visualizando el listado de “data”: `ls -l`

6. **MANIPULACIÓN DE ARCHIVOS Y DIRECTORIOS (COPIAR)**

En una consola o terminal:

- Copiar Archivo

```bash
cd /data
cp  docu1 archi1
ls
```

- Copiar un directorio en forma recursiva (Todo el contenido del directorio):

```bash
cp –f –r /data  /copia
ls /copia
```

**Nota**: Opciones (-f) no solicita confirmación, (-r) toma toda la información de la estructura.

7. **MANIPULACIÓN DE ARCHIVOS Y DIRECTORIOS (BORRAR)**

En una consola o terminal:

- Borrar  archivo

```bash
cd /data
rm archi1
```

- Borrar Directorio

```bash
cd /
rm –f  -r  data
```

**Nota**: Opciones (-f) no solicita confirmación, (-r) toma toda la información de la estructura.

8. Coloque el comando:

```bash
uptime
```

¿Qué es lo que realiza?

9. Se puede verificar el estado de los procesos con el comando `ps`. Para mostrar todos los procesos que están corriendo ejecute el comando `ps –ef` (Este comando es común en los sistemas Unix). Note que los procesos demonios muestran un signo de interrogación (?) en el campo `tty`:

```bash
ps –ef  |  more
```

¿Qué se visualiza con esta opción?

10. En Linux se utiliza mayormente el comando `ps –aux`.  Note la diferencia entre los dos comandos anteriores.  Solo se mostraran las primeras líneas

```bash
# ps –ef  |  head
# ps –aux  |  head
```

¿Qué información adicional relevante le proporciona el comando `ps –aux`?

11. Cree el usuario `francisco` y desde otra consola ingrese con este usuario y ejecute el editor vi.
Analicemos cada una de las opciones del comando `ps –aux`.

```bash
# ps 
# ps –a
# ps –au
# ps –aux  |  more
```

Anote las diferencias que encontró al ejecutar estos comandos:

12. Un comando similar pero que funciona en forma interactiva es el comando top: Ejecute este comando:

```bash
# top	(Revise su texto y identifique los comandos disponibles)
```

- Ordene la información mostrada por uso de Procesador. ¿Qué comando utilizó?

- Ordene la información mostrada por uso de Memoria. ¿Qué comando utilizó?	

Presione la tecla `q` para salir.

13. Muestre el uso de memoria física y swap. Muestre la información en megabytes):

```bash
# free –m
```
- Mate los procesos asociados a este terminal (recuerde respetar la genealogía de proceso)

```bash
# kill –15  pid. (el PID del VI)
```

Muestre que el programa finalizó sin ningún problema.

- Ejecute nuevamente el programa vi en una terminal y en la otra mate el proceso:

```bash
# kill –9  pid.
```

¿Cuál es la diferencia entre kill –15 y kill –9? (Investigue)

14. Usando filtros y redireccionamiento realice un listado de todos los paquetes instalados en forma ascendente y enviarlo a un archivo llamado reporte4.
	
