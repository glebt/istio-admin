### install
```bash
helm repo add istio https://istio-release.storage.googleapis.com/charts
helm repo update
kubectl create namespace istio-system

#base
helm install istio-base istio/base -n istio-system
helm install istiod istio/istiod -n istio-system --wait
```

### references
[src](https://istio.io/latest/docs/setup/install/helm/)