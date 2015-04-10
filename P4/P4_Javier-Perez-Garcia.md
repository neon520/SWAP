## *Práctica 3* 
- Realizado por : 
   + Antonio Solís Izquierdo
   + Javier Pérez García


Empezamos instalando nginx según indica el guión de prácticas


![Captura 1](capturas/1.png)
![Captura 2](capturas/2.png)
 
A continuación configuramos el propio nginx modificando el archivo /etc/nginx/conf.d/default.conf como mostramos en la imagen

![Captura 3](capturas/3.png)

Una vez hecho esto lo probamos (en la imagen podemos observar su ejecución)

![Captura 4](capturas/4.png)

A continuación realizamos la configuración mediante pesos de carga para probarla también

![Captura 5](capturas/5.png)

A continuación procedemos a instalar haproxy.
Primero paramos nginx con el siguiente comando:

	nginx -s stop

Ahora ejecutamos el comando: 

	sudo apt-get install haproxy

Después procedemos a configurarlo modificando el archivo /etc/haproxy/haproxy.cfg y lo ponemos de la siguiente forma:


	global
		daemon
		maxconn 256

	defaults
		mode http
		contimeout 4000
		clitimeout 42000
		srvtimeout 43000

	frontend http-in
		bind *:80
		default_backend servers	

	backend servers	
		server m1 192.168.1.99:80 maxconn 32
		server m2 192.168.1.100:80 maxconn 32


Nota: las IP's puestas son las correspondientes a nuestros servidores.

A continuación comprobamos su funcionamiento:

![Captura 6](capturas/6.png)