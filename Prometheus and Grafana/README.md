## https://blog.exxactcorp.com/deploying-prometheus-and-grafana-in-kubernetes/
## Step 1) Dynamic NFS Provisioning
```
[vagrant@kmaster ~]$ kubectl get storageclass -n kube-system
[vagrant@kmaster ~]$ kubectl patch storageclass managed-nfs-storage -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
[vagrant@kmaster ~]$ kubectl get storageclass -n kube-system

```

## Step 2) Installing Prometheus
```
[vagrant@kmaster /]$ helm2 install stable/kube-state-metrics --name kube-state-metrics --namespace kube-system
[vagrant@kmaster ~]$ helm2 search prometheus
[vagrant@kmaster ~]$ helm2 inspect values stable/prometheus > ./prometheus/prometheus.values

vagrant@kmaster:~/$ helm2 install stable/prometheus --name prometheus --values ./prometheus/prometheus.values --namespace prometheus

change
loadBalancerIP: ""
    loadBalancerSourceRanges: []
    servicePort: 80
    # nodePort: 30000
    sessionAffinity: None
    type: ClusterIP

To:
    loadBalancerIP: ""
    loadBalancerSourceRanges: []
    servicePort: 80
    nodePort: 32322
    type: NodePort


vagrant@kmaster:~$ kubectl get ns
vagrant@kmaster:~$ kubectl get all -n prometheus
vagrant@kmaster:~$ kubectl get svc prometheus-server -n prometheus

```
## Delete 
```
helm2 ls --all prometheus
helm2 del --purge prometheus
```


## Installing Grafana
helm2 ls -a
helm2 delete --purge grafana
$ helm upgrade -f ./grafana/grafana.values grafana stable/grafana

[vagrant@kmaster /]$ helm2 search grafana
[vagrant@kmaster /]$ helm2 inspect stable/grafana > ./grafana/grafana.values
[vagrant@kmaster ~]$ helm2 install stable/grafana --name grafana --values ./grafana/grafana.values --namespace grafana
[vagrant@kmaster]$  kubectl get secret --namespace grafana grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
[vagrant@kmaster tmp]$ kubectl get secret 
[vagrant@kmaster tmp]$ kubectl get pvc -n grafana
vagrant@k8s-master:~$ sudo ls -l /srv/nfs/kubedata/
[vagrant@kmaster /]$ kubectl get pods -n grafana -o wide
http://192.168.1.201:32323/login

## Kubernetes Clusters
$ kubectl apply -f grafana/grafana_deploy.yaml
$ kubectl apply -f grafana/grafana_node_exporter.yaml 

$ kubectl config view --minify --raw --output 'jsonpath={..cluster.certificate-authority-data}' | base64 -D | openssl x509 -text -out -