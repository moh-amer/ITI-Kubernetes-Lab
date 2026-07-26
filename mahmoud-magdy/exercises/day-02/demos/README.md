# Guided demos — Kubernetes Volumes

Follow these demos step by step on **KillerKoda** or **single-node k3s**. Each folder has a `README.md` and (where needed) YAML you can apply.

All objects are created in the **`default`** namespace (no `namespace:` in YAML, no `-n` flags).

| # | Demo | What you learn |
|---|------|----------------|
| 01 | [Docker named volume](01-docker-named-volume/) | Writable layer dies; mounts persist |
| 02 | [emptyDir](02-emptydir/) | Survives container restart, not Pod delete |
| 03 | [hostPath](03-hostpath/) | Node disk; fine on one node |
| 04 | [ConfigMap volume](04-configmap-volume/) | Config as files, no image rebuild |
| 04 · extra | [ConfigMap from file](04-configmap-volume/11-configmap-from-file/) | `kubectl create cm --from-file` + mount |
| 05 | [Secret volume](05-secret-volume/) | Credentials as files |
| 05.5 | [Static PV + PVC](05.5-static-pv-pvc/) | Bind without a StorageClass |
| 06 | [PVC + local-path](06-pvc-local-path/) | Claim outlives the Pod |
| 07 | [Sidecar share](07-sidecar-shared-volume/) | Same volume, two containers |
| 09 | [Custom StorageClass](09-custom-storageclass/) | Create a class and set it default |
| 10 | [Volume resize](10-volume-resize/) | Patch PVC larger (`allowVolumeExpansion`) |
| 12 | [PV binding rules](12-pv-binding-rules/) | 10Gi vs 12Gi PVC; two 5Gi PVCs |

## Setup (once)

```bash
kubectl get nodes
kubectl get sc
kubectl config current-context
# work in default (usual unless you changed context)
```

**Important for demos 09–10:** always restore StorageClass `local-path` as `(default)` when you finish.
