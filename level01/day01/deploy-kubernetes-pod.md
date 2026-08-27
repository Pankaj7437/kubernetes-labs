# Kubernetes Pod Creation – `pod-httpd`

## Overview

This lab focuses on creating and configuring a basic Kubernetes Pod using `kubectl`.

The requirement was to create a Pod named `pod-httpd` using the `httpd:latest` image, configure a custom container name, and apply a specific label.

---

## Requirements

| Configuration  | Value             |
| -------------- | ----------------- |
| Pod Name       | `pod-httpd`       |
| Container Name | `httpd-container` |
| Image          | `httpd:latest`    |
| Label          | `app=httpd_app`   |

---

## 1. Verify Kubernetes Access

The `kubectl` utility on the jump host was already configured for the Kubernetes cluster.

```bash
kubectl get nodes
```

This verifies that the cluster is accessible.

---

## 2. Create the Pod Manifest

Create a YAML file:

```bash
vi pod.yaml
```

Add the following:

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: pod-httpd
  labels:
    app: httpd_app

spec:
  containers:
    - name: httpd-container
      image: httpd:latest
```

### Configuration Explanation

* `kind: Pod` → Creates a Kubernetes Pod.
* `metadata.name` → Sets the Pod name to `pod-httpd`.
* `labels` → Adds the required `app=httpd_app` label.
* `containers.name` → Sets the container name to `httpd-container`.
* `image` → Uses the `httpd:latest` image.

---

## 3. Create the Pod

Apply the manifest:

```bash
kubectl apply -f pod.yaml
```

Expected output:

```text
pod/pod-httpd created
```

---

## 4. Verify the Pod

Check the Pod status:

```bash
kubectl get pods
```

Expected:

```text
NAME         READY   STATUS    RESTARTS   AGE
pod-httpd    1/1     Running   0          ...
```

---

## 5. Verify Container Name

```bash
kubectl get pod pod-httpd \
  -o jsonpath='{.spec.containers[0].name}'
```

Expected:

```text
httpd-container
```

---

## 6. Verify Image

```bash
kubectl get pod pod-httpd \
  -o jsonpath='{.spec.containers[0].image}'
```

Expected:

```text
httpd:latest
```

---

## 7. Verify Label

```bash
kubectl get pod pod-httpd \
  -o jsonpath='{.metadata.labels.app}'
```

Expected:

```text
httpd_app
```

Alternatively:

```bash
kubectl get pods --show-labels
```

---

## 8. Inspect the Pod

For detailed information:

```bash
kubectl describe pod pod-httpd
```

To view the complete Kubernetes manifest generated for the Pod:

```bash
kubectl get pod pod-httpd -o yaml
```

---

## Kubernetes Architecture

```text
Kubernetes Cluster
        │
        ▼
┌─────────────────────────────┐
│ Pod: pod-httpd              │
│                             │
│ Label: app=httpd_app        │
│                             │
│  ┌───────────────────────┐  │
│  │ Container              │  │
│  │ Name: httpd-container  │  │
│  │ Image: httpd:latest    │  │
│  └───────────────────────┘  │
│                             │
└─────────────────────────────┘
```

---

## Troubleshooting

### Check Pod status

```bash
kubectl get pods
```

### Check detailed events

```bash
kubectl describe pod pod-httpd
```

### Check container logs

```bash
kubectl logs pod-httpd
```

### Check Pod configuration

```bash
kubectl get pod pod-httpd -o yaml
```

---

## Final Verification

The completed Pod should have the following configuration:

```text
Pod Name:       pod-httpd
Container Name: httpd-container
Image:          httpd:latest
Label:          app=httpd_app
Status:         Running
```

## Key Concepts

* Kubernetes Pods
* Pod YAML manifests
* `kubectl apply`
* Kubernetes labels
* Container configuration
* Docker images in Kubernetes
* Pod inspection and troubleshooting
* JSONPath queries with `kubectl`
