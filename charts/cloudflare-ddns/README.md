# Cloudflare DDNS Helm Chart

This Helm chart deploys a Cloudflare DDNS service that automatically updates your DNS records with your current IP address.
Source: https://github.com/favonia/cloudflare-ddns

## Prerequisites

- Kubernetes 1.16+
- Helm 3.0+
- Cloudflare API Token with Zone:DNS:Edit permissions

## Installation

1. Add the repository:
```bash
helm repo add askosyrskiy https://askosyrskiy.github.io/helm-charts
helm repo update
```

2. Create a values file (e.g., `my-values.yaml`):
```yaml
cloudflareApiToken: "your-cloudflare-api-token"
domains: "your.domain.com,another.domain.com"
proxied: "true"  # Whether to proxy the domain through Cloudflare
ip6Provider: "none"  # Set to "none" to disable IPv6 updates
```

3. Install the chart:
```bash
helm install cloudflare-ddns askosyrskiy/cloudflare-ddns -f my-values.yaml
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `namespace` | Namespace to deploy to | `cloudflare-ddns` |
| `image.repository` | Image repository | `favonia/cloudflare-ddns` |
| `image.tag` | Image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `cloudflareApiToken` | Cloudflare API Token | `""` |
| `domains` | Domains to update (comma-separated) | `""` |
| `proxied` | Whether to proxy through Cloudflare | `"true"` |
| `ip6Provider` | IPv6 address provider | `"none"` |
| `resources.limits.cpu` | CPU limit | `250m` |
| `resources.limits.memory` | Memory limit | `50Mi` |
| `resources.requests.cpu` | CPU request | `100m` |
| `resources.requests.memory` | Memory request | `30Mi` |

## Security

This chart implements several security best practices:
- Non-root container execution
- Read-only root filesystem
- Dropped capabilities
- Resource limits
- SeccompProfile set to RuntimeDefault

## Updating

To update the configuration:

```bash
helm upgrade cloudflare-ddns askosyrskiy/cloudflare-ddns -f my-values.yaml
```

## Uninstalling

To uninstall/delete the deployment:

```bash
helm uninstall cloudflare-ddns
```