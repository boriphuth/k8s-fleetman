## Step 1) Installing the NFS Server
https://blog.exxactcorp.com/deploying-dynamic-nfs-provisioning-in-kubernetes/

```
Master nodes
sudo apt install nfs-kernel-server nfs-common portmap

[vagrant@kmaster ~]$ sudo mkdir /srv/nfs/kubedata -p
[vagrant@kmaster ~]$ sudo chown nfsnobody: /srv/nfs/kubedata/

[vagrant@kmaster ~]$ sudo systemctl enable nfs-server
[vagrant@kmaster ~]$ sudo systemctl start nfs-server
[vagrant@kmaster ~]$ sudo systemctl status nfs-server

[vagrant@kmaster ~]$ sudo vi /etc/exports
/srv/nfs/kubedata    *(rw,sync,no_subtree_check,no_root_squash,no_all_squash,insecure)

[vagrant@kmaster ~]$ sudo exportfs -rav
[vagrant@kmaster ~]$ sudo exportfs -v

Woker nodes
sudo apt install nfs-kernel-server nfs-common portmap

[vagrant@kworker1 ~]$ sudo mount -t nfs 192.168.1.201:/srv/nfs/kubedata /mnt
[vagrant@kworker1 ~]$ mount | grep kubedata
[vagrant@kworker1 ~]$ sudo umount /mnt

```

## Step 2) Deploying Service Account and Role Bindings
```
[vagrant@kmaster nfs-provisioning]$ kubectl create -f rbac.yaml
[vagrant@kmaster nfs-provisioning]$ kubectl get clusterrole,clusterrolebinding,role,rolebinding | grep nfs

```

## Step 3) Deploying Storage Class
```
[vagrant@kmaster nfs-provisioning]$ kubectl create -f class.yaml
[vagrant@kmaster nfs-provisioning]$ kubectl get storageclass

```

## Step 4) Deploying NFS Provisioner
```
[vagrant@kmaster nfs-provisioning]$ kubectl create -f deployment.yaml
[vagrant@kmaster nfs-provisioning]$ kubectl get all
[vagrant@kmaster ~]$ kubectl describe pod nfs-client-provisioner-6b64948cc7-4ds92

```

## Step 5) Creating Persistent Volume and Persistent Volume Claims
```
[vagrant@kmaster ~]$ kubectl get pv,pvc
[vagrant@k8s-master:]~$ sudo ls /srv/nfs/kubedata/
[vagrant@kmaster nfs-provisioning]$ kubectl create -f 4-pvc-nfs.yaml
[vagrant@kmaster nfs-provisioning]$ kubectl get pvc,pv

```

## Step 6) Creating a Pod to use Persistent Volume Claims
```
[vagrant@kmaster nfs-provisioning]$ kubectl get pods
[vagrant@kmaster nfs-provisioning]$ kubectl create -f 4-busybox-pv-nfs.yaml
[vagrant@kmaster nfs-provisioning]$ kubectl get pods
[vagrant@kmaster nfs-provisioning]$ kubectl describe pod busybox
[vagrant@kmaster nfs-provisioning]$ kubectl exec -it busybox -- ./bin/sh
/ # 
/ # ls /mydata/
/mydata # touch myfile


[vagrant@kmaster nfs-provisioning]$ sudo ls -la /srv/nfs/kubedata/default-pvc1-pvc-b228c5d6-c066-4bc9-8704-2e65a08c8f01/

```

## Step 7) Deleting Pods with Persistent Volume Claims
```
[vagrant@kmaster nfs-provisioning]$ kubectl delete pod busybox
[vagrant@kmaster nfs-provisioning]$ kubectl get pvc,pv
```
To delete the PV and PVC use “kubectl delete"
```
[vagrant@kmaster nfs-provisioning]$ kubectl delete pvc --all
[vagrant@kmaster nfs-provisioning]$ kubectl get pvc,pv



```

