# Warehouse Inventory GitOps Repository

This repository contains OpenChoreo GitOps manifests for the warehouse inventory demo.

## Structure

```
warehouse-inventory-gitops/
├── projects/
│   └── default/
│       └── project.yaml           # Project definition
├── environments/
│   └── development/
│       └── environment.yaml       # Environment definition
├── pipelines/
│   └── simple-pipeline/
│       └── pipeline.yaml          # Deployment pipeline
└── components/
    ├── inventory-api-gitops/
    │   └── component.yaml         # API component (GitOps workflow adds releases here)
    └── inventory-dashboard-gitops/
        └── component.yaml         # Dashboard component (GitOps workflow adds releases here)
```

## How It Works

1. **ComponentWorkflowRun** triggers a build in OpenChoreo
2. Workflow builds the image and pushes to registry
3. Workflow creates a **Pull Request** in this repo with:
   - `Workload` manifest
   - `ComponentRelease` manifest
   - `ReleaseBinding` manifest
4. You review and merge the PR
5. OpenChoreo syncs from this repo and deploys

## Components

| Component | Description |
|-----------|-------------|
| `inventory-api-gitops` | Go backend API (port 9090) |
| `inventory-dashboard-gitops` | Next.js frontend (port 3000) |

## Triggering Deployments

From the source repository, run:

```bash
# Trigger API build
kubectl apply -f demo/gitops/inventory-api-gitops-run.yaml

# Trigger Dashboard build
kubectl apply -f demo/gitops/inventory-dashboard-gitops-run.yaml
```

## Related

- Source Repository: https://github.com/LakshanSS/warehouse-inventory-demo
