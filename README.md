# ESCAPE2020-WP2-CERN-Kubernetes-GitOps-with-Flux

## Pre-Requisites
A kubernetes cluster
Helm
fluxctl
## Secrets that need to be configured


## Running Flux
Add FLUX helm charts
```bash
helm repo add fluxcd https://charts.fluxcd.io
```

Add some HELM-FLUX custom resource definitions
```bash

kubectl apply -f https://raw.githubusercontent.com/fluxcd/helm-operator/master/deploy/crds.yaml
```

Create a flux namespace
```bash
kubectl create namespace flux
```

Fork Repo

Install the flux daemon that fetches the charts and manifests from your repo
```bash
helm upgrade -i flux fluxcd/flux \
--set git.url=git@github.com:USERNAME/ESCAPE2020-WP2-CERN-Kubernetes-GitOps-with-Flux \
--namespace flux 
```

Get flux public key
```bash
fluxctl identity --k8s-fwd-ns flux
```

Add flux public key to your deploy key repo settings with write permissions.

Install the helm-operator that applies the manifests
```bash
helm upgrade -i helm-operator fluxcd/helm-operator \
--set git.ssh.secretName=flux-git-deploy \
--namespace flux
```

Sync to test everything is working correctly
```bash
fluxctl sync
```

[Flux Documentation](https://docs.fluxcd.io/en/1.18.0/tutorials/get-started-helm.html)
