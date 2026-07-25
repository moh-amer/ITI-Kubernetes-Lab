# Demo 06 — PVC + StorageClass (local-path)

**Goal:** Dynamic provisioning; data survives Pod delete. Deleting the PVC may wipe the disk (reclaim `Delete`).

Manifest: [`pvc-pod.yaml`](pvc-pod.yaml)

## Steps

```bash
kubectl get sc
# k3s: local-path (default)

kubectl apply -f pvc-pod.yaml
# local-path uses WaitForFirstConsumer: PVC binds after the Pod is scheduled.
# Wait for the Pod (not kubectl wait --for=condition=Bound on the PVC).
kubectl wait --for=condition=Ready pod/pvc-demo --timeout=120s
kubectl get pvc data-pvc
# STATUS should be Bound
kubectl exec pvc-demo -- sh -c 'echo durable > /data/note.txt'

kubectl get pv
kubectl delete pod pvc-demo
# re-apply (PVC already exists — that is fine)
kubectl apply -f pvc-pod.yaml
kubectl wait --for=condition=Ready pod/pvc-demo --timeout=90s
kubectl exec pvc-demo -- cat /data/note.txt
# → durable
```

## Optional — reclaim Delete

```bash
kubectl delete pod pvc-demo
kubectl delete pvc data-pvc
kubectl get pv
# with local-path, the PV usually disappears too
```

## If PVC stays Pending

```bash
kubectl describe pvc data-pvc
# usual causes: no default StorageClass, wrong accessMode (RWX), provisioner down
```

## Takeaway

The app asks for a PVC. The StorageClass provisioner creates the PV. On k3s that is `local-path` — good for one node, not multi-node HA storage.
