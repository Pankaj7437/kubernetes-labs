# Nautilus DevOps: Kubernetes ReplicaSet Deployment

## Problem Statement
The Nautilus DevOps team is preparing to migrate applications to a Kubernetes cluster. To ensure high availability and desired state management for the front-end web tier, a ReplicaSet must be configured and deployed on the cluster.

## Objective
Create a Kubernetes ReplicaSet using the `httpd:latest` image to maintain 4 concurrent running pods.

## Specifications
*   **ReplicaSet Name:** `httpd-replicaset`
*   **Image:** `httpd:latest`
*   **Labels:** `app: httpd_app`, `type: front-end`
*   **Container Name:** `httpd-container`
*   **Replica Count:** 4
*   **Execution Environment:** `jump-host`

---

## Deployment Guide

### 1. Create the Configuration Manifest
On the `jump-host` terminal, create a file named `rs.yaml` with the following definition:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
  labels:
    app: httpd_app
    type: front-end
spec:
  replicas: 4
  selector:
    matchLabels:
      app: httpd_app
      type: front-end
  template:
    metadata:
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest

```

### 2. Apply the Configuration

Deploy the ReplicaSet to the Kubernetes cluster using `kubectl`:

```bash
kubectl apply -f rs.yaml

```

**Expected Output:**

```
replicaset.apps/httpd-replicaset created

```

### 3. Verify the Deployment

Check the status of the ReplicaSet to ensure it has reached the desired state of 4 replicas:

```bash
kubectl get rs httpd-replicaset

```

**Expected Output:**

```
NAME               DESIRED   CURRENT   READY   AGE
httpd-replicaset   4         4         4       15s

```

To view the individual pods managed by the ReplicaSet, you can filter by the assigned labels:

```bash
kubectl get pods -l app=httpd_app,type=front-end

```
