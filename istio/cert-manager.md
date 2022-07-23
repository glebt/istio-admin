## cert-manager
#istio 

### install cmctl
[cmctl](https://cert-manager.io/docs/usage/cmctl/)

```bash
OS=$(go env GOOS); ARCH=$(go env GOARCH); curl -sSL -o cmctl.tar.gz https://github.com/cert-manager/cert-manager/releases/download/v1.7.1/cmctl-$OS-$ARCH.tar.gz
tar xzf cmctl.tar.gz
sudo mv cmctl /usr/local/bin
```

### install cert-manager with cmctl
```bash
cmctl x install -n cert-manager
```

### or install cert-manager with helm chart
```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update
kubectl create namespace cert-manager
helm install -n cert-manager cert-manager jetstack/cert-manager --set installCRDs=true
```

### verify
```bash
for i in cert-manager cert-manager-cainjector cert-manager-webhook; \
do kubectl rollout status deploy/$i -n cert-manager; done
```

### configure
```bash
kubectl apply -n istio-system -f - <<EOF
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: selfsigned
spec:
  selfSigned: {}
---
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: istio-ca
spec:
  isCA: true
  duration: 2160h # 90d
  secretName: istio-ca
  commonName: istio-ca
  subject:
    organizations:
    - cert-manager
  issuerRef:
    name: selfsigned
    kind: Issuer
    group: cert-manager.io
---
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: istio-ca
spec:
  ca:
    secretName: istio-ca
EOF
```
[tetrade](https://istio.tetratelabs.io/istio-ca-certs-integrations/cert-manager-integration/)

