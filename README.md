# TD — Déploiement Kubernetes « Mini Todo »

## Étape 1 — Secret

```bash
kubectl create secret generic backend-secret \
  --from-literal=admin-token=s3cr3t-token-td
```

## Étape 2 — Configmap

```bash
kubectl apply -f manifests/configmap.yaml
```

## Étape 3 — Deployment backend

```bash
kubectl apply -f manifests/deployment-back.yaml
```
