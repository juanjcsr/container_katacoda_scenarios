Los comandos ENTRYPOINT y CMD en los archivos Dockerfile pueden ser fuente de confusión. En este escenario exploraremos cómo funcionan

## ENTRYPOINT especifica el archivo ejecutable por defecto

Aquí tienes un Dockerfile basado en la imagen de Alpine el cual especifica `ls` como entrypoint:

<pre class="file" data-filename="Dockerfile" data-target="replace">

FROM alpine

ENTRYPOINT ["ls"]
</pre>


Construye la imagen:

`docker build -t ls:entrypoint .`{{execute}}

Cuando ejecutes la imagen, `ls` se va a ejecutar por defecto. Puedes especificar parámetros adicionales al final de tu comando `docker run` y estos serán agregados al entrypoint:

`docker run -t ls:entrypoint`{{execute}}

* En `docker run`, el parámetro `-t` asigna una terminal al contenedor, lo que nos permite ver la salida del comando

`docker run -t ls:entrypoint /bin`{{execute}}

`docker run -t ls:entrypoint -ltr`{{execute}}

## Sobreescribiendo el entrypoint

Si queremos cambiar el ejecutable del entrypoint o ejecutar otro archivo del contenedor, necesitamos sobreescribirlo de forma explicita:

`docker run -t  --entrypoint echo ls:entrypoint hello`{{execute}}

## Siguiente paso:

¿Qué pasa cuando usamos el comando CMD?