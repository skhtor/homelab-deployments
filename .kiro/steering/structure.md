# Project Structure

## Repository Layout

```
.
├── app-of-apps.yaml          # Root ArgoCD Application (app-of-apps pattern)
├── appsets/                  # ArgoCD ApplicationSet definitions
│   └── nix-homelab-appset.yaml
├── apps/namespaces/          # Application deployments organized by namespace
│   └── <namespace>/
│       └── <app>/
│           ├── kustomization.yaml
│           ├── values.yaml (or values.sops.yaml for encrypted)
│           └── resources/    # Raw Kubernetes manifests
└── charts/                   # Custom Helm charts
    └── web-app/              # Generic web application chart
```

## Application Organization

Applications are organized in a three-level hierarchy:
- `apps/namespaces/<namespace>/<app-name>/`

Each application directory follows one of two patterns:

### Pattern 1: Helm-based (most common)
```
<app-name>/
├── kustomization.yaml    # Defines Helm chart source
└── values.yaml           # Helm values (or values.sops.yaml if encrypted)
```

### Pattern 2: Raw Kubernetes manifests
```
<app-name>/
├── kustomization.yaml    # Lists resources
└── resources/            # Raw YAML manifests
    ├── deployment.yaml
    ├── service.yaml
    ├── ingress.yaml
    └── external-secret.yaml
```

## Namespace Categories

- **agd**: AGD-specific applications (enrolment-form, n8n, nocodb, postgresql)
- **argocd**: ArgoCD deployment
- **automation**: Workflow automation tools
- **foosball-elo**: Foosball ELO rating system (api, db, ui)
- **gaming**: Game servers
- **gotify-system**: Notification service
- **longhorn-system**: Storage orchestration
- **media-server**: Media streaming and management applications
- **monitoring**: Observability stack
- **networking**: Network infrastructure (DNS, ingress, load balancing)
- **persistence**: Database and storage services
- **security**: Security infrastructure (secrets, certificates)

## Naming Conventions

- Application names in ArgoCD: `<namespace>-<app-name>`
- Namespaces match the directory name under `apps/namespaces/`
- Encrypted files use `.sops.yaml` extension
- Resource manifests go in `resources/` subdirectory

## Key Files

- **kustomization.yaml**: Required in every app directory, defines either Helm charts or raw resources
- **values.yaml**: Helm chart values (plain text)
- **values.sops.yaml**: Encrypted Helm chart values (SOPS-encrypted)
- **.sops.yaml**: Age encryption configuration at repository root

## ArgoCD Discovery

The ApplicationSet automatically discovers any directory matching `apps/namespaces/*/*` and creates an ArgoCD Application for it. No manual registration required.
