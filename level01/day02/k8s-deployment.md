# Kubernetes Nginx Deployment Lab

**Objective:** Create a Kubernetes deployment named `nginx` using the `nginx:latest` image on a pre-configured cluster.

**Environment:** The `kubectl` utility on the `jump-host` is already configured to work with the cluster.

## Solution Methods

You can complete this task using either the imperative (command-line) or declarative (YAML) approach. 

### Method 1: Imperative Command (Fastest)
This is the most efficient way to fulfill the lab requirements without manually formatting a YAML file. Run the following command directly on the `jump-host`:

```bash
kubectl create deployment nginx --image=nginx:latest

```

### Method 2: Declarative YAML File

If you need to use a manifest file, you must include the `selector` and `template` fields, which are mandatory for Kubernetes Deployments.

1. Create a YAML file (e.g., `nginx-deployment.yaml`):

```bash
vi nginx-deployment.yaml

```

2. Add the correct deployment configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest

```

3. Apply the configuration to the cluster:

```bash
kubectl apply -f nginx-deployment.yaml

```

## Verification

Verify that your deployment was created and the pods are spinning up successfully:

```bash
# Verify the deployment exists and is ready
kubectl get deployments

# Verify the underlying pods are running
kubectl get pods

```
