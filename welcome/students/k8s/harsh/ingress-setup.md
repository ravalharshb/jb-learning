FOLLOW:https://kubernetes.github.io/ingress-nginx/deploy/#aws   (NOT TLS!!)

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.0/deploy/static/provider/aws/deploy.yaml
> namespace/ingress-nginx created
serviceaccount/ingress-nginx created
configmap/ingress-nginx-controller created
clusterrole.rbac.authorization.k8s.io/ingress-nginx created
clusterrolebinding.rbac.authorization.k8s.io/ingress-nginx created
role.rbac.authorization.k8s.io/ingress-nginx created
rolebinding.rbac.authorization.k8s.io/ingress-nginx created
service/ingress-nginx-controller-admission created
service/ingress-nginx-controller created
deployment.apps/ingress-nginx-controller created
ingressclass.networking.k8s.io/nginx created
validatingwebhookconfiguration.admissionregistration.k8s.io/ingress-nginx-admission created
serviceaccount/ingress-nginx-admission created
clusterrole.rbac.authorization.k8s.io/ingress-nginx-admission created
clusterrolebinding.rbac.authorization.k8s.io/ingress-nginx-admission created
role.rbac.authorization.k8s.io/ingress-nginx-admission created
rolebinding.rbac.authorization.k8s.io/ingress-nginx-admission created
job.batch/ingress-nginx-admission-create created
job.batch/ingress-nginx-admission-patch created

```

Verify installation:

```bash
kubectl get svc -n ingress-nginx ingress-nginx-controller
> NAME                       TYPE           CLUSTER-IP      EXTERNAL-IP                                                                     PORT(S)                      AGE
ingress-nginx-controller   LoadBalancer   100.70.116.71   a119fefc10f8046a7979476b9527a1ba-039653074ee2053d.elb.eu-west-1.amazonaws.com   80:30406/TCP,443:30626/TCP   55s

(check that the LB is available)
kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
Expected:
NAME                                        READY   STATUS      RESTARTS   AGE
ingress-nginx-admission-create-r2642        0/1     Completed   0          3m42s
ingress-nginx-admission-patch-9zzl7         0/1     Completed   1          3m42s
ingress-nginx-controller-57cb5bf694-2qks4   1/1     Running     0          3m42s

> kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
NAME                                        READY   STATUS      RESTARTS   AGE
ingress-nginx-admission-create-m69kd        0/1     Completed   0          4m26s
ingress-nginx-admission-patch-6srt6         0/1     Completed   1          4m26s
ingress-nginx-controller-7d5548585f-9gqm4   1/1     Running     0          4m27s
```

```bash
kubectl get ingressclass
>NAME    CONTROLLER             PARAMETERS   AGE
nginx   k8s.io/ingress-nginx   <none>       88s

kubectl describe ingressclass NAME
> kubectl describe ingressclass nginx
Name:         nginx
Labels:       app.kubernetes.io/component=controller
              app.kubernetes.io/instance=ingress-nginx
              app.kubernetes.io/managed-by=Helm
              app.kubernetes.io/name=ingress-nginx
              app.kubernetes.io/version=1.0.0
              helm.sh/chart=ingress-nginx-4.0.1
Annotations:  <none>
Controller:   k8s.io/ingress-nginx
Events:       <none>
```