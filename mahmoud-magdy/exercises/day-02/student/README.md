# Student exercises — Kubernetes Volumes

Environment: **KillerKoda** or **single-node k3s**. Official images only (`busybox`, `nginx`).

All work is in the **`default`** namespace (do not set `metadata.namespace` in your YAML).

## Setup (once)

```bash
kubectl get nodes
kubectl get sc
kubectl config current-context
```

## Labs

| # | Lab | Focus | Time |
|---|-----|-------|------|
| 01 | [emptyDir](lab-01-emptydir.md) | Scratch volume lifecycle | 15 min |
| 02 | [hostPath](lab-02-hostpath.md) | Node path mount | 15 min |
| 03 | [ConfigMap volume](lab-03-configmap-volume.md) | Config as files | 15 min |
| 04 | [Secret volume](lab-04-secret-volume.md) | Creds as files | 15 min |
| 05 | [PVC](lab-05-pvc.md) | Durable claim | 20 min |
| 06 | [Sidecar](lab-06-sidecar.md) | Shared emptyDir | 15 min |
| 07 | [Challenge](lab-07-challenge.md) | Combine everything | 30–40 min |
| 08 | [Static PV + PVC](lab-08-static-pv-pvc.md) | No StorageClass | 20 min |
| 09 | [Custom StorageClass](lab-09-custom-storageclass.md) | Create + set default | 20 min |
| 10 | [Volume resize](lab-10-volume-resize.md) | Expand PVC | 15 min |
| 11 | [ConfigMap from file](lab-11-configmap-from-file.md) | `--from-file` mount | 15 min |
| 12 | [PV binding rules](lab-12-pv-binding-rules.md) | Size match + one PV one PVC | 15 min |

## Rules

1. Write YAML files (declarative). Imperative `kubectl create` is OK for Secrets/ConfigMaps if you prefer.
2. Be ready to show `kubectl get` / `describe` / `exec` proof.
3. Clean up when done (careful — deletes PVCs too):

```bash
kubectl delete pod,cm,secret,pvc --all
kubectl delete pv -l type=local --ignore-not-found
# or delete resources by name from your lab
```

## Hints (allowed)

- Guided demos (with YAML): [`../demos/`](../demos/)
- `kubectl explain pod.spec.volumes`
- `kubectl explain pod.spec.containers.volumeMounts`
- `kubectl describe pvc` when a claim is Pending
