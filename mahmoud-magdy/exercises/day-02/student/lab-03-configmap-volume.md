# Lab 03 — ConfigMap as a volume

## Scenario

Serve a custom homepage from nginx without building an image. The HTML lives in a ConfigMap.

## Requirements

### ConfigMap `site-html`

| Key | Value |
|-----|-------|
| `index.html` | Any valid HTML that includes the text `ITI Volumes` |

### Pod `nginx-site`

| Field | Value |
|-------|-------|
| Image | `nginx:1.27` |
| Mount ConfigMap | at `/usr/share/nginx/html` |

## Tasks

1. Create the ConfigMap and Pod.
2. `kubectl exec` and `cat` the mounted `index.html`.
3. Optional: `kubectl port-forward pod/nginx-site 8080:80` and curl it.

## Deliverables

- YAML (ConfigMap + Pod, one file or two)

## Verification

- [ ] Pod Running
- [ ] Mounted file contains `ITI Volumes`
- [ ] You understand that mounting over a directory replaces its contents
