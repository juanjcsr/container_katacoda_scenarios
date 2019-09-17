En este paso vamos a decirle a nuestra aplicación que lea el mensaje desde una variable de ambiente

Modifica el programa en Go para que lea una variable de ambiente y la utilice en la respuesta:

<pre class="file" data-filename="hello.go" data-target="replace">
package main

import (
  "fmt"
  "net/http"
  "os"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		response := os.Getenv("GO_APP_RESPONSE")
		fmt.Printf("response: %s\n", response)
		w.Write([]byte(response))
	})

	err := http.ListenAndServe(":8080", nil)
	if err != nil {
	  fmt.Printf("serving: %v\n", err)
	  os.Exit(1)
	}
}
</pre>

Construye esta nueva versión de la aplicación:

`CGO_ENABLED=0 go build -o hello hello.go`{{execute}}

Y construye una imagen con esta nueva versión:

`docker build -t hello  .`{{execute}}

## Pasa la variable al momento de ejecutar:

Puedes pasar una variable de ambiente como parte del comando Docker para ejecutar el contenedor:

`docker run -d --rm -e GO_APP_RESPONSE="Respuesta desde una variable de ambiente" -p 18082:8080 hello`{{execute}}

Este contenedor ahora lo puedes acceder en el puerto 108082

`curl localhost:18082`{{execute}}

## Construye la variable de ambiente dentro de la imagen

Si la variable de ambiente no va a cambiar, podemos agregarla a la imagen en tiempo de construcción agregando un comando `ENV` dentro del Dockerfile

<pre class="file" data-filename="Dockerfile" data-target="append">
# Define an environment variable
ENV GO_APP_RESPONSE="Variable desde el contenedor"
</pre>

Recuerda reconstruir la imagen:

`docker build -t hello  .`{{execute}}

y ahora ya no es necesario especificar una variable de ambiente:

`docker run -d --rm -p 18083:8080 hello`{{execute}}