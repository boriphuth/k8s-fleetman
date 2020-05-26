$ kubectl apply -f pods.yaml
$ kubectl apply -f services.yaml 

## Connect to Service
$ minikube service fleetman-webapp
$ minikube service fleetman-queue

$ kubectl get po --show-labels
NAME                 READY   STATUS    RESTARTS   AGE   LABELS
queue                                     0/1     ContainerCreating   0          21s   app=queue
webapp                                    1/1     Running             0          38m   app=webapp,release=0
webapp-release-0                          1/1     Running             0          21s   app=webapp,release=0
webapp-release-0-5                        1/1     Running             0          31m   app=webapp,release=0-5

$ kubectl describe pods queue


kubectl rollout status deployment/prometheus-deployment -n monitoring 