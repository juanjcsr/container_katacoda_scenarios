En este paso vamos a construir una imagen de contenedor la cual va a encapsular nuestra aplicación

## Escribiendo un Dockerfile

El archivo Dockerfile describe los pasos que Docker va a utilizar para construir el contenedor:

<pre class="file" data-filename="Dockerfile" data-target="replace">
# Empecemos con una imagen sin nada
FROM scratch

# Copiemos el archivo binario al directorio rail
COPY hello /

# Decirle a Docker qué ejecutable correr cuando el contenedor inicia
ENTRYPOINT ["/hello"]
</pre>

El siguiente comando construye la imagen del contenedor, siguiendo los comandos especificados en el Dockerfile

`docker build -t hello  .`{{execute}}

* Con la opción `-t` estamos especificando un *tag*  que nos permite identificar la imagen. Más abajo encontrarás notas sobre nombres e imágenes.
* El `.` significa que estamos construyendo una imagen en el *contexto* del directorio actual

Revisa que la imagen del contenedor exista:

`docker image ls`{{execute}}

Deberías ver algunas imágenes en la lista, incluyendo una llamada *hello*

Tu imagen tiene la tag *latest*. Esta es una tag predeterminada si no especificamos una. 

## Siguiente paso

Ya creamos una imagen de contenedor! En el siguiente paso ejecutaremos un contenedor basado en esta imagen. Antes de hacerlo, puedes continuar leyendo sobre nombres y tags acá abajo.

### Notas y algunas fuentes extra:

Existen **registries** de los cuales podemos hacer *pull* y *push* de imágenes (como DockerHub). Podemos referirnos a nuestra imagen de las siguientes formas:

* \[*registry*/\]*repository*/*name*:*tag*
* \[*registry*/\]*repository*/*name*@sha256:*image digest*

El *registry* es el hostname del container registra. Si no lo ponemos, se asume que es Docker Hub. 

El *repository* es usualmente nuestro nombre de usuario o el nombre de nuestra organización o proyecto. 

El *name* es el nombre de la imagen. En nuestro caso, utilizamos `hello`

El *image digest* es un hash del contenido de la imagen y es un identificador inmutable para esa versión exacta de la imagen. Si reconstruimos la imagen, va a tener un hash distinto

El *image digest* y el *tag* son dos formas de identificar versiones de la misma imagen. El digestivo es único a una imagen en particular, pero podemos usar el tag que queramos. 

En la práctica, el tag se utiliza para versionar las imágenes utilizando versionado semántico.

Puedes leer más sobre los IDs y los tags en los siguientes links:
* [Explaining Docker Image IDs](https://windsock.io/explaining-docker-image-ids/)
* [Docker Tag vs Hash: A Lesson in Deterministic Ops](https://medium.com/@tariq.m.islam/container-deployments-a-lesson-in-deterministic-ops-a4a467b14a03)
* [Using Docker tags to mess with people's minds](https://medium.com/microscaling-systems/using-docker-tags-to-mess-with-peoples-minds-367bb2c93bd0)