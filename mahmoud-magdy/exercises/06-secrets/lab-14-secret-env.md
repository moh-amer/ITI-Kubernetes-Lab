# Lab 14 — Secret and Pod

## Scenario

Store a license key securely in a Secret and pass it to a running pod as an environment variable.

## Requirements

### Secret `app-license`

| Key | Value |
|-----|-------|
| `license-key` | `5ecur3` |

### Pod `secret-demo`

| Field | Value |
|-------|-------|
| Image | `busybox:latest` |
| Command | Keep the container running long enough to inspect it |
| Config | Expose the secret value as env var `LICENSE_KEY` using `secretKeyRef` |

**Do not use volume mounts.** Use environment variables only.

## Deliverables

- YAML manifest(s), or `kubectl create secret` plus pod YAML

## Verification checklist

- [ ] Secret `app-license` exists
- [ ] Pod is `Running`
- [ ] Inside the container, `LICENSE_KEY` equals `5ecur3`
- [ ] Secret value is not hard-coded as plain text in the pod spec (use `valueFrom`)

## Hint

You may create the Secret with `kubectl create secret generic ...` or with `stringData` in YAML.
