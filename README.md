
[INSTALL]
kind create cluster --config kind-cluster-config.yaml
kubectl apply -f namespace.yaml 
cd mlflow/
kubectl apply -f mlflow-pvc-yaml 
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
kubectl apply -f mlflow-app.yaml
kubectl apply -f mlflow-ingress.yaml


[STATUS]
kubectl port-forward svc/mlflow 5000:80 -n mlops-tools
kubectl get services -n mlops-tools
kubectl get pods -n mlops-tools
kubectl get ingress -n mlops-tools

[ENDPOINTS]
kubectl get endpoints mlflow -n mlops-tools
kubectl get all

[DELETE]
cd ..
kind delete cluster --name kuberflow
kubectl  delete -f mlflow-app.yaml

[INGRESS]
kubectl describe ingress mlflow-ingress -n mlops-tools
kubectl logs -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx

[RESTART]
kubectl rollout restart deployment ingress-nginx-controller -n ingress-nginx

[HOSTNAME_WSL2]
sudo nano /etc/hosts
hostname -i
sudo systemctl restart systemd-networkd