# Argo CD demo repo!

## Application for standalone-backend

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: backend
spec:
  destination:
    namespace: default
    server: https://kubernetes.default.svc
  source:
    path: examples/app-of-apps/charts/backend
    repoURL: git@github.com:emil-vahlstrom/argo-demo.git
    targetRevision: master
    helm:
      valueFiles:
        - example-values.yaml
  sources: []
  project: default
  syncPolicy:
    automated:
      prune: false
      selfHeal: true
      enabled: true
```