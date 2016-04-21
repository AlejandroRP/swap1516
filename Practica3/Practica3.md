

# **PRACTICA 3**

**Instalamos y configuramos Ngix**
Vamos a configurar Nginx con dos algoritmos de balanceo simples: round robin y por pesos. El archivo de configuración de Nginx RoundRobin se queda de la siguiente forma:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-1%20Configuracion%20NGINX%20RoundRobin.JPG)

El archivo de configuración de Nginx ponderación 1 -2 se queda de la siguiente forma:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-3%20Configuracion%20NGINX%20ponderacion.JPG)

Ahora vemos las respuestas al comando `curl IP-Balanceador` con nginx: 

Reparto equitativo RoundRobin:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-2%20Funcionamiento%20NGINX%20RoundRobin.JPG)

Reparto ponderacion 1 - 2:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-4%20Funcionamiento%20NGINX%20ponderacion.JPG)

-------------------------

**Instalamos y configuramos Haproxy**

Vamos a hacer lo mismo con Haproxy. Así se quedará el archivo de configuración `/etc/haproxy/haproxy.cfg` Round Robin:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-1%20Configuracion%20HAPROXY%20RoundRobin.JPG)

Resultado de `curl IP-Balanceador` con Haproxy Round Robin:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-2%20Funcionamiento%20HAPROXY%20RoundRobin.JPG)

Configuración del archivo `/etc/haproxy/haproxy.cfg` con pesos pesos 1 - 3:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-3%20Configuracion%20HAPROXY%20ponderacion.JPG)

Resultado de `curl IP-Balanceador` con pesos 1 - 3:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-4%20Funcionamiento%20HAPROXY%20ponderacion.JPG)

-------------------------

*Instalamos Pound y lo configuramos para balancear la carga*

`sudo apt-get install pound`

Y lo configuramos primero con un algoritmo de pesos, editando su archivo de configuración:

`nano /etc/pound/pound.cfg`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-3-1%20Configuracion%20POUND%20prioridades.JPG)

Arrancamos el servicio de Pound:

`/etc/init.d/pound restart`

Para que Pound pueda funcionar con una configuración personalizada hace falta modificar el valor del parámetro `startup` a 1 en el archivo de configuración localizado en`etc/default/pound`.

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-3-2%20Modificar%20startup%3D1.JPG)

Resultado de `curl IP-Balanceador` con Pound pesos 1 - 4:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-3-3%20Funcionamiento%20POUND%20prioridades.JPG)

**Glosario de órdenes para iniciar y apagar los balanceadores**

Nginx:

`service nginx restart`

`service nginx stop`

Haproxy:

`/usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg`

`/etc/init.d/haproxy stop`

Pound:

`/etc/init.d/pound restart`

`service pound stop`


**Referencias:**

[Linux install and configure pound reverse proxy for Apache http / https web server](http://www.cyberciti.biz/faq/linux-http-https-reverse-proxy-load-balancer/)

[How To Use HAProxy to Set Up HTTP Load Balancing on an Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-use-haproxy-to-set-up-http-load-balancing-on-an-ubuntu-vps)

[pound(8) - Linux man page](http://linux.die.net/man/8/pound)
