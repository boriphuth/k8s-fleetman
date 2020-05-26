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
$ kubectl get all
$ kubectl exec -it webapp-858957ccc9-lzw62 sh

/ # apk update
/ # apk add mysql-client
/ # mysql -h database -uroot -ppassword fleetman
MySQL [fleetman]> create table testtable (test varchar(255));
MySQL [fleetman]> show tables;
+--------------------+
| Tables_in_fleetman |
+--------------------+
| testtable          |
+--------------------+
1 row in set (0.01 sec)
MySQL [fleetman]> exit

## FQDN
/ # nslookup database
nslookup: can't resolve '(null)': Name does not resolve
Name:      database
Address 1: 10.98.236.124 database.default.svc.cluster.local

/ # cat /etc/resolv.conf
nameserver 10.96.0.10
search default.svc.cluster.local svc.cluster.local cluster.local
options ndots:5

$ kubectl config get-contexts
CURRENT   NAME                               CLUSTER           AUTHINFO                NAMESPACE
*         kubernetes-admin@example           example           kubernetes-admin        
          kubernetes-admin@kubernetes        kubernetes        kubernetes-admin        
          kubernetes-bori-admin@kubernetes   kubernetes-bori   kubernetes-bori-admin   
          minikube                           minikube          minikube     

$ kubectl config current-context
kubernetes-admin@example

$ kubectl config use-context kubernetes-bori-admin@kubernetes  