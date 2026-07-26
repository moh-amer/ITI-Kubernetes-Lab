# Demo 12 — PV binding rules (size + one-PV-one-PVC)

**Goal:** Answer two questions with hands-on proof:

1. PV = **10Gi**, PVC asks for **12Gi** → what happens?
2. One PV = **10Gi**, **two** PVCs ask for **5Gi** each → what happens?

## Setup

Work in the `default` namespace (no extra setup).

---

## Experiment A — PVC larger than the PV

| Object | Size |
|--------|------|
| PV `bind-pv` | **10Gi** |
| PVC `too-big` | **12Gi** |

```bash
kubectl apply -f pv.yaml
kubectl apply -f experiment-a-pvc.yaml

kubectl get pv bind-pv
kubectl get pvc too-big
kubectl describe pvc too-big | sed -n '/Events/,$p'
```

### Expected result

| Object | Status | Why |
|--------|--------|-----|
| PV | **Available** | Nothing matched it |
| PVC | **Pending** | Request **12Gi** > PV capacity **10Gi**. A PVC can only bind to a PV that is **≥** the request. |

There is no “stretch the PV” — the claim stays Pending until a large enough PV (or a StorageClass) exists.

```bash
# cleanup A only
kubectl delete -f experiment-a-pvc.yaml
# keep the PV for experiment B
```

---

## Experiment B — Two 5Gi PVCs, one 10Gi PV

Same PV (`bind-pv` = 10Gi). Create **two** PVCs that each ask for **5Gi**.

```bash
kubectl apply -f experiment-b-pvcs.yaml

kubectl get pv bind-pv
kubectl get pvc
kubectl describe pvc claim-a claim-b | sed -n '/Name:/,/Events:/p'
```

### Expected result

| Object | Status | Why |
|--------|--------|-----|
| One PVC (A or B) | **Bound** to `bind-pv` | 5Gi ≤ 10Gi, access mode matches, `storageClassName: ""` |
| The other PVC | **Pending** | A PersistentVolume binds to **exactly one** PVC. Size left over is **not** shared with a second claim. |
| PV | **Bound** | Shows `CLAIM = default/<the-winner>` |

So: leftover capacity on a PV is **not** a second volume. One PV → one PVC.

Optional proof the winner works:

```bash
kubectl apply -f pod-winner.yaml   # edit claimName if B won instead of A
kubectl wait --for=condition=Ready pod/bind-winner --timeout=60s
kubectl exec bind-winner -- sh -c 'echo ok > /data/x && cat /data/x'
```

---

## Cleanup

```bash
kubectl delete -f pod-winner.yaml --ignore-not-found
kubectl delete -f experiment-b-pvcs.yaml --ignore-not-found
kubectl delete -f experiment-a-pvc.yaml --ignore-not-found
kubectl delete -f pv.yaml --ignore-not-found
```

## Cheat-sheet answers

| Question | Answer |
|----------|--------|
| PV 10Gi + PVC 12Gi? | PVC **Pending**, PV **Available**. Request must be ≤ PV capacity. |
| One PV 10Gi + two PVC 5Gi? | **Only one** PVC binds; the other stays **Pending**. One PV ↔ one PVC. |
