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
		w.Write([]byte("hello world\n"))
	})

	err := http.ListenAndServe(":8080", nil)
	if err != nil {
	  fmt.Printf("serving: %v\n", err)
	  os.Exit(1)
	}
}
</pre>