# Demo 09 — Create a StorageClass and make it default

**Goal:** Create your own StorageClass (`iti-local`), mark it as the cluster default, and provision a PVC that uses it. **Restore `local-path` as default when you finish.**

## Files

- [`storageclass.yaml`](storageclass.yaml)
- [`pvc-pod.yaml`](pvc-pod.yaml)

## Steps

### 1) See current defaults

```bash
kubectl get sc
# local-path should show (default)
```

### 2) Create your StorageClass

```bash
kubectl apply -f storageclass.yaml
kubectl get sc iti-local
```

### 3) Make `iti-local` the default

```bash
# remove default from local-path
kubectl annotate sc local-path \
  storageclass.kubernetes.io/is-default-class-

# set iti-local as default
kubectl annotate sc iti-local \
  storageclass.kubernetes.io/is-default-class=true --overwrite

kubectl get sc
# iti-local (default)
```

### 4) Use it (explicit name — clearest for demos)

```bash
kubectl apply -f pvc-pod.yaml
kubectl wait --for=condition=Ready pod/iti-sc-demo --timeout=120s
kubectl get pvc iti-sc-pvc
# STORAGECLASS = iti-local , STATUS = Bound

kubectl exec iti-sc-demo -- sh -c 'echo via-iti-local > /data/ok && cat /data/ok'
```

Optional: create a PVC **without** `storageClassName` while `iti-local` is default — it should pick `iti-local`.

## Cleanup (restore cluster default!)

```bash
kubectl delete -f pvc-pod.yaml --wait=true
kubectl delete -f storageclass.yaml

# put local-path back as default
kubectl annotate sc local-path \
  storageclass.kubernetes.io/is-default-class=true --overwrite

kubectl get sc
```

## Takeaway

A StorageClass is a recipe (provisioner + binding mode + reclaim). The annotation `storageclass.kubernetes.io/is-default-class=true` controls which class fills in when a PVC omits `storageClassName`.
