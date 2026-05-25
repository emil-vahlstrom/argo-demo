# Argo CD demo repo!

## YAML-specification for basic nginx-app

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: nginx
spec:
  destination:
    namespace: default
    server: https://kubernetes.default.svc
  source:
    path: examples/nginx
    repoURL: https://github.com/emil-vahlstrom/argo-demo.git
    targetRevision: master
  sources: []
  project: default
  syncPolicy: {}
```

## YAML-specification for a standalone Application called 'backend'

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

## YAML-specification for a standalone Application called 'frontend'

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: frontend
spec:
  destination:
    namespace: default
    server: https://kubernetes.default.svc
  source:
    path: examples/app-of-apps/charts/frontend
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