# Lab 01 — Namespace and Pod

## Scenario

Your team is splitting workloads by environment. Create a dedicated namespace and run a web server pod inside it.

## Requirements

1. Create a namespace named `dev`.
2. In the `dev` namespace, create a pod named `dev-nginx-pod`:
   - Image: `nginx:latest`
   - Label: `app: dev-nginx-pod`

## Deliverables

- YAML manifest(s) you used
- Pod running in the `dev` namespace

## Verification checklist

- [ ] `dev` namespace exists
- [ ] Pod `dev-nginx-pod` is in `Running` state
- [ ] Pod is in namespace `dev`, not `default`
