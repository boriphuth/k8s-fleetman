## Deployments
```
kubectl apply -f deployment.yaml
kubectl scale deployment counter --replicas=2
```
## Results
new pod is same log count and use same Persistent Volumes


## StatefulSets
```
kubectl apply -f statefulset.yaml
kubectl scale statefulsets counter --replicas=3
```
## Results
new pod is different log count and different Persistent Volumes


## DaemonSet
```
kubectl apply -f daemonset.yaml
```
## Results
new pods equal to the number of nodes .it will behave the same as Deployments i.e. all pods will share the same Persistent Volume.