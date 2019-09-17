Vamos a modificar el Dockerfile para especificar  el puerto que nuestro servidor en contenedor expone:

<pre class="file" data-filename="Dockerfile" data-target="append">
# The app uses port 8080
EXPOSE 8080
</pre>

# Construir y ejecutar la imagen del contenedor

`docker build -t hello .`{{execute}}

`docker run -d -P hello`{{execute}}

* La opción -P le dice a Docker que exponga el puerto que se encuentra especificado en la imagen del contenedor.

Ya que no especificamos un puerto del host, Docker asigna uno de forma automática. Lo podemos encontrar mediante el siguiente comando:

`docker ps`{{execute}}

Ya que no hemos eliminado ninguna imagen, vamos a ver varias entradas. Las nuevas se muestran primero