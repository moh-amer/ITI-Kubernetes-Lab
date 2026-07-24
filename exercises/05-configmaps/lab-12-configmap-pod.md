# Lab 12 — ConfigMap and Pod

## Scenario

A monitoring pod prints timestamps on an interval. The interval is stored in a ConfigMap (not hard-coded in the pod).

## Requirements

### Namespace

Create namespace `datacenter`.

### ConfigMap `time-config` (in `datacenter`)

| Key | Value |
|-----|-------|
| `TIME_FREQ` | `11` |

### Pod `time-check` (in `datacenter`)

| Field | Value |
|-------|-------|
| Container name | `time-check` |
| Image | `busybox:latest` |
| Behavior | Print current date/time, wait `TIME_FREQ` seconds, repeat forever |
| Config | Read `TIME_FREQ` from the ConfigMap as an **environment variable** |
| Output | Write to stdout (use `kubectl logs` — **no volumes**) |

## Deliverables

- YAML manifest(s)

## Verification checklist

- [ ] ConfigMap `time-config` exists in `datacenter`
- [ ] Pod is `Running`
- [ ] Logs show a new timestamp roughly every 11 seconds
- [ ] `TIME_FREQ=11` is visible inside the container environment

## Bonus (optional)

Change `TIME_FREQ` to `5` in the ConfigMap, recreate the pod, and confirm logs update to ~5 second intervals.
