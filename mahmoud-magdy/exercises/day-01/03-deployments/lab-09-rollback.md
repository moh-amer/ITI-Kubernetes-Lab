# Lab 09 — Rollback

## Scenario

The new nginx version from Lab 08 has a bug. Roll back to the previous working revision.

## Prerequisite

Complete **Lab 08** so the Deployment has at least two revisions in its rollout history.

## Requirements

1. Roll back `nginx-deployment` to the **previous** revision.
2. Do not delete and recreate the Deployment.

## Deliverables

- Command(s) you ran
- Deployment running the previous image version

## Verification checklist

- [ ] Rollout history shows multiple revisions
- [ ] Pods run the image from before Lab 08 (not `nginx:1.18`)
- [ ] Deployment is healthy with 3 replicas

## Hint

Check rollout history before and after the rollback.
