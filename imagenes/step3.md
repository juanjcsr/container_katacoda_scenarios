Ejecuta tu aplicación:

`docker run --rm -d -p 18080:8080 hello`{{execute}}

Recuerda que puedes accederlo via curl local o exponiendo el puerto y el host a internet:

`curl localhost:18080`{{execute}}

o:

`curl https://[[HOST_SUBDOMAIN]]-18080-[[KATACODA_HOST]].environments.katacoda.com/`{{execute}}

Copiamos el archivo `text/response` de forma que pertenece a la imagen en la ubicación `/text/response`. Esta imagen está auto-contenida ya que el archivo de respuesta existe en la ruta `/text/response` del contenedor. Recuerda que este archivo *NO* es el mismo que el archivo local. El sistema de archivos del contenedor es distinto a lo que el host ve.

Podemos verificar que esto es cierto al ejecutar una petición al contenedor y cambiar el contenido del archivo `/text/response`.

`text/response`{{open}}

`curl localhost:18080`{{execute}}

## Siguiente paso:

Vamos a ver cómo modificar este archivo, montando una carpeta del host al contenedor.