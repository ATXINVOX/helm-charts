# ATXINVOX Microservices Helm Charts

Individual Helm charts for deploying ATXINVOX microservices using the [invox-service-deploy](https://github.com/ATXINVOX/invox-service-deploy) library chart.

## Available Charts

- **auth-service** - Authentication and authorization service
- **file-metadata-service** - File metadata management service  
- **signup-service** - User registration service
- **storage-service** - File storage service

## Quick Start

Each service can be deployed independently:

```bash
# Install auth-service
helm dependency update auth-service/
helm install my-auth-service auth-service/

# Install file-metadata-service
helm dependency update file-metadata-service/
helm install my-file-metadata file-metadata-service/

# Install signup-service
helm dependency update signup-service/
helm install my-signup signup-service/

# Install storage-service
helm dependency update storage-service/
helm install my-storage storage-service/
```

## Configuration

Each service uses the standardized configuration from the library chart. See individual `values.yaml` files for service-specific configurations.

### Common Configuration

All services support:
- GHCR image configuration
- Health check endpoints (`/health`)
- Environment variables from ConfigMaps/Secrets
- Resource limits and autoscaling
- Ingress configuration

### Example: Enable Ingress for Auth Service

```yaml
# auth-service-values.yaml
ingress:
  enabled: true
  hosts:
    - host: auth.your-domain.com
      paths:
        - path: /
          pathType: Prefix
```

```bash
helm install my-auth auth-service/ -f auth-service-values.yaml
```

## Dependencies

All charts depend on:
- [ATXINVOX/invox-service-deploy](https://github.com/ATXINVOX/invox-service-deploy) library chart
- GHCR authentication for pulling images
- Kubernetes 1.19+