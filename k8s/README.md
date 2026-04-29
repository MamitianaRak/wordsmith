Kubernetes manifests for wordsmith

Included files:

- `db-deployment.yaml` — Deployment + ClusterIP Service for the DB (port 5432)
- `words-deployment.yaml` — Deployment + ClusterIP Service for the words service (port 8080)
- `web-deployment.yaml` — Deployment + NodePort Service for the web UI (port 80)

Quick deploy (on a cluster with kubectl configured):

```bash
kubectl apply -f k8s/db-deployment.yaml
kubectl apply -f k8s/words-deployment.yaml
kubectl apply -f k8s/web-deployment.yaml
```

Find web NodePort and connect from outside (example):

```bash
kubectl get svc wordsmith-web -o yaml
# or
kubectl get svc wordsmith-web
```

To get a usable URL on a single-node cluster (minikube):

```bash
minikube service wordsmith-web --url
```

Notes & assumptions:

- Images are pulled from the registry: `jpetazzo/wordsmith-db:latest`, `jpetazzo/wordsmith-words:latest`, `jpetazzo/wordsmith-web:latest`.
- I set simple environment variables so the `words` service can reach the `db` service and `web` can reach `words` via Kubernetes DNS (`wordsmith-db`, `wordsmith-words`). If your services expect different env var names, tell me and I will adjust.
- For production you should add resource requests/limits, readiness/liveness probes, persistent volume for the DB, and configure secrets for DB credentials.
