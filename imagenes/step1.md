Empieza escribiendo una aplicación simple en Go.  Este ejemplo es muy similar a la aplicación del escenario anterior, sin embargo, este servidor va a leer la respuesta de un archivo, en lugar de estar hardcodeada.

## Hola mundo!

<pre class="file" data-filename="hello.go" data-target="replace">
package main

import (
  "fmt"
  "io/ioutil"
  "net/http"
  "os"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		response, err := ioutil.ReadFile("./text/response")
		if err != nil {
			fmt.Printf("reading file: %v\n", err)
			os.Exit(1)
		}

		fmt.Printf("response: %s\n", response)
		w.Write(response)
	})

	err := http.ListenAndServe(":8080", nil)
	if err != nil {
	  fmt.Printf("serving: %v\n", err)
	  os.Exit(1)
	}
}
</pre>

Compila la aplicación de forma similar a la anterior:

`CGO_ENABLED=0 go build -o hello hello.go`{{execute}}

Necesitas especificar el archivo con la respuesta de la que este servidor va a leer. Primero abre el archivo en tu editor:

`text/response`{{open}}

Y agrega un mensaje en este archivo:

<pre class="file" data-filename="text/response" data-target="replace">
Esta es una respuesta
</pre>

## Ejecuta tu aplicación

Ejecuta tu aplicación en segundo plano:

`./hello &`{{execute}}

y revisa que puedes hacer peticiones a tu servidor:

`curl localhost:8080`{{execute}}

Deberías ver:
* El mensaje de texto que especificaste en tu archivo.

## Deten la aplicación

`kill %1`{{execute}}

## Siguiente paso:

En el siguiente paso vamos a incluir a nuestra imagen el archivo binario y el archivo de texto