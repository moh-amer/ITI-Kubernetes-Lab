# Lab 12 — What binds? (one lab, two experiments)

## Scenario

You will prove how the control plane matches static PVs to PVCs. No StorageClass — use `storageClassName: ""` everywhere.

---

## Experiment A — PV smaller than the PVC

1. Create PersistentVolume `quiz-pv`:
   - capacity **10Gi**
   - `ReadWriteOnce`
   - `storageClassName: ""`
   - `hostPath` → `/tmp/quiz-pv` + `DirectoryOrCreate`

2. Create PersistentVolumeClaim `too-big`:
   - request **12Gi**
   - `ReadWriteOnce`
   - `storageClassName: ""`

3. Run:

```bash
kubectl get pv quiz-pv
kubectl get pvc too-big
kubectl describe pvc too-big
```

4. **Write your answer:** What are the statuses of the PV and the PVC, and why?

Delete **only** the PVC `too-big` before continuing (keep the PV).

---

## Experiment B — Two PVCs, one PV

Keep the same PV (`quiz-pv` = 10Gi).

1. Create two PVCs, both with request **5Gi**, `storageClassName: ""`:
   - `claim-a`
   - `claim-b`

2. Run:

```bash
kubectl get pv quiz-pv
kubectl get pvc
```

3. **Write your answers:**
   - How many PVCs are `Bound`?
   - How many stay `Pending`?
   - Which PVC name owns the PV (`kubectl get pv quiz-pv` → `CLAIM` column)?
   - Why didn’t both 5Gi claims bind to the 10Gi volume?

---

## Rubric (must state clearly)

| Question | Your conclusion (fill in) |
|----------|---------------------------|
| PV 10Gi + PVC 12Gi | |
| One PV 10Gi + two PVC 5Gi | |

## Cleanup

```bash
kubectl delete pvc too-big claim-a claim-b  --ignore-not-found
kubectl delete pv quiz-pv --ignore-not-found
```
