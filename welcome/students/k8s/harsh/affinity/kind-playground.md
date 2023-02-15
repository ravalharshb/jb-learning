Use k8s playground https://killercoda.com/kubernetes/scenario/a-playground
Kind
Install docker
Install k8s kind (download it)
Run 
kind create cluster -f mycluster.yaml



KIND CONFIGURATION: 
```bash
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```