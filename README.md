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

## Étape 4 — Deployment frontend

```bash
kubectl apply -f manifests/deployment-front.yaml
```

## Étape 5 — Deployment frontend

```bash
kubectl apply -f manifests/service-back.yaml
kubectl apply -f manifests/service-front.yaml
```

## Étape 6 — Tester l'application

[TODOs dans le front](screenshots/etape_6_front.png)
[nom du pod backend retrouvé dans le terminal](screenshots/etape_6_front.png)