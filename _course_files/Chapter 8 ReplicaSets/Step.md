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