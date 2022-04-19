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

# 55
k create namespace reddit-ns
helm install reddit kubernetes/Charts/reddit/ --wait --namespace=reddit-ns
k get ingress -nreddit-ns

# 61
helm repo add gitlab https://charts.gitlab.io
helm fetch gitlab/gitlab-omnibus  --version 0.1.37 --untar

# 64 это нихера не работает
helm dep update gitlab-omnibus
helm install gitlab gitlab-omnibus

# from internet https://docs.gitlab.com/charts/quickstart/index.html
helm install gitlab gitlab/gitlab \
  --set global.hosts.domain=maxx.su \
  --set certmanager-issuer.email=maxx@maxx.su

kubectl get ingress -lrelease=gitlab
echo "51.250.73.242 gitlab.maxx.su minio.maxx.su registry.maxx.su” >> /etc/hosts


kubectl get secret gitlab-gitlab-initial-root-password -ojsonpath='{.data.password}' | base64 --decode ; echo
root
EuzVaN8FtiknNcZILYt9QQKBmTJSwq9HE84wkaTfq5nG4pSqpD6SaKI5hha6zxe0





