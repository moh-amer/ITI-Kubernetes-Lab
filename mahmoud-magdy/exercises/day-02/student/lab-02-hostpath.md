# Lab 02 — hostPath

## Scenario

On a **single-node** cluster you mount a directory from the node into the Pod.

## Requirements

### Pod `hostpath-lab`

| Field | Value |
|-------|-------|
| Image | `busybox:1.36` |
| Keep running | yes |
| Volume type | `hostPath` |
| Node path | `/tmp/hostpath-lab` |
| hostPath type | `DirectoryOrCreate` |
| Mount | `/data` |

## Tasks

1. Apply the Pod. Write `node-disk` into `/data/note.txt`.
2. Delete the Pod and apply it again.
3. Confirm `/data/note.txt` still contains `node-disk`.

## Deliverables

- Pod YAML

## Verification

- [ ] File survives Pod delete + recreate
- [ ] You can explain why this is unsafe on a multi-node cluster

## Note

Do not use hostPath for database data in production apps — use a PVC.
