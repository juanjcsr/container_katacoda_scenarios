Ahora toca ejecutar nuestro servidor dentro un **contenedor**

El siguiente comando ejecutará un contenedor, basado en la imagen que apenas construimos:

`docker run --rm -d -p 18080:8080 hello`{{execute}}

* La opción -d ejecuta el contenedor en segundo plano (para no perder el acceso a la terminal
* La opción -p 108080:8080 le dice a Docker que relacione el puerto 8080 del contenedor al puerto 108080 del host

Al ejecutar el comando, vamos a ver como resultado varios dígitos en la terminal. Este es el ID que identifica al contenedor ejecutándose.

## Revisando los contenedores en ejecución

El comando:

`docker ps`{{execute}}

Permite listar los contenedores que actualmente se encuentran ejecutandose en nuestro sistema.

## Revisa que puedes acceder al contenedor

`curl localhost:18080`{{execute}}

o:

`curl https://[[HOST_SUBDOMAIN]]-18080-[[KATACODA_HOST]].environments.katacoda.com/`{{execute}}

## Siguiente paso

En el siguiente paso veremos otras opciones para especificar el host y el puerto para nuestro contenedor