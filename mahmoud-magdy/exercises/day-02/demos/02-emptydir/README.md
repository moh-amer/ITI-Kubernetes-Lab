# Demo 02 — emptyDir

**Goal:** A file survives a container restart, but disappears when the Pod is deleted.

Manifest: [`pod.yaml`](pod.yaml)

## Steps

```bash
kubectl apply -f pod.yaml
kubectl wait --for=condition=Ready pod/emptydir-demo --timeout=60s

kubectl exec emptydir-demo -- sh -c 'echo hi > /data/note.txt && cat /data/note.txt'

# Kill PID 1 → kubelet restarts the container; emptyDir remains
kubectl exec emptydir-demo -- kill 1 || true
sleep 3
kubectl wait --for=condition=Ready pod/emptydir-demo --timeout=60s
kubectl exec emptydir-demo -- cat /data/note.txt
# → hi

# Delete the Pod → emptyDir is gone
kubectl delete pod emptydir-demo
kubectl apply -f pod.yaml
kubectl wait --for=condition=Ready pod/emptydir-demo --timeout=60s
kubectl exec emptydir-demo -- cat /data/note.txt
# → No such file
```

## Cleanup

```bash
kubectl delete -f pod.yaml --ignore-not-found
```

## Takeaway

`emptyDir` is Pod scratch space — good for caches and sharing between containers in the same Pod. Not for databases.
