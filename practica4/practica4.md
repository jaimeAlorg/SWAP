# Práctica 4

Jaime Álvarez Orgaz

## Tareas

1. Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.
2. Configurar las reglas del cortafuegos para proteger la granja web.

## Instalar Certifacado SSL y Configurar Acceso HTTPS a los Servidores

Primero vamos a activar el modulo SSL mediante **sudo a2enmod ssl & sudo service apache2 restart** y crear el directorio ssl para los certificados **sudo mkdir /etc/apache2/ssl**

![Imagen ssl1](Img/ssl1.png)

Una vez hecho esto, vamos a generar el certificado y configurarlo mediante el comando **sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 –keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt**

![Imagen ssl2](Img/ssl2.png)

Cuando generamos el certificado, editamos **sudo nano /etc/apache2/sites-available/default-ssl.conf** y le añadimos las siguientes 3 lineas:

![Imagen ssl3](Img/ssl3.png)

Una vez configurado **default-ssl.conf** escribimos en la terminal **sudo a2ensite default.ssl** y **sudo service apache2 reload**. Con esto ya tendriamos activado el sitio default-ssl.

![Imagen ssl4](Img/ssl4.png)

En cuanto reiniciamos apache, ya podremos acceder al servidor web mediante el protocolo HTTPS. En la foto de debajo he accedido a ejemplo.html que contiene por escrito **Maquina 1**

![Imagen ssl5](Img/ssl5.png)

Ya no hay que generar mas certificados. Simplemente hay que pasar el que tenemos en M1 a M2 y M3. Esto lo hacemos mediante **sudo scp apache.crt usuario@ipm2:/home/usuario/apache.crt** y **sudo scp apache.key usuario@ipm2:/home/usuario/apache.key**. Una vez lo tengamos en M2, seguimos las siguientes instrucciones: 

![Imagen ssl6](Img/ssl8.png)

A diferencia de M2, en M3, solo hay que pasarlo desde M1 con **scp**. En mi caso lo he guardado en **/home/jaimealorg/ssl**. Una vez lo tengamos guardado en M3, tenemos que configurar **/etc/nginx/conf.d/default.conf** añadiendole las tres líneas que hay debajo de listen 80. Para esta práctica he tenido que cambiar las direcciones ip de todas las máquinas por lo que en mi caso también he tenido que modificar upstream servidoresSWAP.

![Imagen ssl7](Img/ssl6.png)

Podemos ver que todo funciona correctamente al hacer varias peticiones al balanceador mediante curl -k **https://192.168.56.11/ejemplo.html**

![Imagen ssl8](Img/ssl7.png)

## Configuración del Cortafuegos

El cortafuegos es un componente esencial que protege a la granja web de accesos indebidos. El cortafuegos se configura mediante **iptables**. Para la configuración he realizado un script pero previamente he aprendido a usar iptables mediante unas pruebas en la terminal. Para que el script funcione cada vez que arranque el equipo, hay que configurar un demonio. El script que he realizado es una configuración básica para un servidor web. Es el siguiente:

![Imagen cf](Img/cf.png)

Con **iptables -L -n -v** podemos ver la correcta configuración y funcionamiento del script para el cortafuegos. 

![Imagen cf](Img/cf2.png)