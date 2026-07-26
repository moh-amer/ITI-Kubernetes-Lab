# Kubernetes Volumes — Lab Pack

Works on **KillerKoda** and **single-node k3s** (class VPS). No cloud disks required.

Everything runs in the **`default`** namespace — manifests do not set `metadata.namespace`.

## Folders

| Path | What | Answers included? |
|------|------|-------------------|
| [`demos/`](demos/) | Guided demos — follow along with YAML | Yes |
| [`student/`](student/) | Exercises to solve yourself | No |
| [`student-solutions/`](student-solutions/) | Exercise answers (instructor / self-check) | Yes |

## Suggested order

1. Work through [`demos/`](demos/) while watching the slides.
2. Complete [`student/`](student/) labs on your own.
3. Use [`student-solutions/`](student-solutions/) only after you have tried the exercise.

## Cluster check (first)

```bash
kubectl get nodes -o wide
kubectl get sc
kubectl config current-context
```

- **k3s:** expect StorageClass `local-path` marked `(default)`.
- **KillerKoda:** use whatever SC is `(default)`; omit `storageClassName` on PVCs or set it explicitly.
