# Lab 13 — ConfigMap and Deployment

## Scenario

Application settings live in a ConfigMap. A Deployment runs a demo app that reads those settings from the environment.

## Requirements

### ConfigMap `web-config`

| Key | Value |
|-----|-------|
| `PAGE_TITLE` | `ITI Kubernetes Lab` |
| `ENVIRONMENT` | `dev` |

### Deployment `web-config-demo`

| Field | Value |
|-------|-------|
| Replicas | `1` |
| Image | `busybox:latest` |
| Config | Inject all ConfigMap keys as **environment variables** |
| Behavior | Every 10 seconds, print `PAGE_TITLE` and `ENVIRONMENT` to stdout |

## Deliverables

- YAML manifest(s)

## Verification checklist

- [ ] ConfigMap exists with both keys
- [ ] Deployment pod is `Running`
- [ ] Logs show lines like `ITI Kubernetes Lab` and `dev`
- [ ] No volumes used — config comes from env vars only

## Bonus (optional)

Edit the ConfigMap, restart the Deployment, and show the new values in the logs.
