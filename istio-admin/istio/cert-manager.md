## cert-manager
#istio 

### install cmctl
[cmctl](https://cert-manager.io/docs/usage/cmctl/)

```bash
curl -L -o cmctl.tar.gz https://github.com/jetstack/cert-manager/releases/latest/download/cmctl-linux-arch.tar.gz
tar xzf cmctl.tar.gz
sudo mv cmctl /usr/local/bin
```

### install cert-manager
```bash
cmctl x install -n cert-manager
```

### configure 
[tetrade](https://istio.tetratelabs.io/istio-ca-certs-integrations/cert-manager-integration/)
