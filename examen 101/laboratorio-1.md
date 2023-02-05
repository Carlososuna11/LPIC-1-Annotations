# Laboratorio 1 - Tópico 1 - Examen 101

1. **Comando `lsmod`**.  
    - ¿Cuántos módulos tiene el kernel?

2. **Comando `modinfo`**. 
    - Coloque la siguiente sintaxis. `modinfo -d <módulo de la lista del lsmod>`.
    
    - ¿Qué es lo que aparece cuando se ejecuta esta operación?

3. **¿Qué es lo que hace el archivo `/proc/modules`.?** . 
    - ¿Es igual que el anterior comando? 
    - ¿Encontró alguna diferencia? ¿Cual seria si su respuesta es afirmativa?

4. **Comando `lspci`**. 
    - ¿Cuántas ranuras PCI tiene el hardware detectado?

5. **Comando `lsusb`**. 
    - Usar el parámetro -t ¿Qué es lo que muestra?

6. **Comando `dmesg`**. 
    - Realice un listado usando el comando dmesg de los mensajes que tengan “ERROR” sin distinguir la palabra de mayúsculas o minúsculas.
    - Enviar el resultado anterior a un archivo llamado reporte1.txt.

7. **Comando `journalctl`**. 
    - Usando el comando journalctl realice un listado de todos los eventos que tengan la palabra kernel.

8. **Comando `service`**. 
    - ¿Qué es lo que realiza los siguientes comandos? (Ubuntu)
```bash
service apache2 status 
```
```bash
service apache2 start 
```
```bash
service apache2 stop
```