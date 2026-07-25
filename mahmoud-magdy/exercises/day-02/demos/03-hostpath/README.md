# Demo 03 — hostPath

**Goal:** Data lives on the **node** path; deleting the Pod does not erase it (single-node clusters).

Manifest: [`pod.yaml`](pod.yaml) — mounts `/tmp/k8s-hostpath-lab` with `DirectoryOrCreate`.

## Steps

```bash
kubectl apply -f pod.yaml
kubectl wait --for=condition=Ready pod/hostpath-demo --timeout=60s

kubectl exec hostpath-demo -- sh -c 'echo from-pod > /data/note.txt'

kubectl delete pod hostpath-demo
kubectl apply -f pod.yaml
kubectl wait --for=condition=Ready pod/hostpath-demo --timeout=60s
kubectl exec hostpath-demo -- cat /data/note.txt
# → from-pod

# Optional on a k3s VPS (SSH into the node):
# cat /tmp/k8s-hostpath-lab/note.txt
```

## Cleanup

```bash
kubectl delete pod hostpath-demo --ignore-not-found
# on the node, if you want: rm -rf /tmp/k8s-hostpath-lab
```

## Takeaway

On one node this looks like persistence. On multiple nodes the Pod might start elsewhere and the path can be empty — that is why real apps use a PVC.
