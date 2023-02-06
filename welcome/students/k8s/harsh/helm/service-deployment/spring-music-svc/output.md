Helm Install:
```bash
helm install spring-music ./spring-music-svc --debug

install.go:193: [debug] Original chart version: ""
install.go:210: [debug] CHART PATH: /home/ubuntu/workarea/jb-learning/welcome/students/k8s/harsh/helm/service-deployment/spring-music-svc

client.go:396: [debug] checking 2 resources for changes
client.go:675: [debug] Looks like there are no changes for Service "spring-music-service"
client.go:417: [debug] Created a new Deployment called "spring-music-deployment" in default

NAME: spring-music
LAST DEPLOYED: Mon Feb  6 16:29:13 2023
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
USER-SUPPLIED VALUES:
{}

COMPUTED VALUES:
deployment:
  container_name: spring-music
  container_port: 8080
  replica_val: 2
pods:
  image: yanivomc/spring-music
  tag: latest
service:
  node_port: 80
  port_name: http
  spec_type: LoadBalancer

HOOKS:
MANIFEST:
---
# Source: spring-music-svc/templates/spring-service.yaml
kind: Service     
apiVersion: v1     
metadata:
  name: spring-music-service #from RELEASE NAME
spec:
  selector:
    app: music    
  type: LoadBalancer  #from values | DEFAULT TO NODEPORT
  ports:         
  - name: http   
    protocol: TCP
    port: 80
    targetPort: 8080
---
# Source: spring-music-svc/templates/spring-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: spring-music-deployment #from RELEASE NAME
spec:
  selector: 
    matchLabels:
      app: music  
  replicas: 2  #from values
  template:
    metadata:
      labels:
        app: music
    spec:
      containers:
      - name: spring-music #from values
        image: yanivomc/spring-music:latest #from values
        ports:
        - containerPort: 8080
```
Helm list charts:

```bash
helm ls

NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
spring-music    default         1               2023-02-06 16:29:13.39819182 +0000 UTC  deployed        spring-music-svc-0.1.0  1.16.0
```

Fetch K8s service:
```bash
kubectl get service

NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   100.64.0.1   <none>        443/TCP   3h54m
```

Fetch K8s deployment:
```bash
kubectl get deployment

NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
spring-music-deployment   2/2     2            2           93s
```

Fetch K8s pods:
```bash
kubectl get pods

NAME                                       READY   STATUS    RESTARTS   AGE
spring-music-deployment-68854f579c-9q25v   1/1     Running   0          98s
spring-music-deployment-68854f579c-tg24h   1/1     Running   0          97s
```

If you do decide to update the values and need to redeploy use command:
```bash
helm update spring-music ./spring-music-svc --debug
```

If you would like to delete it, use uninstall command:
```bash
helm uninstall spring-music
```