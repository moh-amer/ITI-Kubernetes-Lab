# Lab 07 — Nginx Deployment and NodePort Service

## Scenario

Expose a scalable web app outside the cluster using a Deployment and a NodePort Service.

## Requirements

**Deployment** `nginx-deployment`:

| Field | Value |
|-------|-------|
| Replicas | `3` |
| Container name | `nginx-container` |
| Image | `nginx:latest` |

**Service** `nginx-service`:

| Field | Value |
|-------|-------|
| Type | `NodePort` |
| Port | `80` → target port `80` |
| nodePort | `30011` |
| Selector | Must match Deployment pod labels |

## Deliverables

- YAML manifest(s)
- Three running pods
- Service exposing the app on node port `30011`

## Verification checklist

- [ ] Deployment shows `3/3` ready replicas
- [ ] Service type is `NodePort` with port `30011`
- [ ] You can reach nginx from outside the cluster (Minikube: `minikube service nginx-service --url`, or `curl` to node IP)
