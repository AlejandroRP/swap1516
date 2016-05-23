

# **PRÁCTICA 5: Réplica de bases de datos MySQL**

En esta práctica vamos a alojar una base de datos en nuestra granja web. Lo haremos de tal forma que el primer servidor web (M1) contenga la base de datos, y el segundo (M2) actúe de servidor de backup. Esto nos dará mayor fiabilidad frente a fallos totales que, tarde o temprano, ocurrirán.

Vamos a hacerlo de dos formas: manual y automáticamente.

###Forma manual

Lo primero que hay que hacer es crear una base de datos en M1 y rellenarla de algunos datos. Ejecutamos lo siguiente:

  `mysql -uroot -p`
  
[Introducimos la contraseña del usuario root]
```sql
  mysql> create database contactos;
  mysql> use contactos;
  mysql> create table datos(nombre varchar(100), tlf int);
  mysql> insert into datos(nombre, tlf) values ("pepe", 958818293);
  mysql> insert into datos(nombre, tlf) values ("nombre2", 958818293);
  mysql> insert into datos(nombre, tlf) values ("nombre3", 958818293);
  mysql> insert into datos(nombre, tlf) values ("nombre4", 958818293);
```

Podemos comprobar qué hemos insertado con:

```sql
  mysql> select * from datos;
```

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica5/5-1-1%20Base%20de%20datos.JPG)

Ahora vamos a clonar esta base de datos con MySQLDump. Primero, tenemos que bloquear las tablas de la base de datos para que haya datos modificándose mientras hacemos el proceso de clonado:

```sql
  mysql> FLUSH TABLES WITH READ LOCK;
  mysql> quit
```

Fuera de mysql, guardamos los datos listos para ser exportados:
```
  mysqldump contactos -u root -p > /root/ejemplodb.sql
```

Y ahora desbloqueamos las tablas para que puedan seguir siendo utilizadas:

````
mysql -u root -p
```
```sql
  mysql> UNLOCK TABLES;
  mysql> quit
```

En la máquina esclava (M2) ejecutamos lo siguiente:

  `mysql -u root -p`
```sql
  mysql> CREATE DATABASE 'contactos';
  mysql> quit
```

  `mysql -u root -p contactos < /root/ejemplodb.sql`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica5/5-1-2%20BD%20en%20Maquina2%20tras%20hacerlo%20manual.jpg)

###Forma automática
Para no tener que hacer a mano el proceso anterior cada vez que queramos actualizar la copia de seguridad que tengamos, o para hacer una nueva, podemos configurar el demonio de MySQL para hacerlo automáticamente. Partiendo del punto anterior, en M1, editamos el archivo */etc/mysql/my.cnf* de la siguiente forma:

######NOTA: se recomienda ENCARECIDAMENTE hacer una copia de la imagen del sistema (o de la máquina virtual) llegados a este punto puesto que los errores de SQL son tediosos, fáciles de provocar y difíciles de arreglar.

1. Comentamos el parámetro bind-address
2. Establecemos el archivo `log error = /var/log/mysql/error.log`
3. Establecemos el identificador del servidor: `server-id = 1`
4. Establecemos el archivo `log_bin = /var7log/mysql-bin.log`

Después, reiniciamos el servicio de MySQL con:
  `/etc/init.d/mysql restart`

Todo debería funcionar hasta ahora. En la M2, editamos el mismo archivo y de la misma forma salvo por el `server-id`, que será `2`. Nuestras máquinas funcionan con una versión de SQL superior a la 5.5, así que no tenemos que editar más por ahora este archivo de configuración.

En el esclavo, además, tenemos que reiniciar el servicio de MySQL con:
  `/etc/init.d/mysql restart`

Si todo ha ido bien, ~~hacemos otra copia de seguridad de las máquinas virtuales~~ ejecutamos lo siguiente en el maestro (M1):
```sql
  mysql> CREATE USER esclavo IDENTIFIED BY 'esclavo';
  mysql> GRANT REPLICATION SLAVE ON *.* TO 'esclavo'@'%' IDENTIFIED BY 'esclavo';
  mysql> FLUSH PRIVILEGES;
  mysql> FLUSH TABLES;
  mysql> FLUSH TABLES WITH READ LOCK;
```

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica5/5-2-1%20Estableciendo%20esclavo%20a%20la%20M2%20desde%20la%20M1.jpg)

En M2, ejecutamos:
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica5/5-2-1-2%20Estableciendo%20esclavo%20a%20la%20M2%20desde%20la%20M1%20-%20final.jpg)

Finalmente, ejecutamos en M2:

```sql
mysql> START SLAVE;
```

Y en M1, para desbloquear las tablas, lo siguiente:
```sql
mysql> UNLOCK TABLES;
```

Para comprobar si el esclavo está funcionando adecuadamente, ejecutamos en M2:
```sql
mysql> SHOW SLAVE STATUS\G
```

Y si la variable `Seconds_Behind_Master`es distinto de null, significa que hemos hecho todo correctamente. 

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica5/5-2-2%20Esclavo%20establecido.jpg)

---

Podemos probar nuestra configuración automática introduciendo valores nuevos en la base de datos del maestro (M1) y después comprobando si se han copiado en el esclavo (M2):

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica5/5-2-3%20Comprobacion.jpg)



