

# **PRACTICA 2**


Para la realizacion de la practica basicamente se han seguido los pasos del guion, al probar el funcionamiento de rsyn este no funcionaba porque lo estabamos haciendo como root y no lo habiamos configurado previamente para esto, asi que finalmente lo hicimos en modo usuario pero para que funcionara debiamos darle permisos al directorio web(**/var/www/**) de cada maquina con la orden **chown usuario:usuario -R /var/www/** 

*Cambio de dueño del directorio*
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica2/Imagenes/1-1%20Cambiar%20due%C3%B1o%20del%20directorio%20-var-www-.JPG)

*Resultado de la orden rsync*
Ejecutado desde la maquina 2.
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica2/Imagenes/1-2%20Resultado%20final%20rsync.JPG)

*Creacion de las claves compartidas con keygen*
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica2/Imagenes/1-3%20Creando%20claves%20con%20keygen.JPG)

*Cambio de permisos authorized-keys*
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica2/Imagenes/1-4%20Cambiando%20permisos%20a%20authorized-keys.JPG)

*Configuramos ssh en la maquina 1 para que la maquina 1 acceda a esta*
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica2/Imagenes/1-5%20ssh%20configurado.JPG)

*Configuramos ssh en la maquina 2 para que la maquina 1 acceda a esta*
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica2/Imagenes/1-5%20ssh%20configurado%20M2.JPG)
