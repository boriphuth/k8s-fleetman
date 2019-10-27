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

$ kubectl apply -f networking-tests.yaml

## Interact in Pod
$ kubectl exec -it webapp-cf5b978df-fdz8w sh
/ # cat /etc/resolv.conf
/ # nslookup database
/ # apk update
/ # apk add mysql-client
/ # mysql -h database -uroot -ppassword fleetman
MySQL [fleetman]> create table testtable (test varchar(255));
MySQL [fleetman]> show tables;
MySQL [fleetman]> exit

## FQDN
/ # nslookup database
nslookup: can't resolve '(null)': Name does not resolve
Name:      database
Address 1: 10.98.236.124 database.default.svc.cluster.local