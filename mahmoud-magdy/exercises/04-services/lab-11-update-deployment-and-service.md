# Lab 11 — Update Deployment and Service

## Scenario

An existing nginx app needs more capacity, a new image, and a different external port — without deleting the resources.

## Part A — Create initial resources

Create these resources in `default` (or your lab namespace):

**Deployment** `nginx-deployment`:

| Field | Value |
|-------|-------|
| Replicas | `1` |
| Image | `nginx:1.19` |

**Service** `nginx-service`:

| Field | Value |
|-------|-------|
| Type | `NodePort` |
| nodePort | `30008` |
| Port | `80` |

### Part B — Update in place

Change the existing resources (do not delete and recreate):

| Resource | Change |
|----------|--------|
| Deployment | Replicas: `1` → `5` |
| Deployment | Image: `nginx:1.19` → `nginx:latest` |
| Service | nodePort: `30008` → `32165` |

## Deliverables

- Initial YAML
- Record of how you applied the updates (`kubectl edit`, patch, or updated YAML)

## Verification checklist

- [ ] Deployment shows `5/5` ready replicas
- [ ] Pods use image `nginx:latest`
- [ ] Service nodePort is `32165`
- [ ] Same Deployment and Service names as before (not recreated)
