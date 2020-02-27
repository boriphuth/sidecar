## More Info at
```
https://www.magalix.com/blog/implemeting-a-reverse-proxy-server-in-kubernetes-using-the-sidecar-pattern
```
## Step
```
$ docker rm -vf $(docker ps -a -q)

$ cd app
$ docker build -t boriphuth/flasksidecar .
$ docker run -d -p 5000:5000 boriphuth/flasksidecar
$ curl localhost:5000
{"message":"Hello World!"}
$ docker push boriphuth/flasksidecar

$ cd web
$ docker build -t boriphuth/nginxsidecar .
$ docker push boriphuth/nginxsidecar

$ kubectl apply -f deploy_nosidecar.yml 
$ kubectl delete -f deploy_nosidecar.yml 
$ curl http://192.168.64.52:32001/
{"message":"Hello World!"}

$ kubectl apply -f deploy.yml
$ kubectl delete -f deploy.yml

$ minikube start --cpus 4 --memory 8192
```