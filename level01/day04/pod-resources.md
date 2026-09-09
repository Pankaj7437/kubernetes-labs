# Nautilus DevOps: Kubernetes Resource Limits Lab

## Objective

Address performance issues by deploying a Kubernetes pod with strict container-level resource requests and limits to constrain CPU and memory utilization.

## Lab Specifications

* **Pod Name:** `httpd-pod`
* **Container Name:** `httpd-container`
* **Image:** `httpd:latest`
* **Requests:** Memory `15Mi`, CPU `100m`
* **Limits:** Memory `20Mi`, CPU `100m`

---

## Deployment Steps

Execute the following commands sequentially on the `jump-host` terminal to provision the pod using a declarative YAML manifest.

### 1. Create the Pod Manifest

Generate the YAML configuration file (`httpd-pod.yaml`) with the required resource constraints:

```bash
cat <<EOF > httpd-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"
EOF

```

### 2. Apply the Configuration

Deploy the pod to the Kubernetes cluster using the newly created manifest:

```bash
kubectl apply -f httpd-pod.yaml

```

### 3. Verify the Deployment

Confirm that the pod is running and inspect its configuration to validate that the resource limits and requests were applied correctly:

```bash
kubectl get pods
kubectl describe pod httpd-pod | grep -A 5 Limits

```
