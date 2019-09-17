¿Cómo podemos obtener los logs?

Primero necesitamos identificar nuestro contenedor:

docker ps{{execute}}

Éste es un ejemplo de la salida del comando que vas a ver:

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS  NAMES
63e325cf0886        hello               "/hello"            5 seconds ago       Up 3 seconds        0.0.0.0:18080->8080/tcp  gifted_ardinghelli
```

Podemos identificar un contenedor mediante:

* **container ID** - En este ejemplo es 63e25... 
* **name** - En el ejemplo es gifted_ardinghelli

## Obten los logs

`docker logs <ID DEL CONTENEDOR>`{{execute}}