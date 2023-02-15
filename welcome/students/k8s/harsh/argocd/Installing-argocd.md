Installing ARGO CD
we start by installing ArgoCD in our K8S Cluster.

Please follow the next instructions.

Create a new namespace called “argocd”
```bash
kubectl create namespace argocd
```

apply;
```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

verify that all is working by running 
```bash
kubectl get pods -n argocd -w 
```
wait until everything is running 

Change the argocd services to type loadbalancer using kubectl PATCH
```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

verify: 
```bash
kubectl get svc argocd-server -n argocd
```

Get the initial password (user is: admin ) :
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Test access to ui:

To browse: 
https://<External-IP from kubectl get svc argocd-server -n argocd>

