# Biske labern

Was ich eigentlich vor hatte, aber ich muss noch was zum Imagabau sagen..

Motivation: Kubernetes als RZ, also als "Runtime" für alles. (z.B. auch Kubevirt)
Es geht nicht um eine Einführung in Webassembly
Wir wollen nur schauen, wie es in Kubernetes läuft
Es geht darum eine Runtime in Kubernetes zu integrieren umd WASM-Module/Code auszuführen.
Da schauen wir uns veschiedene Methoden an.

Z.B. das es auch und vor allem in Embeded geil werden könnte


# 

Wir wollen Webassembly also ausserhalb eines Browsers laufen lassen.
WASI => WebAssembly System Interface (0.2.0 behandeln wir nicht)

Hier gibt es eine fülle von Implementierungen (wir nehmen wasmtime u. wasmedge).


Binary bauen

~~~
GOOS=wasip1 GOARCH=wasm go build -o main.wasm main.go
~~~

~~~
wasmtime ./main.wasm
wasmedge ./main.wasm
~~~

Toll, dass ist aber in nem Container 

~~~
docker build -f DockerfileOCI -t jaxwiegaudi:oci .
docker container run --rm jaxwiegaudi:oci
~~~

Warum reicht das nicht? (keinen Plan)

Wir wollen "WASM"Images (warum/wann klappt das? `/etc/docker/daemon.json`)

~~~
docker build --platform wasi/wasm --provenance=false -f DockerfileWASM  -t jaxwiegaudi:wasm .
docker container run --rm --runtime wasmtime --platform wasi/wasm  jaxwiegaudi:wasm 
~~~


# Supar ABA KUBERNETES!!!

Bild malen

Containerd + [runwasi](https://github.com/containerd/runwasi)

Auf das Daemonmodell eingehen

RuntimeClasses

Kurz auf CRI-O und crun verweisen und wie doof das ist ( Handson in: CRUN.md)


# Zeigen mit Probs

deployment.yaml und deployment-wasmtime.yaml (mit ohne annotations crun vs shim)






# (Serverless) Framework


Irgendwie sollte Knative hier etwas mehr Aufmerksamkeit bekommen können. 
Naja es gibt (mind.) zwei Framworks für mit WebAssembly:
 
* [Spin/Ferymon](https://www.fermyon.com/_
* [WasmCloud](https://wasmcloud.com/)
Beide bauen auf runwasi auf.

Gerade auf WASI 0.2.0 24.01.24 eingehen und dem Webassembly Componenten Modell



# MONITORING?????

wie wird das gemonitort?

