# Demo 11 — ConfigMap from a file, mounted as a volume

**Goal:** Create a ConfigMap with `kubectl create configmap --from-file`, then mount it into a Pod so each file becomes a path under the mount.

## Steps

### 1) Create local config files

```bash
mkdir -p /tmp/cm-from-file && cd /tmp/cm-from-file

cat > app.conf <<'EOF'
color=blue
debug=true
course=ITI Volumes
EOF

cat > welcome.txt <<'EOF'
Hello from --from-file
EOF

ls -l
```

### 2) Create the ConfigMap from the directory (or a single file)

```bash
kubectl create configmap app-files \
  --from-file=app.conf \
  --from-file=welcome.txt
# equivalent from a directory:
# kubectl create configmap app-files --from-file=/tmp/cm-from-file

kubectl get cm app-files -o yaml
```

### 3) Mount it

```bash
kubectl apply -f pod.yaml
kubectl wait --for=condition=Ready pod/cm-from-file --timeout=90s

kubectl exec cm-from-file -- ls -l /etc/config
kubectl exec cm-from-file -- cat /etc/config/app.conf
kubectl exec cm-from-file -- cat /etc/config/welcome.txt
```

Each ConfigMap **key** (filename) becomes a **file** in the mount path.

## Cleanup

```bash
kubectl delete -f pod.yaml --ignore-not-found
kubectl delete cm app-files --ignore-not-found
rm -rf /tmp/cm-from-file
```

## Takeaway

`--from-file` is the fastest way to load real config files into a ConfigMap. Mounting the CM exposes those files to the container without baking them into the image.
