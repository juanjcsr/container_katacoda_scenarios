Verifica que tu contenedor sigue corriendo:

`docker ps`{{execute}}

En la columna de *PORTS* deberías ver `0.0.0.0:18080->8080/tcp`

* `0.0.0.0` es equivalente a  `localhost` y es la dirección de tu computadora local
* `18080` es el puerto del host
* `8080` es el puerto dentro del contenedor que mapea al host.

## Ejecuta un segundo contenedor

Únicamente una aplicación se puede atar a un puerto al mismo tiempo. El servidor que hicimos en Go tiene hardcodeado el puerto 8080. Podemos ver que no se puede ejecutar un proceso en el mismo puerto si levantamos dos servidores locales:

`./hello &`{{execute}}

`./hello`{{execute}}

Lo cual nos mostrará que el puerto ya se encuentra en uso.

Para matar la primera instancia del servidor podemos matarla de la siguiente forma:

`kill %1`{{execute}}

Cuando ejecutamos un contenedor, podemos tener muchas instancias ejecutandose de forma simultánea utilizando distintos puertos del host. Por ejemplo, podemos ejecutar una nueva instancia de nuestro contenedor pero ahora en el puerto 108081:

`docker run -d -p 18081:8080 hello`{{execute}}

`docker ps`{{execute}}

Deberíamos ver dos instancias del contenedor en ejecución. Podemos hacer peticiones a cualquiera de ellos:

`curl localhost:18080`{{execute}}

`curl localhost:18081`{{execute}}

Dentro de cada contenedor, las dos instancias del servidor se están atando al puerto 8080, pero, ya que cada contenedor tiene su propio **namespace** de red, estos puertos no son los mismos que los del host.

Podemos ejecutar cualquier cantidad de instancias del mismo contenedor en un host, asignándoles un puerto distinto del host.

## Que Docker asigne un puerto de forma dinámica

Si solo le decimos a Docker que exponga un puerto interno, Docker va a elegir un puerto disponible del host:

`docker run -d -p 8080 hello`{{execute}}

`docker ps`{{execute}}

La salida del último comando nos va a decir qué puerto Docker eligió. Prueba el comando mediante cual:

`curl localhost:`{{copy}}

## Siguiente paso:

En el siguiente paso vamos a ver cómo especificar el puerto dentro del Dockerfile para que esta información se encuentre dentro de la imagen del contenedor.