$ kubectl apply -f storage.yaml
$ kubectl apply -f mongo-stack.yaml
$ kubectl apply -f services.yaml
$ kubectl apply -f workloads.yaml
$ kubectl delete -f .

## Extend minikube
$ minikube stop

## Minikube Login
username:docker 
password:tcuser

## Delete mongodb
$ kubectl delete pod mongodb-7dc4596644-9bl8h