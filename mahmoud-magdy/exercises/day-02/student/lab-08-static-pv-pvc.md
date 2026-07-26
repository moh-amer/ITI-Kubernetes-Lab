# Lab 08 — Static PV + PVC (no StorageClass)

## Scenario

An admin prepared a disk path on the node. You must claim it with a PVC that does **not** use dynamic provisioning.

## Requirements

### PersistentVolume `lab-static-pv` (cluster-scoped)

| Field | Value |
|-------|-------|
| capacity | `1Gi` |
| accessModes | `ReadWriteOnce` |
| reclaimPolicy | `Retain` |
| storageClassName | `""` (empty) |
| backend | `hostPath` at `/tmp/lab-static-pv` with `DirectoryOrCreate` |

### PersistentVolumeClaim `lab-static-pvc`

| Field | Value |
|-------|-------|
| accessModes | `ReadWriteOnce` |
| storage request | `1Gi` |
| storageClassName | `""` (empty — required) |
| volumeName | `lab-static-pv` |

### Pod `lab-static`

Mount the PVC at `/data`. Write `static-lab` into `/data/proof.txt`.

## Verification

- [ ] PV was `Available`, then `Bound` to your PVC
- [ ] PVC `Bound` to `lab-static-pv` (not a dynamic `pvc-…` name)
- [ ] File readable via `kubectl exec`

## Cleanup note

Delete Pod + PVC first, then the PV. With `Retain`, the PV may stay `Released` until you delete it.
