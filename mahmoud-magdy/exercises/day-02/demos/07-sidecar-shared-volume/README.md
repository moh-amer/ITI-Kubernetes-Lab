# Demo 07 — Sidecar + shared emptyDir

**Goal:** Writer and reader share `/data`. Multi-container Pods need `kubectl logs -c`.

Manifest: [`pod-sidecar.yaml`](pod-sidecar.yaml)

## Steps

```bash
kubectl apply -f pod-sidecar.yaml
kubectl wait --for=condition=Ready pod/sidecar-demo --timeout=60s

kubectl logs sidecar-demo -c reader -f
# timestamps stream — Ctrl-C

kubectl logs sidecar-demo -c writer --tail=5
```

## Cleanup

```bash
kubectl delete -f pod-sidecar.yaml
```

## Takeaway

Same Pod, same volume name, two `volumeMounts`. That is the sidecar file-sharing pattern (log shippers, agents, sync helpers).
