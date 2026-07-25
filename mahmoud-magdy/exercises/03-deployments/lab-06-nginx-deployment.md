# Lab 06 — Nginx Deployment

## Scenario

Use a Deployment to manage an nginx application (Deployments are preferred over ReplicaSets for rolling updates).

## Requirements

Create a Deployment named `nginx`:

| Field | Value |
|-------|-------|
| Image | `nginx:latest` |
| Replicas | `1` (default is fine) |
| Labels | Use consistent labels on the Deployment and pod template |

## Deliverables

- YAML manifest
- Deployment with one running pod

## Verification checklist

- [ ] Deployment `nginx` exists
- [ ] At least one pod is `Running`
- [ ] Pod is owned/managed by the Deployment
