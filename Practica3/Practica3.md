

# **PRACTICA 3**


*El archivo de configuracion de Nginx se queda de la siguiente forma:*
![imagen](Fotoconfiguracion)


Despues de instalar y configurar nginx vemos las respuestas al comando curl IP-Balanceador con nginx 

Reparto equitativo RoundRobin:

![imagen]()

Reparto ponderacion 1 - 2:

![imagen]()

-------------------------
*Instalamos y configuramos Haproxy

Configuracion del archivo /etc/haproxy/haproxy.cfg :
![imagen]()

Resultado de curl IP-Balanceador con Haproxy

![imagen]()

-------------------------

*Instalamos Pound para balancear la carga*
http://www.cyberciti.biz/faq/linux-http-https-reverse-proxy-load-balancer/

sudo apt-get install pound

Y lo configuramos de la siguiente manera:

nano /etc/pound/pound.cfg

![imagen](Fotopound)

Y reseteamos:
# /etc/init.d/pound restart

Para que no se inicie la configuracion por defecto tenemos que poner el parametro statup del archivo etc/default/pound 
![imagen](foto2 pound)


