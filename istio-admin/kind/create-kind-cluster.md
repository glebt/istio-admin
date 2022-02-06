## Quickly spin up a new Kind cluster
#kind 

[kind](https://kind.sigs.k8s.io/)

```bash
kind create cluster #with default name kind
```

```bash
export CLUSTER_NAME=istio-admin
```

```bash
kind create cluster --name $CLUSTER_NAME --config - <<EOF
# config file
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
- role: worker
EOF

```
