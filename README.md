# Elasticsearch on Minikube

This repository deploys Elasticsearch on Minikube using the official Helm chart.

## Prerequisites

- Minikube running with sufficient resources:
  ```
  minikube start --memory=4096 --cpus=4
  ```
- Helm installed (https://helm.sh/docs/intro/install/)
- kubectl configured to use Minikube context

## Deploy Elasticsearch

```bash
helm repo add elastic https://helm.elastic.co
helm repo update
helm upgrade --install elasticsearch elastic/elasticsearch -n elasticsearch -f values.yaml --create-namespace
```

## Access Elasticsearch

```bash
kubectl port-forward svc/elasticsearch-master 9200 -n elasticsearch
curl http://localhost:9200
```

---

## CI/CD

On every push to `main`, GitHub Actions will lint the Helm chart and deploy Elasticsearch to Minikube automatically.
