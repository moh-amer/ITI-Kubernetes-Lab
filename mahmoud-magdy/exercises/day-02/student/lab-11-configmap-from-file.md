# Lab 11 — ConfigMap `--from-file` as a volume

## Scenario

You have local config files. Load them into a ConfigMap with `kubectl create … --from-file` and mount them read-only.

## Requirements

### Create files on your machine (or KillerKoda terminal)

Create at least two files, for example:

- `nginx-extra.conf` (any short text)
- `banner.txt` containing the exact string `FROM-FILE-LAB`

### ConfigMap `files-cm`

Must be created with **`--from-file`** (not `--from-literal` for these keys).

```bash
kubectl create configmap files-cm \
  --from-file=nginx-extra.conf \
  --from-file=banner.txt \

```

### Pod `files-pod`

| Field | Value |
|-------|-------|
| Image | `busybox:1.36` |
| Mount | ConfigMap `files-cm` at `/etc/files` read-only |

## Verification

- [ ] `kubectl get cm files-cm -o yaml` shows both keys
- [ ] `ls /etc/files` inside the Pod lists both filenames
- [ ] `cat /etc/files/banner.txt` prints `FROM-FILE-LAB`
- [ ] You did **not** hard-code the file contents in the Pod YAML
