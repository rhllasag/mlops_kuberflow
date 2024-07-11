# Kuberflow installed in WSL2 to MLOps at home
This repository creates a cluser on kubernetes for coveing Kuberflow Overview Diagram

![Alt text](./images/kubeflow-intro-diagram.drawio.svg)
<img src="./images/kubeflow-intro-diagram.drawio.svg">

# Requirements

-   Kuberflow
-   WSL2
-   Git
-   Python 3
-   Pip
-   Visual Code
-   Docker
-   Kind

# Official documentation

> [Kubernetes](https://kubernetes.io/)
> [Kuberflow](https://www.kubeflow.org/)
> [Go](https://kind.sigs.k8s.io/)
> [VisualCode](https://code.visualstudio.com/)
> [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install)
> [MLFlow](https://mlflow.org/)
> [Docker](https://docs.docker.com/)
> [DockerHub](https://hub.docker.com/)
> [Jenkings](https://www.jenkins.io/)
> [Kind](https://kind.sigs.k8s.io/)

## Installation
```
git clone https://github.com/rhllasag/mlops_kuberflow.git
cd mlops_kuberflow
```
### Cluster
```
kind create cluster --config kind-cluster-config.yaml
kubectl apply -f namespace.yaml 
cd mlflow/
kubectl apply -f mlflow-pvc-yaml 
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
kubectl apply -f mlflow-app.yaml
kubectl apply -f mlflow-ingress.yaml
```
### Status
```
kubectl port-forward svc/mlflow 5000:80 -n mlops-tools
kubectl get services -n mlops-tools
kubectl get pods -n mlops-tools
kubectl get ingress -n mlops-tools
```
### Check Endpoints
```
[ENDPOINTS]
kubectl get endpoints mlflow -n mlops-tools
kubectl get all
kubectl get pods
kubectl get services
kubectl get ingress
```
### Delete Cluster
```
cd ..
kind delete cluster --name kuberflow
kubectl  delete -f mlflow-app.yaml
```
### Ingress status
```
kubectl describe ingress mlflow-ingress -n mlops-tools
kubectl logs -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx
```
### Restart deployment
```
kubectl rollout restart deployment ingress-nginx-controller -n ingress-nginx
```
### Host
```
sudo nano /etc/hosts
hostname -i
sudo systemctl restart systemd-networkd
```