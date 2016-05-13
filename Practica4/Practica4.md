

# **PRACTICA 4**


En esta práctica vamos a comprobar el rendimiento de los distintos balanceadores de carga que hemos instalado en prácticas anteriores. Utilizaremos Apache Benchmark y Siege en los servidores con los balanceadores (Nginx y Haproxy) y mediremos también el rendimiento de un único servidor. Con todos estos datos podremos sacar conclusiones sobre las ventajas de utilizar balanceador para montar una granja web.

###Apache Benchmark
La orden para utilizar Apache Benchmark es la siguiente:

`ab -n 1000 -c 10 http://192.168.25.130/script.php`

El script que vamos a ejecutar hará que cada petición lleve un tiempo no despreciable y así tomar medidas significativas. Este es el contenido:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/scriptphp.JPG?raw=true)

Hemos elegido las métricas de Apache Benchmark [] [] y [] porque []. Estos son los resultados con Apache Benchmark:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/Datos%20-%20ApacheBenchmark.JPG)

Conclusiones molonas aquí []


###Siege
La orden para utilizar Siege es la siguiente:

`siege -b -t60S -v 192.168.25.130/script.php`

Hemos elegido las métricas de Siege [] [] y [] porque []. Estos son los resultados con Siege:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/Datos%20-%20SIEGE.JPG)  

Conclusiones molonas aquí []

##Nota final
No podemos comparar los balanceadores entre sí porque ambos tienen una forma muy diferente de funcionar, de realizar los tests... así como los resultados que presentan.

###Fuentes:
[Speed testing your website with Siege: Part One](https://www.euperia.com/website-performance-2/speed-testing-your-website-with-siege-part-one/720)

[Benchmarking and Load Testing with Siege](http://blog.remarkablelabs.com/2012/11/benchmarking-and-load-testing-with-siege)
