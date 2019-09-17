En los pasos anteriores has estado ejecutando contenedores dentro del ambiente de Katacoda en una máquina virtual en la nube.  Si tienes Docker instalado en tu laptop, puedes intentar ejecutar ima imagen de contenedor en tu propia máquina.

## ¿Cuál es tu usuario de DockerHub?

El siguiente comando te va a pedir tu usuario de DockerHub y lo va a guardar en una variable de ambiente `$yourname` para usarlo en los subsecuentes comandos:

`read -p 'Enter your Docker Hub username: ' yourname`{{execute}}

Puedes obtener una cuenta de DockerHub en [hub.docker.com](https://hub.docker.com).

## Asigna un tag a tu imagen

En el siguiente comando vamos a pedirle a Docker que haga *push* de nuestra imagen a nuestro repositorio en DockerHub. Lo primero que necesitamos es asignarle un tag a nuestra imagen e incluir nuestro repositorio:

`docker tag hello $yourname/hello`{{execute}}

##Loggeate a DockerHub

Ejecuta:

`docker login -u $yourname`{{execute}}

##Da push a tu imagen a DockerHub

`docker push $yourname/hello`{{execute}}

##Da pull de la imagen a tu laptop

Si tienes Docker instalado en tu laptop, puedes ejecutar la imagen que construiste en Katacoda. Primero necesitas hacer pull de tu imagen desde DockerHub

`docker pull *tu_nombre*/hello`{{copy}}

Y con esto ya la puedes ejecutar de forma local:

`docker run -d -P *tu_nombre*/hello`{{copy}}

