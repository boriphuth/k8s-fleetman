$ kubectl apply -f pods.yaml
$ kubectl apply -f services.yaml 

## Connect to Service
$ minikube service fleetman-webapp
$ minikube service fleetman-queue

$ kubectl get po --show-labels

$ kubectl describe rs webapp

$ kubectl describe svc

## Test delete pod to see  replicaSet
$ kubectl delete po webapp-kgqwb