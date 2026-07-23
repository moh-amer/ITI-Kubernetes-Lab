# Lab 10 — Httpd deploy, update, and rollback

## Scenario

Practice a full lifecycle in an isolated namespace: deploy Apache, expose it, upgrade the image, then roll back.

## Requirements

### 1. Namespace

Create namespace `nautilus`.

### 2. Deployment `httpd-deploy` (in `nautilus`)

| Field | Value |
|-------|-------|
| Replicas | `3` |
| Container name | `httpd` |
| Image | `httpd:2.4.27` |
| Strategy | `RollingUpdate` with `maxSurge: 1`, `maxUnavailable: 2` |

### 3. Service `httpd-service` (in `nautilus`)

| Field | Value |
|-------|-------|
| Type | `NodePort` |
| nodePort | `30008` |
| Port | `80` → container port `80` |

### 4. Upgrade

Rolling update the Deployment to image `httpd:2.4.43`.

### 5. Rollback

Roll back to image `httpd:2.4.27`.

## Deliverables

- YAML for namespace, Deployment, and Service
- Record of update and rollback commands

## Verification checklist

- [ ] All resources are in namespace `nautilus`
- [ ] Service is reachable on node port `30008`
- [ ] After upgrade, pods briefly run `httpd:2.4.43`
- [ ] After rollback, pods run `httpd:2.4.27` again
- [ ] Deployment maintains 3 replicas throughout
