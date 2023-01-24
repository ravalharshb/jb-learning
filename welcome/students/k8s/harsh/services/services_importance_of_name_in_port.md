When the Name is not used, we see the service as:

kubectl describe svc animals-bear-moose-svc
Name:                     animals-bear-moose-svc
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=animal-deploy
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       100.68.209.158
IPs:                      100.68.209.158
LoadBalancer Ingress:     ab3d0bab7c2d04f968d1a8bcc653c677-805744910.eu-west-1.elb.amazonaws.com
Port:                     **<unset>**  80/TCP
TargetPort:               80/TCP
NodePort:                 **<unset>**  31858/TCP
Endpoints:                100.121.145.83:80,100.121.145.84:80
Session Affinity:         None

When I added the name for the port, we see the service at:

kubectl describe svc animals-bear-moose-svc
Name:                     animals-bear-moose-svc
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=animal-deploy
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       100.68.209.158
IPs:                      100.68.209.158
LoadBalancer Ingress:     ab3d0bab7c2d04f968d1a8bcc653c677-805744910.eu-west-1.elb.amazonaws.com
Port:                     **http-web**  80/TCP
TargetPort:               80/TCP
NodePort:                 **http-web**  31858/TCP
Endpoints:                100.121.145.83:80,100.121.145.84:80
Session Affinity:         None
External Traffic Policy:  Cluster