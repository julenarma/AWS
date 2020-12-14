<a id="top"></a>
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

Antes que nada haremos un update:  sudo apt-get update


![Apache Instalación](Imagenes/Apache/1.JPG)


Y ahora instalaremos apache. sudo apt-get install apache2


![Apache Instalación](Imagenes/Apache/2.JPG)

Para comprobar que funciona correctamente primero accederemos al **wizard de AWS** para comprobar que HTTP y HTTPS están habilitados:


![Apache Instalación](Imagenes/Apache/3.JPG)


Una vez aquí clickaremos en Edit:


![Apache Instalación](Imagenes/Apache/4.JPG)


Para acabar, con Add rule añadiremos una regla nueva donde seleccionaremos HTTP en la sección de tipo. Repite este paso para añadir HTTPS:
![Apache Instalación](Imagenes/Apache/5.JPG)

![Apache Instalación](Imagenes/Apache/6.JPG)

Ahora ya podemos comprobar si la instalación del Apache2 se ha hecho de manera correcta, para ello escribe lo siguiente en tu navegador:

http://ip_de_tu_servidor o http://dns_de_tu_servidor


![Apache Instalación](Imagenes/Apache/7.JPG)

Puedes encontrar tu ip o dns en esta sección una vez que la máquina está encendida:

![Apache Instalación](Imagenes/Apache/8.JPG)


[Subir](#top)

<a id="item2"></a>

# Instalar MySQL

Instalaremos MySQL, para ello usaremos este comando: 

sudo apt-get install mysql-server mysql-client

![MYSQL Instalación](Imagenes/MYSQL/1.JPG)

Con este comando instalaremos tanto el servidor como el cliente de MySQL.

Al finalizar la instalación ejecutaremos el siguiente comando:


sudo mysql_secure_installation

![MYSQL Instalación](Imagenes/MYSQL/2.JPG)


Con este comando borraremos algunos parametros peligrosos y aseguraremos el acceso ala base de datos.

Después te pedirá que completes unos pasos. Hazlo de la siguiente manera:


![MYSQL Instalación](Imagenes/MYSQL/3.JPG)

![MYSQL Instalación](Imagenes/MYSQL/4.JPG)



Si quisieras comprobar tu versión de MySQL puedes hacerlo con esté comando:

mysql --version


![MYSQL Instalación](Imagenes/MYSQL/5.JPG)


[Subir](#top)

<a id="item3"></a>

# Instalar PHP

Ahora toca instalar PHP, para ello comenzaremos con el comando de instalación de nuevo:

sudo apt install php libapache2-mod-php php-mysql

![PHP Instalación](Imagenes/PHP/1.JPG)

Si tus archivos van a ser de tipo .php es recomendable que modifiques el archivo dir.conf para dar prioridad a dicho tipo de archivos.

Para conseguir esto ejecutaremos el siguiente comando:

sudo nano /etc/apache2/mods-enabled/dir.conf


![PHP Instalación](Imagenes/PHP/2.JPG)

Con esto te saldra algo como esto:

![PHP Instalación](Imagenes/PHP/3.JPG)

Cambiaremos de sitio el archivo index.php colocándolo en primer lugar y lo guardaremos con Ctrl+o y saldremos con Ctrl+x:

![PHP Instalación](Imagenes/PHP/4.JPG)

Seguidamente reiniciaremos el servicio de Apache2 para que los cambios se efectuen:

sudo systemctl restart apache2


![PHP Instalación](Imagenes/PHP/5.JPG)

Una vez reiniciado comprobaremos el estado del servicio con este otro comando:


Ahora comprobaremos que estos cambios son eficaces. Para esto, crearemos un archivo de tipo .php, el mas útil de ellos es info.php:

sudo nano /var/www/html/info.php

![PHP Instalación](Imagenes/PHP/6.JPG)

Esto creará una página en blanco donde escribiremos el siguiente código:

![PHP Instalación](Imagenes/PHP/7.JPG)

Cuando acabes guarda el archivo con Ctrl+o y sal de el con Ctrl+x.

Ahora podremos ver ese archivo en nuestro navegador escribiendo lo siguiente:

http://ip_de_tu_servidor/info.php o http://dns_de_tu_servidor/info.php


![PHP Instalación](Imagenes/PHP/8.JPG)


[Subir](#top)


<a id="item4"></a>

# Instalar FTP
Vamos a instalar el servidor FTP
[Subir](#top)