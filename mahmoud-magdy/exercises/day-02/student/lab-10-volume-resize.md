# Lab 10 — Request a PVC resize

## Scenario

Create an expandable StorageClass, a 1Gi PVC, then patch it to 2Gi. Document what your cluster actually does.

## Requirements

### StorageClass `student-expand`

| Field | Value |
|-------|-------|
| provisioner | `rancher.io/local-path` |
| allowVolumeExpansion | `true` |
| volumeBindingMode | `WaitForFirstConsumer` |

### PVC `resize-lab-pvc` + Pod `resize-lab`

- Start at `1Gi`, class `student-expand`
- Mount at `/data`

### Resize

```bash
kubectl patch pvc resize-lab-pvc -p \
  '{"spec":{"resources":{"requests":{"storage":"2Gi"}}}}'
```

Record:

1. `kubectl get pvc resize-lab-pvc` (capacity / conditions)
2. `kubectl describe pvc resize-lab-pvc` (events)
3. Whether `df -h /data` grew (restart Pod if you see `FileSystemResizePending`)

## Verification

- [ ] StorageClass has `allowVolumeExpansion: true`
- [ ] You attempted the patch to `2Gi`
- [ ] Written notes: **expanded successfully** OR **not supported / why** (both are acceptable)

## Note

You cannot shrink a PVC. On k3s `local-path`, the patch often updates **requests** to `2Gi` while **capacity** stays `1Gi` (`ExternalExpanding`). That is an acceptable lab outcome — write it down. Cloud CSI drivers are where resize usually completes.
