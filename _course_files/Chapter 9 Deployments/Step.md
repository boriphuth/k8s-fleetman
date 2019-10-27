$ kubectl apply -f pods.yaml
$ kubectl apply -f services.yaml 

## Connect to Service
$ minikube service fleetman-webapp
$ minikube service fleetman-queue

$ kubectl get po --show-labels
NAME                 READY   STATUS    RESTARTS   AGE   LABELS
webapp               1/1     Running   0          92m   app=webapp,release=0
webapp-release-0-5   1/1     Running   0          48m   app=webapp,release=0-5

$ kubectl get po --show-labels -l release=0
$ kubectl get po --show-labels -l release=1
No resources found in default namespace.

$ kubectl describe svc

## Test delete pod to see  replicaSet
$ kubectl delete po --all

## Deploy different version
```
pods.yaml
minReadySeconds: 30
```
## Rollouts
change image: richardchesterwood/k8s-fleetman-webapp-angular:release0
$ kubectl rollout status webapp
$ kubectl rollout status deploy webapp
$ kubectl rollout history deploy webapp
$ kubectl rollout undo deploy webapp --to-revision=7
$ kubectl rollout undo deploy webapp

## Error docker images
image: richardchesterwood/k8s-fleetman-webapp-angular:release0-5
$ kubectl apply -f pods.yaml
$ kubectl describe pod webapp-7c7cd8cd7-8zmmt