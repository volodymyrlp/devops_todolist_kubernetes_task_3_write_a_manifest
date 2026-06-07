# Deployment and Testing Instructions

This guide provides instructions on how to deploy the application manifests, test connectivity via port-forwarding, and verify the application's health using a `busyboxplus:curl` container.

---

## 1. Applying Manifests

To deploy the entire infrastructure, apply the manifests located in the `.infrastructure` folder in the following order:

```bash
# 1. Create the dedicated namespace
kubectl apply -f .infrastructure/namespace.yml

# 2. Deploy the main Django application Pod
kubectl apply -f .infrastructure/todoapp-pod.yml

### 3. Testing via busyboxplus:curl
# First, check the actual Pod IP using: kubectl get pods -n todo-namespace -o wide
kubectl exec -it busybox-test-pod -n todo-namespace -- curl http://10.244.0.10:8000/api/healthz/readiness/
