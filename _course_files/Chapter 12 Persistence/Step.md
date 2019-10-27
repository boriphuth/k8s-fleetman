$ kubectl apply -f workloads.yaml
$ kubectl apply -f services.yaml

$ kubectl logs -f position-simulator-d5fdcbc98-lvnqq
$ kubectl logs -f webapp-5c5dcc8d66-wncj9
2019/10/27 09:09:25 [emerg] 1#1: host not found in upstream "fleetman-api-gateway.default.svc.cluster.local" in /etc/nginx/nginx.conf:23
nginx: [emerg] host not found in upstream "fleetman-api-gateway.default.svc.cluster.local" in /etc/nginx/nginx.conf:23

$ kubectl logs -f webapp-5c5dcc8d66-wncj9 sh