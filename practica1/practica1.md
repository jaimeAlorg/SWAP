# Práctica 1

Jaime Álvarez Orgaz

## Configuración

Para la realización de esta práctica vamos a necesitar dos máquinas con Ubuntu Server. En ambas máquinas vamos a necesitar tener instalado LAMP que nos proporcionará apache, php y mysql. En la proxima imagen se puede ver que mis dos máquinas estan funcionando correctamente.

![Imagen Máquinas](https://github.com/jaimeAlorg/SWAP/blob/master/practica1/Img/maquinas.png)

Para acceder a una maquina mediante SSH previamente hemos de haber configurado en cada una de ellas un adaptador de red en modo nat y otro en solo-anfitrión, para así crear una red local entra ambas máquinas y el anfitrión.

A continuación hemos de configurar la dirección IP y puerta de enlace de cada máquina. Con nuevas versiones de Ubuntu se configura con netplan pero yo he preferido hacerlo mediante ifupdown. Aquí se pueden ver las ip de ambas máquinas:

![Imagen Máquinas](https://github.com/jaimeAlorg/SWAP/blob/master/practica1/Img/ip.png)

Podemos observar que la primera máquina tiene la ip **192.168.1.100** mientras que la segunda es **192.168.1.101**

## Acceder por SSH de una Máquina a Otra

Una vez configuradas las máquinas, para conectarnos de m1 a m2 tenemos que escribir en la terminal **ssh 192.168.1.101** y poner la contraseña. Para ver que ha funcionado correctamente, he dejado un archivo **hola.txt** en la máquina 2.

![Imagen Máquinas](https://github.com/jaimeAlorg/SWAP/blob/master/practica1/Img/ssh.png)

Ahora voy a hacer lo mismo pero conectandome desde m2 a m1. El archivo que voy a dejar en m1 se va a llamar **hola2.txt**

![Imagen Máquinas](https://github.com/jaimeAlorg/SWAP/blob/master/practica1/Img/ssh2.png)

## Acceder Mediante Curl Desde una Máquina a Otra

En m1 he creado un archivo **ejemplo.html**. Simplemente para acceder a el desde m2 he de escribir en la terminal **curl http://192.168.1.100/ejemplo.html**

![Imagen Máquinas](https://github.com/jaimeAlorg/SWAP/blob/master/practica1/Img/curl.png)
