# Infrastructure Deployment Guide

This guide explains how to deploy the ToDo application and verify its status within the Kubernetes cluster.

## 1. Apply Manifests

Run the following commands sequentially to create the namespace, application pod, and test utility pod:

```bash
kubectl apply -f .infrastructure/namespace.yml
kubectl apply -f .infrastructure/todoapp-pod.yml
kubectl apply -f .infrastructure/busybox.yml


### Application Verification

# Port-forwarding for local verification
kubectl port-forward pod/todoapp-pod 8080:8000 -n todoapp

Once the command is running, open the following URL in your browser: http://localhost:8080

# Testing availability via busyboxplus:curl pod
kubectl exec -it busybox-test-pod -n todoapp -- curl http://todoapp-pod:8000/api/healthz/liveness/