# Product Overview

This is a homelab Kubernetes infrastructure repository that manages a self-hosted cluster using GitOps principles. The cluster hosts various applications including:

- **Media Server**: Plex, Sonarr, Radarr, Prowlarr, Overseerr, SABnzbd
- **Automation**: n8n workflow automation
- **Databases**: PostgreSQL, NocoDB
- **Gaming**: Minecraft server
- **Monitoring**: Prometheus stack, Grafana, metrics-server
- **Networking**: Pi-hole DNS, MetalLB load balancer, ingress controllers (public and internal)
- **Security**: cert-manager, 1Password integration, external-secrets-operator
- **Storage**: Longhorn, NFS CSI driver

The infrastructure is deployed on a NixOS-based homelab cluster and uses ArgoCD for continuous deployment with automated sync and self-healing capabilities.
