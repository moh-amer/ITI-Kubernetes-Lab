# Lab 09 — Custom StorageClass as default

## Scenario

Create StorageClass `student-local`, make it the **default**, provision a PVC that uses it, then **restore** `local-path` as the default.

## Requirements

### StorageClass `student-local`

| Field | Value |
|-------|-------|
| provisioner | `rancher.io/local-path` |
| volumeBindingMode | `WaitForFirstConsumer` |
| reclaimPolicy | `Delete` |
| allowVolumeExpansion | `false` |

### Make it default

1. Remove default annotation from `local-path`
2. Set `storageclass.kubernetes.io/is-default-class=true` on `student-local`
3. Show `kubectl get sc` with `(default)` on `student-local`

### PVC `sc-lab-pvc` + Pod `sc-lab`

- PVC uses `storageClassName: student-local`, `1Gi`, `ReadWriteOnce`
- Pod mounts at `/data` and writes a file

## Verification

- [ ] `kubectl get sc` shows `student-local (default)` during the lab
- [ ] PVC Bound with `STORAGECLASS=student-local`
- [ ] **After cleanup**, `local-path` is `(default)` again

## Important

Leaving the wrong default breaks the rest of the class. Restore `local-path` before you leave.
