# Technology Stack

## Core Technologies

- **GitOps**: ArgoCD with ApplicationSet pattern
- **Configuration Management**: Kustomize
- **Package Management**: Helm charts
- **Secret Management**: SOPS with age encryption, External Secrets Operator with 1Password
- **Operating System**: NixOS

## Key Tools & Frameworks

- **Kustomize**: Declarative Kubernetes configuration management
- **Helm**: Package manager for Kubernetes applications
- **SOPS**: Encrypted secrets in Git (age encryption key configured)
- **External Secrets Operator**: Syncs secrets from 1Password to Kubernetes
- **ArgoCD**: Continuous deployment and GitOps automation

## Common Commands

### Decrypt SOPS-encrypted files
```bash
sops -d apps/namespaces/<namespace>/<app>/values.sops.yaml
```

### Encrypt files with SOPS
```bash
sops -e apps/namespaces/<namespace>/<app>/values.yaml > values.sops.yaml
```

### Build Kustomize manifests locally
```bash
kubectl kustomize apps/namespaces/<namespace>/<app>
```

### Validate Kustomize configuration
```bash
kustomize build apps/namespaces/<namespace>/<app> | kubectl apply --dry-run=client -f -
```

### Sync ArgoCD application manually
```bash
argocd app sync <namespace>-<app-name>
```

### View ArgoCD application status
```bash
argocd app get <namespace>-<app-name>
```

## Deployment Pattern

Applications are automatically discovered and deployed via ArgoCD ApplicationSet that scans `apps/namespaces/*/*` directories. Each application is named `<namespace>-<app-name>` and deployed to its corresponding namespace.
