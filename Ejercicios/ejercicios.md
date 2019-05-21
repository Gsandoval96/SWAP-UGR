# Autor
Realizados por Guillermo Sandoval Schmidt.

## Tema 1

### Ejercicio 1

Buscar información sobre las tareas o servicios web para los
que se usan más los programas que comentamos al
principio de la sesión:

- Apache: es un servicio de código abierto (lo cuál le aporta una gran configurabilidad) cuya finalidad principal es la de servir páginas web.

- nginx: se usa principalmente como balanceador de carga y como un proxy para protocolos de correo eléctrónico (como IMAP/POP3). Es usado por algunos sitios web muy conocidos como pueden ser: WordPress, Netflix o GitHub.

- thttpd: es simple, sencillo, rápido y seguro. Estos motivos lo hacen ideal para servir grandes cantidades de información estática.

- Cherokee: está escrito en C y está bajo una Licencia Pública General de GNU. La versión básica es rápida y funcional, aunque soporta complemento que añaden diversas funcionalidades.

- Node.js: no se limita a poder desarrollar servidores web y es flexible y rápido.

## Tema 2

### Ejercicio 1

| Componente             | Inicial    | An          | An-1                    |
| ---------------------- | ---------- | ----------- | ----------------------- |
| Web                    | 85,0000%   | 97,7500%    | 99,6625000%             |
| Aplicacion             | 90,0000%   | 99,0000%    | 99,9000000%             |
| DB                     | 99,9000%   | 99,9999%    | 99,9999999%             |
| DNS                    | 98,0000%   | 99,9600%    | 99,9992000%             |
| Firewall               | 85,0000%   | 97,7500%    | 99,6625000%             |
| Switch                 | 99,0000%   | 99,9900%    | 99,9999000%             |
| Centro de datos        | 99,9900%   | 99,9900%    | 99,9900000%             |
| ISP                    | 95,0000%   | 99,7500%    | 99,9875000%             |
|                        |            |             |                         |
| Sistema                | *          | *           | 99,20360%               |

### Ejercicio 2

Buscar frameworks y librerías para diferentes lenguajes que
permitan hacer aplicaciones altamente disponibles con
relativa facilidad.

- PM2: es un gestor de procesos de producción para las aplicaciones Node.js que tiene un equilibrador de carga incorporado. PM2 permite mantener siempre activas las aplicaciones y volver a cargarlas sin ningún tiempo de inactividad, a la vez que facilita tareas comunes de administrador del sistema. PM2 también permite gestionar el registro de aplicaciones, la supervisión y la agrupación en clúster.

- Forever: este gestor de procesos permite que un script se ejecute de manera continua sin interrupciones.

- StrongLoop Process Manager:  es un gestor de procesos de producción para las aplicaciones Node.js. StrongLoop PM tiene incorporado un despliegue de equilibrio de carga, supervisión y varios hosts, así como una consola gráfica. Puede utilizar StrongLoop PM para las siguientes tareas

## Tema 3

### Ejercicio 1

Buscar con qué órdenes de terminal o herramientas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.

Para Windows podemos usar:

	route ADD [destino] MASK [mascara] [gateway] [metrica]

Para Linux podemos usar:

	route add -net [destino] netmask [mascara] gw [gateway]

Con estos comandos se añaden rutas estáticas que permiten redirigir el tráfico de una subred a otra estableciendo una gateway por defecto por la que saldrá el tráfico.

## Tema 5

### Ejercicio 1

Buscar información sobre cómo calcular el número de conexiones por segundo.

He encontrado dos maneras de calcular las conexiones, la primera sería utilizar el comando *netstat*:

	netstat | grep http | wc -l

La segunda forma es aprovechando las capacidades del servicio que estemos usando, concretamente, en *Apache* y *nginx* podemos modificar el archivo de configuración e indicarle que imprima el número de conexiones por segundo.

## Tema 6

### Ejercicio 3

Buscar información acerca de los tipos de ataques más comunes en servidores web. Detallar en qué consisten, y cómo se pueden evitar.

- DDos: Una ampliación del ataque DoS es el llamado ataque de denegación de servicio distribuido, también llamado DDoS (por sus siglas en inglés, Distributed Denial of Service) el cual se lleva a cabo generando un gran flujo de información desde varios puntos de conexión hacia un mismo punto de destino. Ambos tienen como objetivo sobrecargar el sistema y por consecuente, no dejar espacio a las peticiones reales de los usuarios.

- Phising: es un método suplanta la identidad de un sitio web de confianza para que el usuario revele información personal, como contraseñas o datos de tarjetas de crédito. La principal defensa ante el phising es no utilizar url "extrañas", mantener actualizados los parches de seguridad y principalmente, mantener buenos hábitos en cuanto a no abrir adjuntos de correos que no sean de confianza o no dar información personal.

- MITM: Un ataque Man-In-The-Middle es un ataque en el que se consigue la capacidad de leer, modificar y reenviar datos a voluntad. De esta forma se puede acceder al contenido privado como, por ejemplo, datos confidenciales y contraseñas. Para más info: [](https://github.com/Gsandoval96/SWAP-UGR/tree/master/Trabajo)
