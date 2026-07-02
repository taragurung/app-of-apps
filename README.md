# ArgoCD App-of-Apps Demo (kind)

## What is "app of apps"?

Instead of manually creating one ArgoCD `Application` per workload, you create **one
root Application** whose job is to sync a folder of *other* `Application` manifests.
ArgoCD then creates those child Applications, and each child deploys real workloads.

```
root-app (Application)         --> watches  apps/
   ├── hello (Application)     --> watches  manifests/hello/   --> Deployment + Service
   └── nginx (Application)     --> watches  manifests/nginx/   --> Deployment + Service
```

You apply ONLY `root-app.yaml` by hand. Everything else appears automatically.

## Layout

```
root-app.yaml            # the ONE app you kubectl apply manually
apps/                    # child Application manifests (synced by root-app)
  hello-app.yaml
  nginx-app.yaml
manifests/               # actual Kubernetes resources (synced by child apps)
  hello/{deployment,service}.yaml
  nginx/{deployment,service}.yaml
```

## Steps — see chat for the full command walkthrough.
