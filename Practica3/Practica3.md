

# **PRACTICA 3**

**Instalamos y configuramos Ngix**

El archivo de configuracion de Nginx RoundRobin se queda de la siguiente forma:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-1%20Configuracion%20NGINX%20RoundRobin.JPG)

El archivo de configuracion de Nginx ponderacion 1 -2 se queda de la siguiente forma:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-3%20Configuracion%20NGINX%20ponderacion.JPG)

Ahora vemos las respuestas al comando `curl IP-Balanceador` con nginx: 

Reparto equitativo RoundRobin:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-2%20Funcionamiento%20NGINX%20RoundRobin.JPG)

Reparto ponderacion 1 - 2:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-1-4%20Funcionamiento%20NGINX%20ponderacion.JPG)

-------------------------

**Instalamos y configuramos Haproxy**

Configuracion del archivo `/etc/haproxy/haproxy.cfg` Round Robin:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-1%20Configuracion%20HAPROXY%20RoundRobin.JPG)

Resultado de `curl IP-Balanceador` con Haproxy Round Robin:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-2%20Funcionamiento%20HAPROXY%20RoundRobin.JPG)

Configuracion del archivo `/etc/haproxy/haproxy.cfg` Ponderacion 1 - 3:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-3%20Configuracion%20HAPROXY%20ponderacion.JPG)

Resultado de `curl IP-Balanceador` con Haproxy ponderacion 1 - 3:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-2-4%20Funcionamiento%20HAPROXY%20ponderacion.JPG)

-------------------------

*Instalamos Pound y lo configuramos para balancear la carga*

`sudo apt-get install pound`

Y lo configuramos de la siguiente manera:

`nano /etc/pound/pound.cfg`

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-3-1%20Configuracion%20POUND%20prioridades.JPG)

Y reseteamos:

`/etc/init.d/pound restart`

Para que no se inicie la configuracion por defecto tenemos que poner el parametro statup a 1 en el archivo `etc/default/pound`.

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-3-2%20Modificar%20startup%3D1.JPG)

Resultado de `curl IP-Balanceador` con Pound ponderacion 1 - 4:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica3/Imagenes/3-3-3%20Funcionamiento%20POUND%20prioridades.JPG)

**Ordenes para iniciar y apagar los balanceadores**

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

http://www.cyberciti.biz/faq/linux-http-https-reverse-proxy-load-balancer/
https://www.digitalocean.com/community/tutorials/how-to-use-haproxy-to-set-up-http-load-balancing-on-an-ubuntu-vps
http://linux.die.net/man/8/pound


