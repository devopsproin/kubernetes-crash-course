# Kubernetes Crash Course

A **hands-on Kubernetes project** that teaches core concepts the way DevOps engineers use them: Deployments, ConfigMaps, NodePort Services, and zero-downtime restarts — with minimal theory.

---

## What You'll Learn

- What Kubernetes is and how it manages containers
- Deploying apps with **Deployments**
- Externalizing config with **ConfigMaps**
- Exposing apps with **NodePort Services**
- Updating configuration **without rebuilding images**
- Safe restarts with **rollout restart** (no downtime)
- Working with YAML and kubectl like in production

---

## Application Overview

- Runs in Kubernetes on **port 3000**
- Docker image on Docker Hub; UI driven by a **ConfigMap**
- Config changes take effect after a rollout restart — a common production pattern

---

## Prerequisites

- A Kubernetes cluster (KillerCoda, Minikube, Kind, or EKS/AKS/GKE)
- `kubectl` installed and configured

---

## Deploy the Application

**1. Check cluster**

```bash
kubectl get nodes
```

**2. Apply resources**

```bash
kubectl apply -f configmap.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

**3. Verify**

```bash
kubectl get deploy
kubectl get pods
kubectl get svc
kubectl get cm
```

Wait until pods are `Running` and `READY` is `1/1`.

---

## Access the Application

Get the NodePort:

```bash
kubectl get svc
```

Open: **`<node-ip>:<node-port>`**

> On **KillerCoda**, use **Traffic / Ports** in the UI to open the NodePort.

---

## Update Config Without Rebuilding the Image

1. Edit `configmap.yaml`
2. Apply and restart:

```bash
kubectl apply -f configmap.yaml
kubectl rollout restart deployment k8s-crash-course
```

3. Refresh the browser to see changes. Restart is rolling (no downtime).
