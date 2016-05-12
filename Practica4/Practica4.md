

# **PRACTICA 4**


En esta practica vamos a comprobar el rendimiento de los servidores web que hemos instalado anteriormente, para ello utilizaremos Apache Benchmark y Siege en los servidores con balenceadores de carga distintos(Nginx,Haproxy y sin balanceador a un servidor solo).

**Servidor Único con Apache Bencmark**
`ab -n 1000 -c 10 http://192.168.25.128/script.php`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/AB-Servidor%20Unico.PNG)


**Nginx con Apache Bencmark**
`ab -n 1000 -c 10 http://192.168.25.130/script.php`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/AB-Nginx.PNG)  


**Haproxy Único con Apache Bencmark**
`ab -n 1000 -c 10 http://192.168.25.130/script.php`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/AB-%20Haproxy.PNG)



**Comparamos el rendimiento**
![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/Grafica%20Apache%20Benchmark.PNG)


---------------------------------------------------------------------------------

**Servidor Único con Siege**
`./siege -b -t60s -v http://192.168.25.128/script.php`

**Nginx con Siege**
`./siege -b -t60s -v http://192.168.25.130/script.php`


**Haproxy Único con Siege**
`./siege -b -t60s -v http://192.168.25.130/script.php`    


