# Lab 03 — Pod with environment variables

## Scenario

A greeting script reads configuration from environment variables. Deploy a pod that prints a message and exits.

## Requirements

Create a pod named `print-envars-greeting`:

| Field | Value |
|-------|-------|
| Container name | `print-env-container` |
| Image | `bash:latest` |
| `GREETING` | `Welcome to` |
| `COMPANY` | `ITI` |
| `GROUP` | `DevOps` |
| Command | Print `GREETING`, `COMPANY`, and `GROUP` on one line |
| Restart policy | `Never` |

## Deliverables

- YAML manifest
- Pod logs showing the greeting line

## Verification checklist

- [ ] Pod completes successfully (or shows `Completed`)
- [ ] Logs contain: `Welcome to ITI DevOps` (or equivalent spacing)
