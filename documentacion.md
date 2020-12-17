<a id="top"></a>

# Ejercicio 1. EC2.
# ¿Qué es Amazon EC2?

Amazon Elastic Compute Cloud (Amazon EC2) proporciona capacidad de computación escalable en la nube de Amazon Web Services (AWS). El uso de Amazon EC2 elimina la necesidad de invertir inicialmente en hardware, de manera que puede desarrollar e implementar aplicaciones en menos tiempo. 

# ¿Para que sirve?
Se puede usar Amazon EC2 para lanzar tantos servidores virtuales como necesite, configurar la seguridad y las redes y administrar el almacenamiento.

# Documentación

Primero empezaremos a lanzar una instancia.


![Imagen 1](Imagenes/AWS/1.JPG)


Le daremos a free tier y después descargaremos la última versión de el servidor- Ubuntu.


![Imagen 2](Imagenes/AWS/2.JPG)


Elegimos un tipo de instancia y le damos a siguiente:


![Imagen 3](Imagenes/AWS/3.JPG)

Esta página es para configurar las instancias, dejamos como están y damos a siguiente.


![Imagen 4](Imagenes/AWS/4.JPG)

Vamos a añadir 30GB de almacenamiento, que es el máximo permitido, así sacaremos el máximo rendimiento de manera gratuita.


![Imagen 5](Imagenes/AWS/5.JPG)


Seguimos y daremos a next.


![Imagen 6](Imagenes/AWS/6.JPG)


En la configuración de seguridad de grupo, el tipo será de SSH, protocolo TCP y puerto 22. 


![Imagen 7](Imagenes/AWS/7.JPG)


Revisamos si esta todo correcto y le damos a launch.


![Imagen 8](Imagenes/AWS/8.JPG)


En esta ventana tendremos la opción de crear una llave o escoger una existente, en mi caso creare una nueva y llamaré clave2. Esta key tendremos que guardar en un sitio seguro, ya que luego la necesitaremos.


![Imagen 9](Imagenes/AWS/9.JPG)


Le damos a next:


![Imagen 10](Imagenes/AWS/10.JPG)

Se nos descargará la key, el tipo de archivo será ".pem".


![Imagen 11](Imagenes/AWS/11.JPG)


Como podemos ver, se nos ha creado la instancia. Por el momento tenemos detenida.


![Imagen 12](Imagenes/AWS/12.JPG)

Para conectar la instancia, daremos al botón de acciones y damos a conectar.


![Imagen 13](Imagenes/AWS/13.JPG)

Ahora tendremos que darle permisos y ejecutar nuestro DNS público para conectarse a la instancia.


![Imagen 14](Imagenes/AWS/14.JPG)


Hacemos un Git bash en la carpeta donde tenemos guardada la Key, copiamos los permisos y nuestro DNS público. Le daremos a yes:


![Imagen 15](Imagenes/AWS/15.JPG)


Ya estaríamos conectados a la instancia. Podemos comprobar en la página de AWS.


![Imagen 16](Imagenes/AWS/16.JPG)


Como podemos ver, ya estaríamos conectados a la instancia.


![Imagen 17](Imagenes/AWS/17.JPG)


Para detener la instancia, le daremos al botón de acciones y le damos a detener instancia.


![Imagen 18](Imagenes/AWS/18.JPG)

# Ejercicio 2. Instalando aplicaciones. 

# Instalacion de APACHE2, MYSQL, PHP Y FTP.

Primero tenemos que abrir una consola donde tengamos nuestra clave privada y darle permisos: chmod 400 clave2.pem.

Despues nos conectaremos mediante SSH: ssh -i "clave2.pem" ubuntu@ec2-52-55-225-137.compute-1.amazonaws.com

Una vez conectados instalaremos lo siguiente:

## Índice de contenidos

* [Instalar Apache2](#item1)
* [Instalar MySQL](#item2)
* [Instalar PHP](#item3)
* [Instalar FTP](#item4)



<a id="item1"></a>
# Instalar Apache2

Antes que nada haremos un update con el siguiente comando: 

<code> sudo apt-get update</code>


![Apache Instalación](Imagenes/Apache/1.JPG)


Y ahora instalaremos apache con el sigueinte comando:

<code>sudo apt-get install apache2</code>


![Apache Instalación](Imagenes/Apache/2.JPG)

Para comprobar que funciona correctamente primero accederemos al **wizard de AWS** para comprobar que HTTP y HTTPS están habilitados:


![Apache Instalación](Imagenes/Apache/3.JPG)


Una vez aquí clickaremos en Edit:


![Apache Instalación](Imagenes/Apache/4.JPG)


Para acabar, con Add rule añadiremos una regla nueva donde seleccionaremos HTTP en la sección de tipo. Repite este paso para añadir HTTPS:


![Apache Instalación](Imagenes/Apache/5.JPG)

![Apache Instalación](Imagenes/Apache/6.JPG)

Ahora ya podemos comprobar si la instalación del Apache2 se ha hecho de manera correcta, para ello escribe lo siguiente en tu navegador:

<code>http://ip_de_tu_servidor o http://dns_de_tu_servidor</code>


![Apache Instalación](Imagenes/Apache/7.JPG)

Puedes encontrar tu ip o dns en esta sección una vez que la máquina está encendida:

![Apache Instalación](Imagenes/Apache/8.JPG)



<a id="item2"></a>

# Instalar MySQL

Instalaremos MySQL, para ello usaremos este comando: 

<code>sudo apt-get install mysql-server mysql-client</code>

![MYSQL Instalación](Imagenes/MYSQL/1.JPG)

Con este comando instalaremos tanto el servidor como el cliente de MySQL.

Al finalizar la instalación ejecutaremos el siguiente comando:

<code>sudo mysql_secure_installation</code>


![MYSQL Instalación](Imagenes/MYSQL/2.JPG)

Con este comando borraremos algunos parametros peligrosos y aseguraremos el acceso ala base de datos.

Después te pedirá que completes unos pasos. Hazlo de la siguiente manera:


![MYSQL Instalación](Imagenes/MYSQL/3.JPG)


![MYSQL Instalación](Imagenes/MYSQL/4.JPG)



Si quisieramos comprobar tu versión de MySQL puedes hacerlo con esté comando:

<code>mysql --version</code>


![MYSQL Instalación](Imagenes/MYSQL/5.JPG)



<a id="item3"></a>

# Instalar PHP

Ahora toca instalar PHP, para ello comenzaremos con el comando de instalación de nuevo:

<code>sudo apt install php libapache2-mod-php php-mysql</code>

![PHP Instalación](Imagenes/PHP/1.JPG)

Si tus archivos van a ser de tipo .php es recomendable que modifiques el archivo dir.conf para dar prioridad a dicho tipo de archivos.

Para conseguir esto ejecutaremos el siguiente comando:

<code>sudo nano /etc/apache2/mods-enabled/dir.conf</code>


![PHP Instalación](Imagenes/PHP/2.JPG)

Con esto te saldra algo como esto:

![PHP Instalación](Imagenes/PHP/3.JPG)

Cambiaremos de sitio el archivo index.php colocándolo en primer lugar y lo guardaremos con Ctrl+o y saldremos con Ctrl+x:

![PHP Instalación](Imagenes/PHP/4.JPG)

Seguidamente reiniciaremos el servicio de Apache2 para que los cambios se efectuen:

<code>sudo systemctl restart apache2</code>


![PHP Instalación](Imagenes/PHP/5.JPG)


Una vez reiniciado comprobaremos el estado del servicio con este otro comando:

<code>sudo systemctl status apache2</code>

![PHP Instalación](Imagenes/PHP/6.JPG)

Ahora comprobaremos que estos cambios son eficaces. Para esto, crearemos un archivo de tipo .php, el mas útil de ellos es info.php:

<code>sudo nano /var/www/html/info.php</code>


Esto creará una página en blanco donde escribiremos el siguiente código:

![PHP Instalación](Imagenes/PHP/7.JPG)

Cuando acabes guarda el archivo con Ctrl+o y sal de el con Ctrl+x.

Ahora podremos ver ese archivo en nuestro navegador escribiendo lo siguiente:


![PHP Instalación](Imagenes/PHP/8.JPG)


<code>http://ip_de_tu_servidor/info.php o http://dns_de_tu_servidor/info.php</code>


![PHP Instalación](Imagenes/PHP/9.JPG)

<a id="item4"></a>

# Instalar FTP

Primero vamos a crear 3 usuarios cliente, servidor y administrador para eso meteromos el siguiente comando.

<code> sudo adduser cliente</code>

![FTP Instalación](Imagenes/FTP/1.JPG)

<code> sudo adduser servidor</code>

![FTP Instalación](Imagenes/FTP/2.JPG)

<code> sudo adduser administrador</code>

![FTP Instalación](Imagenes/FTP/3.JPG)

Ahora instalaremos el servidor FTP, para ello meteremos el siguiente comando:

<code>sudo apt-get install vsftpd</code>

![FTP Instalación](Imagenes/FTP/4.JPG)

Una vez que haya instalado el paquete, puede ejecutar el servicio y habilitarlo para que se ejecute al iniciar el sistema.

<code>sudo systemctl start vsftpd</code>

<code>sudo systemctl enable vsftpd</code>

![FTP Instalación](Imagenes/FTP/5.JPG)

Ahora habilitaremos el puerto 21 para el servicio FTP:

![FTP Instalación](Imagenes/FTP/6.JPG)

Por lo ultimo reseteamos el servicio FTP con el sigiente comando

<code>sudo service vsftpd restart</code>

![FTP Instalación](Imagenes/FTP/7.JPG)

# Ejercicio 3. IP elástica.

# Direcciones IP elásticas

Las direcciones IP elásticas son direcciones IPv4 estáticas diseñadas para la informática en la nube dinámica.

# ¿Para que sirve?

Con una dirección IP elástica, puede enmascarar los errores de una instancia o software volviendo a mapear rápidamente la dirección a otra instancia de su cuenta. Se asigna una dirección IP elástica a su cuenta de AWS, que es suya hasta que la libere.

# Documentación

Para asignar una dirección IP elástica desde un grupo de direcciones IPv4 públicas de Amazon utilizando la consola:

- Abra la consola de Amazon EC2 en https:// console.aws.amazon.com/ec2/.

- En el panel de navegación, elija Elastic IPs (Direcciones IP elásticas).

- Elija Allocate new address (Asignar nueva dirección).


![IP_ELASTICA](Imagenes/IP_ELASTICA/1.JPG)

En IPv4 address pool (Grupo de direcciones IPv4), elija Amazon pool (Grupo de Amazon).

![IP_ELASTICA](Imagenes/IP_ELASTICA/2.JPG)

Elija Allocate (Asignar) y cierre la pantalla de confirmación.

![IP_ELASTICA](Imagenes/IP_ELASTICA/3.JPG)

Aquí sale un resumen de nuestra IP alocada:

![IP_ELASTICA](Imagenes/IP_ELASTICA/4.JPG)

[Subir](#top)


# Ejercicio 4. DNS. 

# ¿QUÉ ES?

- Sistema en general en el que está basado el funcionamiento de los dominios en Internet: una red mundial de servidores que traducen nombres que tú como humano entiendes, a direcciones IP que las máquinas entienden.

- Es una tecnología basada en una base de datos que sirve para resolver nombres en las redes, es decir, para conocer la dirección IP de la máquina donde está alojado el dominio al que queremos acceder.


# ¿Para que sirve?

Los DNS sirven para indicarle al usuario que teclea un dominio a que servidor debe ir a recoger la página web que desea consultar.

# Tipos de DNS

Los tipos de registros más utilizados son:

- A = Dirección (address). Este registro se usa para traducir nombres de servidores de alojamiento a direcciones IPv4.
- AAAA = Dirección (address). Este registro se usa en IPv6 para traducir nombres de hosts a direcciones IPv6.
CNAME = Nombre canónico (canonical Name). Se usa para crear nombres de servidores de alojamiento adicionales, o alias, para los servidores de alojamiento de un dominio. Es usado cuando se están corriendo múltiples servicios (como FTP y servidor web) en un servidor con una sola dirección IP. Cada servicio tiene su propia entrada de DNS (como ftp.ejemplo.com. y www.ejemplo.com.). Esto también es usado cuando corres múltiples servidores HTTP, con diferentes nombres, sobre el mismo host. Se escribe primero el alias y luego el nombre real. Ej. Ejemplo1 IN CNAME ejemplo2
- NS = Servidor de nombres (name server). Define la asociación que existe entre un nombre de dominio y los servidores de nombres que almacenan la información de dicho dominio. Cada dominio se puede asociar a una cantidad cualquiera de servidores de nombres.
- MX = Intercambio de correo (mail exchange). Asocia un nombre de dominio a una lista de servidores de intercambio de correo para ese dominio. Tiene un balanceo de carga y prioridad para el uso de uno o más servicios de correo.
PTR = Indicador (pointer). También conocido como 'registro inverso', funciona a la inversa del registro A, traduciendo IPs en nombres de dominio. Se usa en el archivo de configuración de la zona DNS inversa.
- SOA = Autoridad de la zona (start of authority). Proporciona información sobre el servidor DNS primario de la zona.
- SRV = Service record (SRV record).
- ANY = Toda la información de todos los tipos que exista. (No es un tipo de registro, sino un tipo de consulta)


# Gestión de DNS

Para empezar, en la página principal de Guebs iremos a Registro DNS.

![DNS](Imagenes/DNS/1.JPG)

TIPOS DE REGISTROS
Tipo A: Con este tipo asociamos un nombre a una dirección IP IPv4 para buscar esa direccón mediante un nombre en vez de una IP.

Tipo AAAA: Este tipo es exactamente igual que el anterior pero para direcciones IPv6.

Tipo CNAME: Se utiliza para asociar un nombre a una url para correr diferentes servicios (FTP y servidor web) con una sola dirección.

Tipo TXT: Con este tipo asociamos un nombre a texto plano que contiene información externa a tu página.

Tipo SRV: Es utilizado para asociar un nombre a un servicio.


# Ejercicio 5. DNS. 

# Documentación: 

### ¿Cuántos servidores DNS existen?
  
Una de las creencias muy extendidas en el mundo de las redes es que existen en el mundo sólo 13 root servers, esto es, 13 servidores encargados de almacenar información sobre los dominios de primer nivel (o Top Level Domain TLD) en el sistema de nombre de dominio (DNS) utilizado en Internet.

### ¿Cuántas redirecciones DNS son posibles?

Root Server. Como en cualquier jerarquía, cuando hablamos de servidor DNS tiene que existir un nivel superior, un punto en el que una consulta no contestada no pueda subir más y tenga que ser resuelta de un modo u otro. En este nivel superior la consulta será resuelta por un Root Server.


TLD. Significa “Top Level Domain”. Siguiendo con el ejemplo, el TLD de miweb.es es “.es”. Se trata del dominio “padre”, y es responsabilidad de alguna entidad nacional o internacional que se encarga de gestionar los servidores de nombres que tienen información sobre esta extensión. Por ejemplo, los dominios .es son responsabilidad de nic.es, los .com son responsabilidad de Verisign, etc …


### ¿Qué son los servidores DNS Raíz?

El directorio raíz de un dominio es la carpeta a la que apunta el dominio, que contiene los ficheros y carpetas de la web que carga dicho dominio. En cpanel, el dominio principal apunta a la carpeta public_html de tu cuenta. Si quieres puedes apuntar el dominio principal a otra carpeta.


### ¿Para qué montar un servidor si simplemente escribiendo en un fichero la relación IP/Nombre el sistema ya funcionaría?

Cada equipo conectado directamente a Internet tiene al menos una dirección IP específica. Sin embargo, los usuarios no desean trabajar con direcciones numéricas, como por
ejemplo 194.153.205.26, sino con un nombre de dominio o más específicamente, con direcciones (llamadas direcciones FQDN) como por ejemplo es.kioskea.net. 

### Según lo expuesto, y si en tu configuración de red del sistema operativo solamente posees un servidor DNS, entonces: ¿cuál sería el proceso para encontrar la IP de la dirección web: http://www.debian.org/distrib/netinst?
  
1. Nuestro equipo verá que no conoce la IP a la que debe conectarse, así que preguntará a un servidor DNS que tenga configurado.

2. A este servidor DNS le llegará una petición.  Pero tampoco conoce la respuesta, así que pregunta al siguiente en la jerarquía, es decir, a uno de sus propios servidores DNS.

3. Esto puede ocurrir varias veces hasta que al final la pregunta llega a un Root Server.
   
4. El Root Server contestará “Yo no sé a qué IP resuelve miweb.es, pero puedo decirte qué servidor DNS lo sabe.” Entonces dirigirá la consulta a un servidor DNS del dominio padre, o TLD.

5. El servidor del dominio padre de nuevo contestará la consulta, indicando cuáles son los servidores DNS autoritativos para el dominio; en este caso serán ns1.miweb.es y ns2.miweb.es.

6. La petición llega a estos dos servidores DNS, es contestada, y ahora ya todos los equipos por los que ha pasado la consulta van a guardar esta información durante un tiempo (Cache DNS).

7. Por último, tu ordenador ya tiene su respuesta y ya sabe a qué IP resuelve el dominio. Hace una conexión a ella, pide la página web y te la enseña.
   
### ¿Es posible si dispones de una conexión a Internet con IP dinámica ofrecer servicios en Internet? Es decir, si quieres ofrecer los servicios SND, no dispones de IP estática, esto es, cada vez que te conectas a Internet tu IP, aunque a veces sea la misma, no siempre es la misma. 
  
Si, pero no es recomendable ya que estaríamos cada dos por tres cambiando de dirección IP, y nos resultaría muy incómodo.

### ¿Qué es ICANN?

ICANN es una entidad internacional sin ánimo de lucro responsable de alojar direcciones IP, gestionar dominios genéricos y territoriales, y asignar identificadores de protocolos.

