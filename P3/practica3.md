# Practica 3. Balanceo de carga
Realizada por Elena María Gómez Ríos y Guillermo Sandoval Schmidt.

## Objetivos
- Configurar una máquina e instalar el `nginx` como balanceador de carga.
- Configurar una máquina e instalar el `haproxy` como balanceador de carga.
- Someter a la granja web a una alta carga, generada con la herramienta `Apache Benchmark`, teniendo primero `nginx` y después `haproxy`.

## Instalación y configuración de nginx
Lo primero que tenemos que hacer es crearnos otra máquina virtual, en nuestro caso M3-B, que no tenga instalado Apache para que no ocupe el puerto 80.

Una vez creada configuramos las redes como hicimos en la práctica 1, para que las máquinas se vean entre ellas.

![](img/1.png)

Para instalar `nginx` hacemos lo siguiente, cómo se indica en el guión de prácticas:

```
sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove
sudo apt-get install nginx
sudo systemctl start nginx
```

Una vez se ha instalado correctamente `nginx` procedemos a su configuración como balanceador de carga.

Para ello tenemos que modificar el fichero de configuración `/etc/nginx/conf.d/default.conf`, si existe el fichero tenemos que eliminar el contenido que tenga y si no existe lo creamos con el siguiente contenido:

![](img/2.png)

Para asegurarnos de que `ngnix` no funcione como servidor web tenemos que comentar la siguiente línea en el archivo `/etc/nginx/nginx.conf`:

![](img/3.png)

Una vez se ha configurado lanzamos el servicio `nginx` con `sudo systemctl start nginx`, si no sale ningún mensaje de error es que todo está correcto y podemos probar el balanceador haciendo peticiones a la IP de esta máquina. Se puede observar como el balanceador reparte el trabajo. En vez de modificar el index.html de cada máquina, hemos modificado el contenido de hola.html y por ello para comprobar el funcionamiento ponemos curl IP/hola.html.

![](img/4.png)

## Instalación y configuración de HAProxy
Al igual que hicimos para nginx, creamos una máquina virtual, en este caso M3-B2, que no tenga instalado LAMP y configuramos la red, dándole la misma IP que a la máquina M3-B.

Una vez creada la máquina instalamos `HaProxy` con `sudo apt-get install haproxy`.

Ahora procedemos a realizar la configuración de HaProxy como balanceador de carga modificando o creando el archivo `/etc/haproxy/haproxy.cfg` con el siguiente contenido:

![](img/5.png)

Lanzamos el servicio haproxy mediante el comando `sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg`. Al ejecutar el comando salen 3 warning por utilizar directivas obsoletas, por lo que si no queremos que nos salgan los warnig podemos cambiar el archivo `/etc/haproxy/haproxy.cfg` de la siguiente forma:

![](img/6.png)

![](img/7.png)

Ahora probamos que el balanceador funciona correctamente con curl, a igual que hicimos con nginx:

![](img/8.png)

## Someter a una alta carga el servidor balanceado con ab

### Nginx como servidor balanceado con round-robin
Ejecutamos `ab -n 100000 -c 10 http://192.168.2.121/hola.html` en nuestra máquina anfitriona y comprobamos como afecta el nivel de peticiones a cada elemento de la granja web con el comando `htop`.

<img src="img/10.png" width="430"/> <img src="img/11.png" width="430"/>

<img src="img/12.png" width="430"/> <img src="img/13.png" width="430"/>
<img src="img/9.png" width="430"/>

Se puede observar que la CPU del balanceador está prácticamente al 100% mientras que en las máquinas M1 y M2 está al 50% ya que la carga está repartida entre ambas máquinas.

### Nginx como servidor balanceado con ponderación
En este caso supondremos que la máquina 1 tiene el doble de capacidad que la máquina 2. Para que nginx funcione con ponderación tenemos que cambiar el archivo de configuración `/etc/nginx/conf.d/default.conf` de la siguiente forma:

![](img/14.png)

<img src="img/18.png" width="430"/> <img src="img/19.png" width="430"/>

<img src="img/16.png" width="430"/> <img src="img/17.png" width="430"/>
<img src="img/15.png" width="430"/>

En este caso se puede observar como el uso de la CPU de la máquina M1 es mayor que el de la máquina M2.

### Haproxy como servidor balanceado con round-robin
De igual forma que hicimos con el balancedor `nginx` ejecutamos `ab -n 100000 -c 10 http://192.168.2.121/hola.html` en nuestra máquina anfitriona y comprobamos como afecta el nivel de peticiones a cada elemento de la granja web con el comando `htop`.

<img src="img/23.png" width="430"/> <img src="img/24.png" width="430"/>

<img src="img/21.png" width="430"/> <img src="img/22.png" width="430"/>
<img src="img/20.png" width="430"/>

Se puede observar que la CPU del balanceador está prácticamente al 100% mientras que en las máquinas M1 y M2 está al 50% ya que la carga está repartida entre ambas máquinas.

### Haproxy como servidor balanceado con ponderación
Para que el balanceador haga la ponderación dando mas peso a la máquina M1 tenemos que cambiar el archivo de configuración `/etc/haproxy/haproxy.cfg` con el siguiente contenido:

![](img/25.png)

<img src="img/29.png" width="430"/> <img src="img/30.png" width="430"/>

<img src="img/27.png" width="430"/> <img src="img/28.png" width="430"/>
<img src="img/26.png" width="430"/>

En este caso se puede observar como el uso de la CPU de la máquina M1 es mayor que el de la máquina M2.

### Comparación de tiempos
Hemos lanzado 100000 peticiones para comprobar un alto volumen. Consideraremos el tiempo total del test para nuestro análisis. Los resultados obtenidos han sido los siguientes:

| Balanceador          | Algoritmo Balanceo  | Tiempo(s)| Media de tiempo por petición(ms) |
| -------------------- | ------------------- | -------- | -------------------------------  |
| Nginx                | round-robin         | 70.888   | 7.089                            |
| Nginx                | ponderación         | 68.457   | 6.846                            |
| HAProxy              | round-robin         | 54.509   | 5.451                            |
| HAProxy              | ponderación         | 57.025   | 5.703                            |

Como se puede observar el balanceador HaProxy es más rápido que Nginx.
