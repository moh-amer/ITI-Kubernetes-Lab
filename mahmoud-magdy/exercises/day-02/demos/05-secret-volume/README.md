# Demo 05 — Secret as a volume

**Goal:** Credentials appear as files under `/etc/creds`, mounted read-only.

Manifest: [`secret-pod.yaml`](secret-pod.yaml)

## Steps

```bash
kubectl apply -f secret-pod.yaml
kubectl wait --for=condition=Ready pod/secret-vol --timeout=60s

kubectl exec secret-vol -- ls -l /etc/creds
kubectl exec secret-vol -- cat /etc/creds/username
kubectl exec secret-vol -- cat /etc/creds/password
```

## Cleanup

```bash
kubectl delete -f secret-pod.yaml
```

## Takeaway

base64 in etcd is obfuscation, not encryption. Prefer file mounts for secrets when the app supports them, and never commit real Secret YAML with production passwords to git.
