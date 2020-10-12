# nfs-pvc

Helper helm chart for mounting pre-created NFS directories as PVC.

How to use from ArgoCD:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-storage
spec:
  project: default

  source:
    repoURL: https://github.com/mdvorak-cloud/nfs-pvc.git
    targetRevision: HEAD
    path: .
    helm:
      parameters:
        - name: name
          value: myname
        - name: namespace
          value: myns
        - name: server
          value: nfs.example.com
        - name: share
          value: /kubernetes
        - name: storage
          value: 10Mi
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
