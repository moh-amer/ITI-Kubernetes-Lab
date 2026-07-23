# ITI Kubernetes Labs

Hands-on exercises for the Kubernetes module. **You write the YAML and run the commands.**

## Environment

- Minikube or KillerCoda
- Official container images only — no custom Docker builds
- No volumes in these labs (ConfigMaps and Secrets use environment variables)

```bash
minikube start
minikube addons enable ingress   # needed for Lab 16 only
```

## Lab order

| # | Lab | Topic |
|---|-----|-------|
| 01 | [Namespace and Pod](01-namespaces/lab-01-namespace-and-pod.md) | Namespaces, Pods |
| 02 | [HTTPD Pod](02-pods/lab-02-pod-httpd.md) | Pods |
| 03 | [Pod with env vars](02-pods/lab-03-pod-env-vars.md) | Pods |
| 04 | [ReplicaSet](03-replicaset/lab-04-replicaset.md) | ReplicaSet |
| 05 | [ReplicationController](03-replicaset/lab-05-replicationcontroller.md) | ReplicaSet |
| 06 | [Nginx Deployment](04-deployments/lab-06-nginx-deployment.md) | Deployments |
| 07 | [Deployment + NodePort Service](05-services/lab-07-nginx-deployment-and-nodeport.md) | Deployments, Services |
| 08 | [Rolling update](04-deployments/lab-08-rolling-update.md) | Deployments |
| 09 | [Rollback](04-deployments/lab-09-rollback.md) | Deployments |
| 10 | [Httpd deploy, update & rollback](04-deployments/lab-10-httpd-deploy-update-rollback.md) | Namespaces, Deployments, Services |
| 11 | [Update Deployment and Service](05-services/lab-11-update-deployment-and-service.md) | Deployments, Services |
| 12 | [ConfigMap + Pod](06-configmaps/lab-12-configmap-pod.md) | ConfigMaps |
| 13 | [ConfigMap + Deployment](06-configmaps/lab-13-configmap-deployment.md) | ConfigMaps, Deployments |
| 14 | [Secret + Pod](07-secrets/lab-14-secret-env.md) | Secrets |
| 15 | [MySQL StatefulSet](08-statefulsets/lab-15-mysql-statefulset.md) | StatefulSets, Services |
| 16 | [Ingress routing](09-ingress/lab-16-ingress.md) | Ingress, Services |

## Submission

Save your YAML files in a folder named with your name. Be ready to show:

- `kubectl get` output for your resources
- How you tested the app (browser, `curl`, or `kubectl logs`)
