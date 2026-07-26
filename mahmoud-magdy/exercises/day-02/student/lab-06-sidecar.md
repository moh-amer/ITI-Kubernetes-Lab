# Lab 06 — Sidecar with shared volume

## Scenario

One container writes a log file; another tails it. They share an `emptyDir`.

## Requirements

### Pod `pair-lab` — two containers

| Container | Role |
|-----------|------|
| `writer` | Append the date to `/var/log/app/out.txt` every 2 seconds |
| `reader` | `tail -F` the same file |

Both mount the same `emptyDir` at `/var/log/app`.

## Tasks

1. Apply the Pod.
2. Stream logs from the **reader** container (`kubectl logs ... -c reader -f`).
3. Show that `kubectl logs pair-lab` without `-c` is ambiguous / errors — explain why.

## Deliverables

- Pod YAML

## Verification

- [ ] Reader logs show updating timestamps
- [ ] You used `-c` correctly
