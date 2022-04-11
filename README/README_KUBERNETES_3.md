# HW 23
# Kubernetes 3
k delete deployment post mongo ui comment -n dev
kubectl apply -f ./kubernetes/reddit/ -n dev --force
kubectl describe service ui -n dev | grep NodePort

# 7
kubectl get services -n dev

# 11
kubectl scale deployment --replicas 0 -n kube-system kube-dns-autoscaler
kubectl scale deployment --replicas 0 -n kube-system kube-dns

# 12
kubectl scale deployment --replicas 1 -n kube-system kube-dns-autoscaler

# 23
kubectl apply -f ./kubernetes/reddit/ -n dev --force
kubectl get service -n dev --selector component=ui

# 30
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.34.1/deploy/static/provider/cloud/deploy.yaml

# 34
kubectl get ingress -n dev

# 40
kubectl get ingress -n dev
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=51.250.66.167"
kubectl create secret tls ui-ingress --key tls.key --cert tls.crt -n dev
kubectl describe secret ui-ingress -n dev

# 41
kubectl apply -f ./kubernetes/reddit/ -n dev --force

# 50
kubectl apply -f ./kubernetes/reddit/mongo-network-policy.yml -n dev

# 56
yc compute disk create \
    --name k8s \
    --size 4 \
    --description "disk for k8s"

yc compute disk list
+----------------------+------+--------------+---------------+--------+----------------------+--------------+
|          ID          | NAME |     SIZE     |     ZONE      | STATUS |     INSTANCE IDS     | DESCRIPTION  |
+----------------------+------+--------------+---------------+--------+----------------------+--------------+
| fhm6nk9b6sinpk2vl6mc | k8s  |   4294967296 | ru-central1-a | READY  |                      | disk for k8s |
| fhmocjb5331h81q7lo3u |      | 103079215104 | ru-central1-a | READY  | fhmk27eqjuei9i7m9dqk |              |
| fhmu81n2tdeefa0t04cs |      | 103079215104 | ru-central1-a | READY  | fhmbdis1rsta0tos1rcl |              |
+----------------------+------+--------------+---------------+--------+----------------------+--------------+

# 63
kubectl apply -f ./kubernetes/reddit/ -n dev --force
kubectl delete deploy mongo -n dev
kubectl apply -f ./kubernetes/reddit/ -n dev --force










