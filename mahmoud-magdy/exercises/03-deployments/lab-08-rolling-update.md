# Lab 08 — Rolling update

## Scenario

A new nginx version is released. Update the running application without deleting the Deployment.

## Prerequisite

Complete **Lab 07** so `nginx-deployment` exists (3 replicas, current image `nginx:latest` or similar).

## Requirements

1. Change the Deployment image to `nginx:1.18`.
2. Use a rolling update (default Deployment strategy is fine).
3. Keep the Service from Lab 07 working.

## Deliverables

- Record of the command or manifest change you used
- Deployment running the new image

## Verification checklist

- [ ] All pods eventually use image `nginx:1.18`
- [ ] Deployment still has 3 replicas
- [ ] `kubectl rollout status` shows a successful rollout
- [ ] App is still reachable via the NodePort service

## Hint

You can use `kubectl set image`, `kubectl edit`, or re-apply an updated YAML file.
