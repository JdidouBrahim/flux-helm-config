# Flux and Helm Kubernetes Deployment

This repository is used to manage Kubernetes resources using Flux and Helm in a GitOps workflow.

## Structure

The repository is structured as follows:


## Tools Used
1. **Flux**: Automates the deployment and lifecycle management of Kubernetes resources.
2. **Helm**: Manages Kubernetes applications using Helm charts.

## Prerequisites
- A Kubernetes cluster (local: `minikube`, `kind`; cloud: EKS, GKE, AKS, etc.).
- `kubectl` CLI configured to interact with your cluster.
- `flux` CLI installed ([installation guide](https://fluxcd.io/docs/installation/)).
- `helm` CLI installed ([installation guide](https://helm.sh/docs/intro/install/)).
- A GitHub account.

## Usage

### 1. Bootstrap Flux
Run the following command to bootstrap Flux into the Kubernetes cluster and link it to this repository:

```bash
flux bootstrap github \
  --context=default \
  --owner=<your-github-username> \
  --repository=flux-helm-config \
  --branch=main \
  --personal
```

### 2. Add a Helm Repository

Create a `HelmRepository` resource in your repository to allow Flux to fetch charts:

```yaml
apiVersion: source.toolkit.fluxcd.io/v1beta2
kind: HelmRepository
metadata:
  name: bitnami
  namespace: flux-system
spec:
  url: https://charts.bitnami.com/bitnami
  ```


---

### Explanation of Fix
- **Code Block Syntax**: Use triple backticks (\`\`\`) followed by `yaml` to specify the language for syntax highlighting.
- **Proper Nesting**: Make sure the YAML snippet is indented inside the Markdown block.

Let me know if you'd like me to review the full `README.md` with all corrections applied!


### 3. Deploy Nginx using HelmRelease

Define a `HelmRelease` resource in your repository to deploy Nginx:

```yaml
apiVersion: helm.toolkit.fluxcd.io/v2beta1
kind: HelmRelease
metadata:
  name: nginx
  namespace: default
spec:
  releaseName: nginx
  chart:
    spec:
      chart: nginx
      version: 15.0.0
      sourceRef:
        kind: HelmRepository
        name: bitnami
        namespace: flux-system
  interval: 5m
  values:
    replicaCount: 2
```



---

### Explanation of Fix
- **Code Block Syntax**: Wrapped the YAML block inside triple backticks (\`\`\`) with `yaml` specified for syntax highlighting.
- **Proper Nesting**: The YAML content is now correctly displayed and readable in Markdown.

If you'd like, I can provide a fully corrected `README.md` with all sections reviewed and improved! Let me know!

