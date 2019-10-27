$ kubectl apply -f pods.yaml
$ kubectl apply -f services.yaml 

## Connect to Service
$ minikube service fleetman-webapp
$ minikube service fleetman-queue

## Get namespace
$ kubectl get ns
NAME              STATUS   AGE
default           Active   23h
kube-node-lease   Active   23h
kube-public       Active   23h
kube-system       Active   23h

$ kubectl get all -n kube-system
$ kubectl describe svc kube-dns -n kube-system