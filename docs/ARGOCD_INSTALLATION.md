# ArgoCD Installation

ArgoCD installation inside Kubernetes is very simple, just execute this line inside kubernetes
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
Because I am running ArgoCD in Baremetal Kubernetes, I change the service into NodePort.
```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
```
