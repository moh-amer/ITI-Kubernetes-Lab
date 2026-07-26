# Demo 04 — ConfigMap as a volume

**Goal:** Serve HTML from a ConfigMap — no image rebuild.

Manifest: [`nginx-cm.yaml`](nginx-cm.yaml)

## Steps

```bash
kubectl apply -f nginx-cm.yaml
kubectl wait --for=condition=Ready pod/nginx-cm --timeout=90s

kubectl exec nginx-cm -- cat /usr/share/nginx/html/index.html

kubectl port-forward pod/nginx-cm 8080:80
# in another terminal: curl -s localhost:8080
```

## Cleanup

```bash
kubectl delete -f nginx-cm.yaml
```

## Takeaway

Mounting a ConfigMap over a directory **replaces** that directory’s contents with the ConfigMap keys. Need one file only? Use `subPath`.
