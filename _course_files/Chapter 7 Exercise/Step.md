$ kubectl apply -f first-pod.yaml
$ kubectl apply -f webapp-service.yaml 

## Connect to Service
$  minikube service fleetman-webapp

$ kubectl get po --show-labels
NAME                 READY   STATUS    RESTARTS   AGE   LABELS
webapp               1/1     Running   0          92m   app=webapp,release=0
webapp-release-0-5   1/1     Running   0          48m   app=webapp,release=0-5

$ kubectl get po --show-labels -l release=0
$ kubectl get po --show-labels -l release=1
No resources found in default namespace.