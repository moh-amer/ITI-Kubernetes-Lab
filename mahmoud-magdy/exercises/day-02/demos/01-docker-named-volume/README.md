# Demo 01 — Docker named volume

**Goal:** Prove the container writable layer is disposable; a named volume is not.

Needs Docker on your machine (or any host with the Docker CLI). Skip if you only have kubectl — continue with Demo 02.

## Steps

### 1) Disposable layer

```bash
docker run --name tmp alpine:3.20 sh -c 'echo hello > /data.txt && cat /data.txt'
docker rm -f tmp
docker run --rm alpine:3.20 cat /data.txt
# → can't open '/data.txt'
```

### 2) Named volume survives

```bash
docker volume create demo-data

docker run --rm -v demo-data:/data alpine:3.20 \
  sh -c 'echo persisted > /data/note.txt'

docker run --rm -v demo-data:/data alpine:3.20 cat /data/note.txt
# → persisted

docker volume rm demo-data
```

## Takeaway

Without a volume, data dies with the container. Kubernetes uses a different API (`volumes` + `volumeMounts`, later PVC), but the idea is the same.
