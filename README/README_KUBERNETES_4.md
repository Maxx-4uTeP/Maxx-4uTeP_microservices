# HW 24
# Kubernetes 4

# 9
kubectl apply -f tiller.yml
helm init --service-account tiller
kubectl get pods -n kube-system --selector app=helm

# 13 Удаляем старое говно и поднимаем новое )))
k delete deployment comment mongo post ui -n dev
helm install test-ui-1 kubernetes/Charts/ui
helm ls

# 21
helm install test-ui-2 kubernetes/Charts/ui
helm install test-ui-3 kubernetes/Charts/ui

# 26
helm upgrade test-ui-1 kubernetes/Charts/ui/
helm upgrade test-ui-2 kubernetes/Charts/ui/
helm upgrade test-ui-3 kubernetes/Charts/ui/

# 45
helm dep update kubernetes/Charts/reddit/

# 46
helm search hub mongo

# 47
helm dep update kubernetes/Charts/reddit/

# 48
helm install reddit-test kubernetes/Charts/reddit
helm uninstall post ui comment

# 53
helm dep update kubernetes/Charts/reddit/   
helm uninstall reddit
helm install reddit kubernetes/Charts/reddit/

helm uninstall reddit && helm dep update kubernetes/Charts/reddit/ && helm install reddit kubernetes/Charts/reddit/
k get ingress


