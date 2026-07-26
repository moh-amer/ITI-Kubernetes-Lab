# Lab 05 — PersistentVolumeClaim

## Scenario

You need data that survives deleting the Pod. Use the cluster default StorageClass (on k3s: `local-path`).

## Requirements

### PVC `work-pvc`

| Field | Value |
|-------|-------|
| accessModes | `ReadWriteOnce` |
| storage request | `1Gi` |
| storageClassName | omit if a default exists; else set to your cluster’s default |

### Pod `pvc-lab`

| Field | Value |
|-------|-------|
| Image | `busybox:1.36` |
| Keep running | yes |
| Volume | PVC `work-pvc` |
| Mount | `/data` |

## Tasks

1. Apply PVC + Pod. Wait until the Pod is Ready (`kubectl wait --for=condition=Ready pod/pvc-lab`). On k3s (`WaitForFirstConsumer`), the PVC becomes `Bound` after the Pod is scheduled — then check with `kubectl get pvc`.
2. Write `survived` to `/data/state.txt`.
3. Delete **only** the Pod. Re-apply the Pod (keep the PVC).
4. Confirm `/data/state.txt` still says `survived`.
5. Run `kubectl get pv` and note the auto-created PV name.

## Deliverables

- YAML (PVC + Pod)
- Screenshot or paste of `kubectl get pvc,pv`

## Verification

- [ ] PVC Bound
- [ ] Data survives Pod delete
- [ ] You can name your StorageClass / default SC

## Troubleshooting

If PVC is Pending: `kubectl describe pvc work-pvc` — check StorageClass and access mode (do **not** use `ReadWriteMany` on local-path).
