# Lab 16 — Ingress routing

## Scenario

Two web apps run behind one hostname. Route traffic by URL path using an Ingress resource.

## Prerequisite

```bash
minikube addons enable ingress
```

## Requirements

### Backend 1 — `/bar`

| Resource | Value |
|----------|-------|
| Deployment name | `web-bar` (your choice for labels) |
| Image | `nginx:latest` |
| Service name | `service1` |
| Service port | `80` |
| Custom response | Configure nginx to return something identifiable for `/bar` (custom default page, or default nginx page is OK if you can tell backends apart) |

### Backend 2 — `/foo`

| Resource | Value |
|----------|-------|
| Deployment name | `web-foo` |
| Image | `httpd:latest` |
| Service name | `service2` |
| Service port | `80` |

### Ingress `ingress-wildcard-host`

| Field | Value |
|-------|-------|
| Host | `foo.bar.com` |
| Path `/bar` | → service `service1` port `80` |
| Path `/foo` | → service `service2` port `80` |
| pathType | `Prefix` for both paths |

## Deliverables

- YAML for both Deployments, both Services, and the Ingress

## Verification checklist

- [ ] Ingress controller is running
- [ ] Ingress resource exists with host `foo.bar.com`
- [ ] Request to `http://foo.bar.com/bar` hits the nginx backend
- [ ] Request to `http://foo.bar.com/foo` hits the httpd backend

## Testing on Minikube

1. Get Minikube IP: `minikube ip`
2. Add to `/etc/hosts`: `<minikube-ip>  foo.bar.com`
3. Test:

```bash
curl -H "Host: foo.bar.com" http://$(minikube ip)/bar
curl -H "Host: foo.bar.com" http://$(minikube ip)/foo
```

You should get different responses from nginx vs httpd.
