# Laboratorio 2 - Tópico 2 - Examen 101

1. Ingrese a la ruta `/var/log`. Haga un listado de lo que tenga la carpeta, que observa?

2. **MONITOREANDO ESPACIO**

   - Verificar el espacio utilizado por algunos directorios.

     - ¿Cuál es el espacio utilizado por el directorio `/bin`?

     - ¿Cuál es el espacio utilizado por el directorio `/usr`?

     - ¿Qué comandos utilizó para obtener esta información?

3. ¿Qué diferencia puede encontrar al ejecutar el comando `df -h` y ver el contenido del archivo `cat /proc/partitions`.?

4. ¿Cuántos puntos de montaje tiene actualmente el sistema operativo?

5. Ingrese a la ruta `/usr/bin` y haga un listado. Luego coloque lo siguiente:

```bash
ldd cat
ldd more
ldd less
```

¿Qué es lo que se muestra al colocar esta información?

6. ¿Cuántos paquetes tiene el repositorio de ubuntu?

7. Listando la relación de todos los programas instalado: (En Centos)

```bash
rpm –qa
```

Anote el nombre de dos programas

```bash
rpm –ql  firefox
```

**Nota**: Aparecerá una relación extensa. Para generar pausa puede usar el comando more:  `#rpm  -ql firefox  |  more`. ¿Qué es lo que aparece?

Ahora volviendo a consultar en los REPOSITORIOS e instalar:
`# yum –y install mc`. ¿Qué es lo que aparece al momento de instalar?

8. Actualice la lista del Ubuntu e instale el paquete `apache2`.

9. Realice la búsqueda del paquete `python3` usando Ubuntu