# Lab 04 — Secret as a volume

## Scenario

An app expects credentials as **files**, not environment variables.

## Requirements

### Secret `api-creds`

| Key | Value |
|-----|-------|
| `token` | `iti-token-42` |
| `user` | `student` |

Use `stringData` or `kubectl create secret generic`.

### Pod `secret-files`

| Field | Value |
|-------|-------|
| Image | `busybox:1.36` |
| Keep running | yes |
| Mount Secret | `/etc/api` **readOnly** |
| Optional | `defaultMode: 0400` |

## Tasks

1. Apply Secret + Pod.
2. List `/etc/api` and show both file contents with `kubectl exec`.
3. Confirm the Pod YAML does **not** hard-code the token as a plain env `value:`.

## Deliverables

- YAML manifests

## Verification

- [ ] Both keys exist as files
- [ ] Mount is read-only
- [ ] Token value is correct
