# nfs-pvc

Helper helm chart for mounting pre-created NFS directories as PVC.

How to use from ArgoCD:

<!--x-release-please-start-version-->

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: mystorage
spec:
  project: default

  source:
    repoURL: https://mdvorak-cloud.github.io/nfs-pvc
    chart: nfs-pvc
    targetRevision: 1.0.1
    helm:
      parameters:
        - name: server
          value: nfs.example.com
        - name: share
          value: /kubernetes
        - name: accessMode
          value: ReadWriteMany

  destination:
    server: https://kubernetes.default.svc
    namespace: myns

  syncPolicy:
    automated:
      prune: true
      selfHeal: false
    syncOptions:
      - CreateNamespace=true
```

<!--x-release-please-end-->
