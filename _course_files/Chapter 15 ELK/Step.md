$ kubectl apply -f elastic-stack.yaml
$ kubectl apply -f fluentd-config.yaml

$ kubectl delete -f .

## Extend minikube
$ minikube stop

## Minikube Login
username:docker 
password:tcuser

## Delete mongodb
$ kubectl delete pod mongodb-7dc4596644-9bl8h