
# **PRÁCTICA 6: Discos en RAID**

En esta práctica configuraremos dos discos en RAID 1 por software, usando una
maquina virtual con Ubuntu 12.04 server. Esta configuración RAID ofrece una gran
seguridad al replicar los datos en los dos discos.

Sólo vamos a necesitar una máquina: M1 o M2.

A esa máquina hay que añadirle dos discos de la misma capacidad para hacer las pruebas con el RAID 1 que vamos a montar. En nuestro caso, utilizamos VMWare Workstation 11:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Pr%C3%A1ctica%206/Im%C3%A1genes/6-1%20Configuraci%C3%B3n%20en%20VMWorkstation.jpg)

Ejecutamos lo siguiente para instalar el software necesario para la configuración del RAID:

` sudo apt-get install mdadm`

Necesitamos buscar la información de los discos que hemos añadido con:

` sudo fdisk -l`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Pr%C3%A1ctica%206/Im%C3%A1genes/6-2%20Informaci%C3%B3n%20de%20discos.jpg)

Para crear el RAID 1 con los discos */dev/sdb* y */dev/sdc*, utilizando en el dispositivo */dev/md0*:

` sudo mdadm -C /dev/md0 --level=raid1 --raid-devices=2 /dev/sdb /dev/sdc`

Ahora vamos a darle formato:

` sudo mkfs /dev/md0`

Para poder utilizar nuestro RAID, lo montamos en un directorio que creamos llamado */dat*
```
  sudo mkdir /dat
  sudo mount /dev/md0 /dat
```

Para comprobar que hemos hecho todo correctamente hasta ahora, utilizamos:

` sudo mount` y `sudo mdadm --detail /dev/md0`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Pr%C3%A1ctica%206/Im%C3%A1genes/6-4%20Informaci%C3%B3n%20del%20RAID%20sin%20fallos.jpg)

Ya está. Sólo falta hacer que se monte automáticamente al arrancar el sistema. Hay que editar el archivo */etc/fstab* añadiendo una línea. Antes de escribir nada, necesitamos saber el UUID de *md0*. Ejecutamos:

` ls -l /dev/disk/by-uuid`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Pr%C3%A1ctica%206/Im%C3%A1genes/6-3%20Informaci%C3%B3n%20de%20discos%202.jpg)

Anotamos el UUID (se parece a *ccbbbbcc-dddd-eeee-ffff-aaabbbcccddd*). Añadimos la siguiente línea en el archivo */etc/fstab*:

` UUID=ccbbbbcc-dddd-eeee-ffff-aaabbbcccddd /dat ext2 defaults 0 0`

---

Ya está funcionando nuestro RAID 1. Ahora podemos simular un fallo en uno de los discos, quitarlo "en caliente" y añadir otro (o el mismo) para que ocupe su lugar con estas órdenes:
```
  sudo mdadm --manage --set-faulty /dev/md0 /dev/sdb
  sudo mdadm --manage --remove /dev/md0 /dev/sdb
  sudo mdadm --manage --add /dev/md0 /dev/sdb
```
Y para ver la información del RAID, utilizábamos:
```
  ` sudo mount` y `sudo mdadm --detail /dev/md0`
```

Para hacer una prueba sobre el correcto funcionamiento del RAID, tan sólo hace falta crear o guardar un archivo de cualquier tipo en */dat*. Nuestro RAID 1 nos garantiza el acceso a dicho archivo porque replica todo lo que haya en */dat*, así que basta con utilizar las órdenes de arriba para:
1. Simular un fallo en uno de los discos (primera orden, opcionalmente la segunda también), y comprobar el contenido de */dat*. Si podemos acceder a él y a todos sus archivos, significa que estamos utilizando la información de backup del otro disco.
2. Restaurar el RAID añadiendo en caliente el disco que retiramos antes (tercera orden). Esperar a que se reconstruya.
3. Repetir el paso 1 y 2 haciendo fallar al otro disco.
4. Si hacemos que fallen ambos discos, o deshacemos el RAID, veremos que */dat* no es accesible.
