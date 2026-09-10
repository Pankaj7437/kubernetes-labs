# Nautilus DevOps: Kubernetes Deployment Rollback Lab

## Problem Statement

Earlier today, the Nautilus DevOps team deployed a new release for an application. However, a customer has reported a bug related to this recent release. Consequently, the team aims to revert to the previous version. There exists a deployment named `nginx-deployment`; initiate a rollback to the previous revision.

## Objective

Quickly mitigate a production bug by rolling back a Kubernetes deployment to its previously stable revision using the `kubectl` utility on the `jump-host`.

## Lab Specifications

* **Deployment Name:** `nginx-deployment`
* **Action:** Rollback to previous revision
* **Execution Environment:** `jump-host`

---

## Execution Steps

Execute the following commands sequentially on the `jump-host` terminal.

### 1. Initiate the Rollback

Revert the deployment to the immediately preceding revision to restore the stable application state.

```bash
kubectl rollout undo deployment/nginx-deployment

```

### 2. Monitor the Rollback Status

Watch the deployment status to confirm that the pods with the buggy release are terminating and the pods for the previous revision are successfully coming online.

```bash
kubectl rollout status deployment/nginx-deployment

```

### 3. Confirm the Current State

Verify that the deployment is running the expected image from the previous version.

```bash
kubectl describe deployment nginx-deployment | grep Image

```
