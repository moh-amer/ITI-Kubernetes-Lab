# Lab 07 — Challenge (combine)

## Scenario

Deploy a tiny “notes” app stack in the `default` namespace using volumes for config, secrets, and durable data.

## Requirements

### 1. ConfigMap `notes-config`

| Key | Value |
|-----|-------|
| `APP_TITLE` | `ITI Notes` |
| `welcome.html` | HTML page whose `<title>` or body includes `ITI Notes` |

### 2. Secret `notes-secret`

| Key | Value |
|-----|-------|
| `admin-password` | choose any password |

### 3. PVC `notes-data`

- `ReadWriteOnce`, `1Gi`, default StorageClass

### 4. Pod `notes-app` (or Deployment with **1** replica)

Containers:

**A. `web` (nginx:1.27)**

- Mount ConfigMap key `welcome.html` at `/usr/share/nginx/html/index.html` using **`subPath`** (do not wipe the whole html dir if you can help it — `subPath` is required for full marks).
- Mount PVC at `/usr/share/nginx/html/data` (writable notes dir).

**B. `agent` (busybox:1.36) — sidecar**

- Mount the **same PVC** at `/data`.
- Loop: every 10s append an ISO-like timestamp line to `/data/heartbeat.log`.

**Also:**

- Mount the Secret read-only at `/etc/notes-secret` on the `web` container (files must be visible with `ls`).

## Acceptance tests

```bash
kubectl get cm,secret,pvc,pod 
kubectl exec notes-app -c web -- cat /usr/share/nginx/html/index.html
kubectl exec notes-app -c web -- ls /etc/notes-secret
kubectl exec notes-app -c agent -- cat /data/heartbeat.log
# delete the pod (not the PVC), recreate, heartbeat.log still grows / still exists
```

## Rubric (40 pts)

| Area | Pts |
|------|-----|
| ConfigMap + subPath mount | 8 |
| Secret volume on web | 6 |
| PVC Bound + shared by both containers | 10 |
| Sidecar writing heartbeat | 8 |
| Data survives Pod recreate | 8 |

## Deliverables

- All YAML in a folder named with your name
- Be ready to demo the acceptance commands
