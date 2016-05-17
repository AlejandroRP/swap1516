

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


![imagen]()


