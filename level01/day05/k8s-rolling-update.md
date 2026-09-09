# Nautilus DevOps: Kubernetes Rolling Update Lab

## Objective

Update a live application running on a Kubernetes cluster with zero downtime by performing a rolling update to deploy a new container image version.

## Lab Specifications

* **Deployment Name:** `nginx-deployment`
* **Container Name:** `nginx-container`
* **Original Image:** `nginx:1.16`
* **Target Image:** `nginx:1.18`
* **Execution Environment:** `jump-host`

---

## Deployment Steps

Execute the following commands sequentially on the `jump-host` terminal to trigger and verify the rolling update.

### 1. Perform the Rolling Update

Update the deployment configuration to use the newly crafted `nginx:1.18` image. This command instructs Kubernetes to incrementally replace the old pods with new ones.

```bash
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.18

```

### 2. Monitor the Rollout Status

Watch the progress of the rolling update in real-time to ensure the new replicas are spinning up and the old ones are terminating properly.

```bash
kubectl rollout status deployment/nginx-deployment

```

### 3. Verify the Update

Confirm that all pods are fully operational and that the deployment has officially registered the new image version.

```bash
kubectl get pods
kubectl describe deployment nginx-deployment | grep Image

```
