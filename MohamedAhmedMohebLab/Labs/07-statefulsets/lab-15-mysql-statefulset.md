# Lab 15 — MySQL StatefulSet

## Scenario

Deploy MySQL with stable pod identities using a StatefulSet and a headless Service. No persistent volumes for this lab.

## Requirements

### Headless Service `mysql-svc`

| Field | Value |
|-------|-------|
| Type | `ClusterIP` with `clusterIP: None` |
| Port | `3306` → target `3306` |
| Selector | `app: mysql` |

### StatefulSet `mysql`

| Field | Value |
|-------|-------|
| Replicas | `2` |
| serviceName | `mysql-svc` |
| Container name | `mysql` |
| Image | `mysql:9.7.1` |
| Port | `3306` |
| Env | `MYSQL_ROOT_PASSWORD=password`, `MYSQL_DATABASE=mydatabase`, `MYSQL_USER=myuser`, `MYSQL_PASSWORD=mypassword` |
| Labels | `app: mysql` on selector and pod template |

## Deliverables

- YAML manifest(s)

## Verification checklist

- [ ] StatefulSet shows `2/2` ready replicas
- [ ] Pods are named `mysql-0` and `mysql-1` (ordered, stable names)
- [ ] Headless service `mysql-svc` exists with no cluster IP
- [ ] Both pods are `Running`

## Hint

StatefulSet pods get predictable DNS names: `mysql-0.mysql-svc.<namespace>.svc.cluster.local`
