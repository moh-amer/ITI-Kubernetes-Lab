# Lab 01 — emptyDir

## Scenario

You need scratch space inside a Pod for temporary files. Prove what survives a container restart vs a Pod delete.

## Requirements

### Pod `scratch-lab`

| Field | Value |
|-------|-------|
| Image | `busybox:1.36` |
| Keep running | `sleep 3600` (or equivalent) |
| Volume | `emptyDir` named `scratch` |
| Mount | `/data` |

## Tasks

1. Apply the Pod. Write `hello` into `/data/msg.txt`.
2. Kill the main process (`kill 1` via `kubectl exec`) and wait until the Pod is Ready again.
3. Confirm `/data/msg.txt` still exists.
4. Delete the Pod, recreate it from the same YAML, and confirm the file is **gone**.

## Deliverables

- Pod YAML
- Short note (2–3 lines): what emptyDir keeps and what it does not

## Verification

- [ ] Pod Running
- [ ] File survives container restart
- [ ] File does not survive Pod delete
