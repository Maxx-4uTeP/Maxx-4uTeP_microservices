# HW 21
# Kubernetes 2

# 8
minikube delete
minikube start --kubernetes-version 1.19.7

# 10
kubectl get nodes

# 12
cat ~/.kube/config

# 17 проверить текущий контекст
kubectl config current-context

# 22
cd kubernetes/reddit
kubectl apply -f ui-deployment.yml
kubectl get deployment

# можно запустить сразу папку (Слабоумие и Отвага!!!1)
cd ../..
kubectl apply -f ./kubernetes/reddit

# 23
kubectl get pods --selector component=ui
kubectl port-forward <pod-name> 8080:9292

# 32
kubectl describe service comment  | grep Endpoints

# 53 вообще не нужная команда
kubectl get all -n kube-system --selector k8s-app=kubernetes-dashboard

# 54
minikube addons enable dashboard
minikube dashboard --url

# 56
cd kubernetes/reddit
kubectl apply -f dev-namespace.yml

# 57
kubectl apply -n dev -f ./kubernetes/reddit --force
minikube service ui -n dev

# 59
kubectl apply -n dev -f ./kubernetes/reddit/ui-deployment.yml --force

# 70
yc managed-kubernetes cluster get-credentials ololo --external

# 71
kubectl config current-context

# 72
kubectl apply -f ./kubernetes/reddit/dev-namespace.yml
kubectl apply -f ./kubernetes/reddit/ -n dev

# 73
kubectl get nodes -o wide
kubectl describe service ui -n dev | grep NodePort





