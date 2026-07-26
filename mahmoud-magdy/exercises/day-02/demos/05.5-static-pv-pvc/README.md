# Demo 08 — Static PV + PVC (no StorageClass)

**Goal:** Pre-create a `PersistentVolume`, claim it with a PVC that has `storageClassName: ""`, and mount it. No dynamic provisioner involved.

## Files

- [`pv.yaml`](pv.yaml) — cluster-scoped PV (`hostPath`)
- [`pvc-pod.yaml`](pvc-pod.yaml) — PVC + Pod

## Steps

```bash
kubectl apply -f pv.yaml
kubectl get pv static-demo-pv
# STATUS = Available

kubectl apply -f pvc-pod.yaml
kubectl wait --for=condition=Ready pod/static-demo --timeout=90s

kubectl get pvc static-demo-pvc
# STATUS = Bound  VOLUME = static-demo-pv

kubectl get pv static-demo-pv
# STATUS = Bound  CLAIM = default/static-demo-pvc

kubectl exec static-demo -- sh -c 'echo static-ok > /data/note.txt && cat /data/note.txt'
```

## Why `storageClassName: ""`?

If you omit it, the **default** StorageClass (e.g. `local-path`) tries to create a new volume dynamically, and your static PV is ignored.

## Cleanup

```bash
kubectl delete -f pvc-pod.yaml --wait=true
kubectl delete -f pv.yaml
# PV reclaim is Retain — remove node data if you want:
# kubectl run tmp --rm -it --restart=Never --image=busybox:1.36 \
#   --overrides='{"spec":{"containers":[{"name":"c","image":"busybox:1.36","command":["rm","-rf","/t/static-demo-pv"],"volumeMounts":[{"name":"t","mountPath":"/t"}]}],"volumes":[{"name":"t","hostPath":{"path":"/tmp"}}]}}'
```

## Takeaway

Static = admin creates the PV. Dynamic = you create only a PVC and a StorageClass provisioner creates the PV.
