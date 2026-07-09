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

## Étape 7 — Rolling update v1 > v2

[front bleu](screenshots/etape_6_front.png)
[front orange](screenshots/etape_7_new_ui.png)

## Étape 8 — Déploiement raté & rollback

- Le nouveau pod reste bloqué en `ImagePullBackOff`, ne devient jamais Ready.
[erreur](screenshots/etape_8_wrong_image.png)
- kubectl rollout status deployment/frontend` reste en attente.
- Sur http://localhost:8080, on voit toujours la v2 fonctionnelle.
    les 2 anciens pods restent en service (`maxUnavailable: 0` interdit de descendre sous le nombre de répliques disponibles). (La prod n'est pas cassée)

```bash
kubectl rollout undo deployment/frontend
kubectl rollout status deployment/frontend
```

`rollout undo` est le plus rapide et le plus sûr — Kubernetes rebascule immédiatement vers la révision précédente (v2.0) déjà connue, sans dépendre de l'état du fichier local. On remet ensuite `deployment-front.yaml` sur `:2.0` pour que le Git reflète l'état réel du cluster.

[plus d'erreur](screenshots/etape_8_no_more_errors.png)

## Étape 9 — Tester le Secret avec curl

[curls](screenshots/etape_9.png)