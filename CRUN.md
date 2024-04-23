# CRUN

OCI Container Runtime (alternative zu runc (welcher default ist))

crun kann mit wasmedgeSupport kompiliert werden. (Bei Fedora4free)

Das doofe ist, dass der Runtime via Annotations gesagt werden muss, dass der Workload mit der wasmruntime ausgeführt werden muss.

Gegeben: crun mit wasmedgeSupport

~~~
$ crun --version
...
....  +WASM:wasmedge ...
$ 
~~~

Achtung `--annotation` beim build (kann nicht jeder) oder Aufruf.

Später in K8s als auch als `annotations`. Eventuell mit kyverno

~~~
podman build --runtime crun --annotation "module.wasm.image/variant=compat-smart" -f DockerfileWASM --platform wasi/wasm -t hallo 
podman run --rm hallo
podman run --rm --runtime crun --platform wasi/wasm --annotation "module.wasm.image/variant=compat-smart"    hallo 
~~~

