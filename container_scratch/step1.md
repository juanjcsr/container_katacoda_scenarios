<pre class="file" data-filename="contenedor.go" data-target="replace">

package main

import (
	"fmt"
	"log"
	"os"
	"os/exec"
	"syscall"
)

// go run main.go run <cmd> <args>
func main() {
	// Esperamos "run" como primer argumento
	switch os.Args[1] {
	case "run":
		fmt.Printf("host ejecutando hijo, pid: %d \n",
			os.Getpid())
		parent()
	case "child":
		// El resto de los argumentos (del 2 en adelante) es el comando que queremos ejecutar
		fmt.Printf("hijo ejecutando %v, pid: %d\n",
			os.Args[2:],
			os.Getpid())
		child()
	default:
		panic("mal argumento")
	}
}

func parent() {
	// Preparamos al padre para ejecutar el hijo
	args := os.Args
	args[1] = "child"
	cmd := exec.Command("/proc/self/exe", args[1:]...)

	cmd.Stdin = os.Stdin
	cmd.Stdout = os.Stdout
	cmd.Stderr = os.Stderr

	cmd.SysProcAttr = &syscall.SysProcAttr{
		Cloneflags: syscall.CLONE_NEWUTS |
			syscall.CLONE_NEWPID |
			syscall.CLONE_NEWNS,
		Unshareflags: syscall.CLONE_NEWNS,
	}

	// Aquí ejecutamos el comando:
	must(cmd.Run())
	fmt.Println("== Fin host ==")
}

func child() {

	// Preparamos al hijo para ejecutar nuestro comando
	cmd := exec.Command(os.Args[2], os.Args[3:]...)
	cmd.Stdin = os.Stdin
	cmd.Stdout = os.Stdout
	cmd.Stderr = os.Stderr

	// syscall para el hostname
	must(syscall.Sethostname([]byte("container")))
	must(syscall.Chroot("/root/alpine"))
	must(syscall.Chdir("/"))
	must(syscall.Mount("proc", "proc", "proc", 0, ""))
	// Aquí ejecutamos el comando:
	must(cmd.Run())

	must(syscall.Unmount("proc", 0))

	fmt.Println("== Fin child ==")
}

func must(err error) {
	if err != nil {
		log.Panicln(err)
	}
}

</pre>

Filesystem:

`mkdir alpine`{{execute T2}}

`cd alpine`{{execute T2}}

`curl -o alpine.tar.gz http://dl-cdn.alpinelinux.org/alpine/v3.10/releases/x86_64/alpine-minirootfs-3.10.0-x86_64.tar.gz`{{execute T2}}

`tar xvf alpine.tar.gz`{{execute T2}}