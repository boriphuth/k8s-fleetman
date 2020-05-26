$ kubectl apply -f workloads.yaml
$ kubectl apply -f services.yaml

$ kubectl logs -f position-simulator-7d555dc46-h96mj
$ kubectl logs -f queue-5cb68d65b7-tctms
$ kubectl logs -f api-gateway-8577999d4f-xrqf7
$ kubectl logs -f webapp-77984bc8b4-rw6dm 
2019/10/27 09:09:25 [emerg] 1#1: host not found in upstream "fleetman-api-gateway.default.svc.cluster.local" in /etc/nginx/nginx.conf:23
nginx: [emerg] host not found in upstream "fleetman-api-gateway.default.svc.cluster.local" in /etc/nginx/nginx.conf:23

$ kubectl logs -f webapp-77984bc8b4-rw6dm sh

$ kubectl describe po position-tracker-5b6685986d-ndqgs
$ kubectl logs -f position-tracker-5b6685986d-ndqgs -v=9

