

# **PRÁCTICA 5: Réplica de bases de datos MySQL**

En esta práctica vamos a alojar una base de datos en nuestra granja web. Lo haremos de tal forma que el primer servidor web (M1) contenga la base de datos, y el segundo (M2) actúe de servidor de backup. Esto nos dará mayor fiabilidad frente a fallos totales que, tarde o temprano, ocurrirán.

Vamos a hacerlo de dos formas: manual y automáticamente.

###Forma manual

Lo primero que hay que hacer es crear una base de datos y rellenarla de algunos datos. Ejecutamos lo siguiente:

`mysql -uroot -p`

###Forma automática


