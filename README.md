# ESCAPE2020-WP2-CERN-Kubernetes-GitOps-with-Flux

## Pre-Requisites
A kubernetes cluster
Helm

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

Install the flux daemon that fetches the charts and manifests from this repo
```bash
helm upgrade -i flux fluxcd/flux \
--set git.url=git@github.com:arisfkiaras/ESCAPE2020-WP2-CERN-Kubernetes-GitOps-with-Flux/flux-get-started \
--namespace flux 
```

Install the helm-operator that applies the manifests
```bash
helm upgrade -i helm-operator fluxcd/helm-operator \
--set git.ssh.secretName=flux-git-deploy \
--namespace flux
```

[Flux Documentation]([google.com](https://docs.fluxcd.io/en/1.18.0/tutorials/get-started-helm.html))
