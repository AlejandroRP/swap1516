

# **PRACTICA 5**

//// NOTAS ////

Replica servidor: descrita en seccion 5 del pdf conf maestro-esclavo( maquina 1 y maquina 2(las dos con LAMP) )

PASOS:

A)maestro
	/etc/mysql/my.cuf  -Editamos y ponemos id=1

B)esclavo
	/etc/mysql/my.cuf  -Editamos y ponemos id=2

C)maestro
	mysql -uroot -p
		dentro del gestor creamos un usuario esclavo esclavo(usuario/contraseña) cal que daremos permisos para que acceda a la base de datos
D)esclavo

	Dentro de la interfaz mysql -uroot -p lo establecemos como esclavo con la orden TOCHA 
E)Comprobar

	Insertamos cosas en el maestro y vemos que se replican en el esclavo(inserccions, crear tablas)
	en la ventana del esclavo comprobamos con un select que se ha replicado


Para la parte opcional se replican los pasos anteriores en los dos servidores, haciendolos esclavo esclavo

---------------------------------------------

1. Crear una BD con al menos una tabla y algunos datos:

 Podemos hacerlo con la siguiente orden `mysqldump ejemplodb -u root -p > /root/ejemplodb.sql` pero antes tenemos que aseguramos de bloquear la BD porque los datos pueden estar actualizandose, para ello utilizamos la orden `FLUSH TABLES WITH READ LOCK;` para bloquear y luego la orden ` UNLOCK TABLES;` para desbloquear en el terminal de mysql.

 Guardamos los datos mysqldump con la siguiente orden `mysqldump ejemplodb -u root -p > /root/ejemplodb.sql` y podremos ir a la maquina esclavo y copiar los datos guardados con la siguiente orden `scp root@maquina1:/root/ejemplodb.sql /root/`. 


![imagen]()


