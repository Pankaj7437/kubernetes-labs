# Nautilus DevOps: Kubernetes CronJob Scheduling

## Problem Statement
The Nautilus DevOps team is configuring automated, recurring tasks across the Kubernetes cluster. As a preliminary step for deploying periodic execution scripts, placeholder CronJobs are being established to validate scheduling, container configurations, and job execution flows.

## Objective
Deploy a CronJob named `datacenter` to execute a dummy command (`echo Welcome to xfusioncorp!`) on a defined schedule using the `httpd:latest` image.

## Lab Specifications
*   **CronJob Name:** `datacenter`
*   **Schedule:** `*/6 * * * *` (Every 6 minutes)
*   **Container Name:** `cron-datacenter`
*   **Image:** `httpd:latest`
*   **Command:** `["echo", "Welcome to xfusioncorp!"]`
*   **Restart Policy:** `OnFailure`

---

## Deployment Guide

### 1. Create the Configuration Manifest
On the `jump-host` terminal, create a file named `cronjob.yaml` with the following definition:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: datacenter
spec:
  schedule: "*/6 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-datacenter
            image: httpd:latest
            command: ["echo", "Welcome to xfusioncorp!"]
          restartPolicy: OnFailure

```

### 2. Apply the Configuration

Deploy the CronJob to the Kubernetes cluster using `kubectl`:

```bash
kubectl apply -f cronjob.yaml

```

**Expected Output:**

```text
cronjob.batch/datacenter created

```

### 3. Verify the Deployment

Check the status of the CronJob to ensure it is registered with the correct schedule:

```bash
kubectl get cronjob datacenter

```

**Expected Output:**

```text
NAME         SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE
datacenter   */6 * * * *   False     0        <none>          15s

```

### 4. (Optional) Manual Trigger Testing

To verify the command executes correctly without waiting for the 6-minute interval, manually trigger a Job from the CronJob:

```bash
kubectl create job --from=cronjob/datacenter datacenter-manual-test

```

View the logs of the resulting pod to confirm the `echo` command executed successfully:

```bash
kubectl logs -l job-name=datacenter-manual-test

```

**Expected Output:**

```text
Welcome to xfusioncorp!

```

