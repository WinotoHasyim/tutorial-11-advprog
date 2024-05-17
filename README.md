# tutorial-11-advprog

## Reflection on Hello Minikube

### Compare the application logs before and after you exposed it as a Service.
```
PS C:\Users\Ato> kubectl logs hello-node-55fdcd95bf-l8zc8
I0514 06:34:15.423085       1 log.go:195] Started HTTP server on port 8080
I0514 06:34:15.423382       1 log.go:195] Started UDP server on port  8081
PS C:\Users\Ato> kubectl expose deployment hello-node --type=LoadBalancer --port=8080
service/hello-node exposed
PS C:\Users\Ato> kubectl get services
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
hello-node   LoadBalancer   10.107.40.86   <pending>     8080:31969/TCP   14s
kubernetes   ClusterIP      10.96.0.1      <none>        443/TCP          17h
PS C:\Users\Ato> minikube service hello-node
W0514 13:41:45.591560   23344 main.go:291] Unable to resolve the current Docker CLI context "default": context "default": context not found: open C:\Users\Ato\.docker\contexts\meta\37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f\meta.json: The system cannot find the path specified.
|-----------|------------|-------------|-----------------------------|
| NAMESPACE |    NAME    | TARGET PORT |             URL             |
|-----------|------------|-------------|-----------------------------|
| default   | hello-node |        8080 | http://172.30.244.180:31969 |
|-----------|------------|-------------|-----------------------------|
🎉  Opening service default/hello-node in default browser...
PS C:\Users\Ato> kubectl logs hello-node-55fdcd95bf-l8zc8
I0514 06:34:15.423085       1 log.go:195] Started HTTP server on port 8080
I0514 06:34:15.423382       1 log.go:195] Started UDP server on port  8081
I0514 06:41:49.215859       1 log.go:195] GET /
I0514 06:41:49.532204       1 log.go:195] GET /
PS C:\Users\Ato> minikube service hello-node
W0514 14:04:18.313062   29976 main.go:291] Unable to resolve the current Docker CLI context "default": context "default": context not found: open C:\Users\Ato\.docker\contexts\meta\37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f\meta.json: The system cannot find the path specified.
|-----------|------------|-------------|-----------------------------|
| NAMESPACE |    NAME    | TARGET PORT |             URL             |
|-----------|------------|-------------|-----------------------------|
| default   | hello-node |        8080 | http://172.30.244.180:31969 |
|-----------|------------|-------------|-----------------------------|
🎉  Opening service default/hello-node in default browser...
PS C:\Users\Ato> kubectl logs hello-node-55fdcd95bf-l8zc8
I0514 06:34:15.423085       1 log.go:195] Started HTTP server on port 8080
I0514 06:34:15.423382       1 log.go:195] Started UDP server on port  8081
I0514 06:41:49.215859       1 log.go:195] GET /
I0514 06:41:49.532204       1 log.go:195] GET /
I0514 07:04:27.686076       1 log.go:195] GET /
I0514 07:04:28.284392       1 log.go:195] GET /
I0514 07:04:28.311371       1 log.go:195] GET /
PS C:\Users\Ato>
```
Jumlah logs bertambah setelah mengakses servicenya

### What is the purpose of the `-n` option and why did the output not list the pods/services that you explicitly created?

-n digunakan untuk mengspesifikasikan namespace dalam menampilkan servies/resources. Dalam hal ini, kubectl get services -n kube-system akan menampilkan service dari namespace kube-system. Jika tidak menspesifikasikan namespace, maka servies yang akan ditampilkan berasal dari namespace `default`
