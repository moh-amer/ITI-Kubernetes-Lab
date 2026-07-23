# Lab 02 — HTTPD Pod

## Scenario

Deploy a single Apache HTTP server pod to verify basic pod creation.

## Requirements

Create a pod named `pod-httpd`:

| Field | Value |
|-------|-------|
| Image | `httpd:latest` |
| Container name | `httpd-container` |
| Label | `app: httpd_app` |

## Deliverables

- YAML manifest
- Pod in `Running` state

## Verification checklist

- [ ] Pod name is `pod-httpd`
- [ ] Container name is `httpd-container`
- [ ] Label `app=httpd_app` is set
