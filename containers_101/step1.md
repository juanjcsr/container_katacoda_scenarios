Empecemos escribiendo un servidor en Go

## Hola Mundo

Escribe un servidor en Go que responda a peticiones en el puerto 8080. Puedes utilizar el servidor que has desarrollado a lo largo de las clase.  Aquí abajo hay un servidor de ejemplo

<pre class="file" data-filename="hello.go" data-target="replace">
package main

import (
  "net/http"
  "fmt"
  "os"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("hola mundo! :D\n”))
	})

	err := http.ListenAndServe(":8080", nil)
	if err != nil {
	  fmt.Printf("serving: %v\n", err)
	  os.Exit(1)
	}
}
</pre>

*De preferencia usa tu servidor desarrollado en clase, sin embargo, ten la libertad de modificar el código del servidor de acá arriba. Solamente recuerda el puerto en donde el servidor está respondiendo a las peticiones (en este caso, es el 8080). Esto es importante porque vamos a usar ese puerto a lo largo del escenario*

## Compila tu app

Compila tu aplicación:

`CGO_ENABLED=0 go build -o hello hello.go`{{execute}}

En este ejemplo estamos apagando el flag de “CGO_enabled” para construir un binario ejecutable sin dependencias al sistema, el cual lo usaremos dentro de la imagen del contenedor.

## Ejecuta tu aplicación

Ejecuta tu aplicación y abre una segunda terminal para poder ejecutar comandos:

`./hello &`{{execute}}

##Revisa que funciona

En la segunda terminal, prueba tu aplicación mediante `curl`:

`curl localhost:8080`{{execute}}

Y deberías ver el mensaje o la funcionalidad de tu servidor.

###Hostname en el ambiente de Katacoda

Vía `curl` acabamos de hacer una petición en el puerto especificado. Dentro de Katacoda podemos llegar a estos puertos mediante el host que se nos configuró automáticamente. En este caso, podemos acceder a nuestra aplicación mediante nuestro navegador visitando [https://\[%5BHOST\_SUBDOMAIN%5D%5D-8080-%5B%5BKATACODA\_HOST%5D%5D.environments.katacoda.com/] (recuerda modificar tu puerto!)

Igualmente puedes hacer una petición mediante  `curl`:

`curl https://[[HOST_SUBDOMAIN]]-8080-[[KATACODA_HOST]].environments.katacoda.com/`{{execute}}

De igual forma, desde la terminal de tu laptop puedes repetir esta misma petición, dado que esa dirección está expuesta a internet.

## Mata la aplicación

Ejecuta Control + C y termina la aplicación. Ejecuta:

`ps`{{execute}}

Y verifica que ya no se encuentre ejecutandose 

## Siguiente paso

Perfecto! Ya tienes un binario en Go compilado y listo para ejecutarse. En el siguiente paso vamos a construir un contenedor que incluye este binario