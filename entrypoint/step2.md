Aquí hay otro Dockerfile basado en Alpine el cual especifica `ls` como entrypoint y `/bin` como el argumento por defecto que se le pasa al ejecutable `ls`

<pre class="file" data-filename="Dockerfile" data-target="replace">
FROM alpine

ENTRYPOINT ["ls"]

CMD ["/bin"]
</pre>

Construye la imagen:

`docker build -t ls:entry-cmd .`{{execute}}

