# Demo 10 — PVC resize (volume expansion)

**Goal:** Grow a PVC from `1Gi` → `2Gi` using a StorageClass with `allowVolumeExpansion: true`.

> **Honest lab note:** stock k3s `local-path` has `allowVolumeExpansion: false`. This demo uses a second class (`iti-expandable`). Whether the **filesystem** actually grows depends on your local-path-provisioner version. You still learn the API either way.

## Files

- [`storageclass.yaml`](storageclass.yaml)
- [`pvc-pod.yaml`](pvc-pod.yaml)

## Steps

### 1) Create expandable class + PVC + Pod

```bash
kubectl apply -f storageclass.yaml
kubectl apply -f pvc-pod.yaml
kubectl wait --for=condition=Ready pod/resize-demo --timeout=120s

kubectl get pvc resize-pvc
# CAPACITY / REQUESTS = 1Gi
kubectl exec resize-demo -- df -h /data
```

### 2) Request a larger size

```bash
kubectl patch pvc resize-pvc --type=merge -p \
  '{"spec":{"resources":{"requests":{"storage":"2Gi"}}}}'

kubectl get pvc resize-pvc
# compare REQUESTS (spec) vs CAPACITY (status)
kubectl describe pvc resize-pvc | sed -n '/Events/,$p'
```

### 3) Interpret the result (k3s / local-path)

On this course cluster you will typically see:

| Field | After patch |
|-------|-------------|
| `spec.resources.requests.storage` | `2Gi` (API accepted the ask) |
| `status.capacity.storage` | stays `1Gi` |
| Events | `ExternalExpanding` / waiting for external controller |

That means: **the PVC API allows the resize request**, but **local-path does not finish expanding** the volume. The teaching point still stands — cloud CSI (EBS, Azure Disk, …) with `allowVolumeExpansion: true` is where capacity actually grows.

**If your cluster *does* expand** (CAPACITY becomes `2Gi`):

```bash
# if you see FileSystemResizePending, restart the Pod once
kubectl delete pod resize-demo
kubectl apply -f pvc-pod.yaml
kubectl wait --for=condition=Ready pod/resize-demo --timeout=120s
kubectl exec resize-demo -- df -h /data
```

## Cleanup

```bash
kubectl delete -f pvc-pod.yaml --wait=true
kubectl delete -f storageclass.yaml
```

## Takeaway

Resize = patch the PVC request upward. You cannot shrink a PVC in core Kubernetes. Need an expandable StorageClass + a provisioner that supports expansion.
