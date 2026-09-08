# Nautilus DevOps: Kubernetes Pod Deployment Lab

## Objective

Deploy a microservice onto a Kubernetes cluster by creating a dedicated namespace and launching an Nginx pod within it.

## Lab Specifications

* **Namespace:** `dev`
* **Pod Name:** `dev-nginx-pod`
* **Image:** `nginx:latest`
* **Execution Environment:** `jump-host`

---

## Deployment Steps

Execute the following commands sequentially on the `jump-host` terminal.

### 1. Create the Namespace

Provision the dedicated namespace for the development environment.

```bash
kubectl create namespace dev

```

### 2. Deploy the Pod

Create and run the Nginx pod specifically within the `dev` namespace using the requested image tag.

```bash
kubectl run dev-nginx-pod --image=nginx:latest -n dev

```

### 3. Verify the Deployment

Confirm that the pod has been successfully scheduled and is running within the correct namespace.

```bash
kubectl get pods -n dev

```
