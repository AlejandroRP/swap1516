

# **PRACTICA 4**


En esta práctica vamos a comprobar el rendimiento de los distintos balanceadores de carga que hemos instalado en prácticas anteriores. Utilizaremos Apache Benchmark y Siege en los servidores con los balanceadores (Nginx y Haproxy) y mediremos también el rendimiento de un único servidor. Con todos estos datos podremos sacar conclusiones sobre las ventajas de utilizar balanceador para montar una granja web.

###Apache Benchmark
La orden para utilizar Apache Benchmark es la siguiente:

`ab -n 1000 -c 10 http://192.168.25.130/script.php`

El script que vamos a ejecutar hará que cada petición lleve un tiempo no despreciable y así tomar medidas significativas. Este es el contenido:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/scriptphp.JPG?raw=true)

Hemos elegido las métricas de Apache Benchmark "Tiempo total de ejecución", Tiempo medio para completar cada petición" y "Número de peticiones procesadas por segundo". Estos son los resultados con Apache Benchmark:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/Tablas%20-%20ApacheBenchmark.JPG)

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/Gr%C3%A1ficas%20-%20ApacheBenchmark.JPG)

Las conclusiones sobre los resultados obtenidos están al final de la memoria.


###Siege
La orden para utilizar Siege es la siguiente:

`siege -b -t60S -v 192.168.25.130/script.php`

Hemos elegido las métricas de Siege [] [] y [] porque []. Estos son los resultados con Siege:

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/Tablas%20-%20SIEGE.JPG)

![imagen](https://github.com/AlejandroRP/swap1516/blob/master/Practica4/Gr%C3%A1ficas%20-%20SIEGE.JPG)

Observando los resultados de cada ejecución, y las medidas estadísticas de estos, podemos concluir que utilizar uno u otro balanceador no supone una diferencia de rendimiento. Es evidente la diferencia que supone utilizar balanceador (que equivale a dos o más servidores que se reparten el trabajo) frente a no utilizarlo (un único servidor). La ganancia en rendimiento llega aproximadamente al doble. Dicho valor no crece siempre linealmente, es decir, cuantos más servidores tengamos, el incremento de la ganancia no será igual de escalado como podríamos esperar.

##Nota final
No podemos comparar los balanceadores entre sí porque ambos tienen una forma muy diferente de funcionar, de realizar los tests... así como los resultados que presentan.

###Fuentes:
[Speed testing your website with Siege: Part  One](https://www.euperia.com/website-performance-2/speed-testing-your-website-with-siege-part-one/720)

[Benchmarking and Load Testing with Siege](http://blog.remarkablelabs.com/2012/11/benchmarking-and-load-testing-with-siege)
