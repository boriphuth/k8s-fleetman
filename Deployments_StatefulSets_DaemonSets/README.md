## Deployments
```
kubectl apply -f deployment.yaml
kubectl scale deployment counter --replicas=2
```

## StatefulSets
```
kubectl apply -f statefulset.yaml
kubectl scale statefulsets counter --replicas=3
```

## DaemonSet
```
kubectl apply -f daemonset.yaml
```