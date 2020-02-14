In this section, we will install and expose the Tekton Dashboard.

## Install the Tekton Dashboard Prerequisites

- Tekton Pipelines
`kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml`{{execute}}
- Tekton Triggers (optional)
`kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml`{{execute}}

Verify the pods are running:
`kubectl get pods -n tekton-pipelines`{{execute}}

## Install the Tekton Dashboard

`kubectl apply --filename https://github.com/tektoncd/dashboard/releases/download/v0.5.1/tekton-dashboard-release.yaml`{{execute}}

<!-- `kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release.yaml`{{execute}} -->

Verify the Dashboard pod is running:
`kubectl get pods -n tekton-pipelines`{{execute}}

## Expose the Tekton Dashboard

### Install Ingress controller

Install the nginx ingress controller into the `ingress-nginx` namespace:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml
```{{execute}}

Verify the ingress controller pod is running:

```bash
kubectl get pods -n ingress-nginx
```{{execute}}

### Create Ingress for the Tekton Dashboard

View the Tekton Dashboard Service:
`kubectl get svc tekton-dashboard -n tekton-pipelines`{{execute}}

The Tekton Dashboard Service is exposed on port `9097`. So, create an Ingress
for the `tekton-dashboard` Service on port `9097`:

```bash
cat << EOF | kubectl apply -f -
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: tekton-dashboard
  namespace: tekton-pipelines
spec:
  backend:
    serviceName: tekton-dashboard
    servicePort: 9097
EOF
```{{execute}}

Verify the Ingress was created:
`kubectl get ingress -n tekton-pipelines`{{execute}}

## Open the Tekton Dashboard

https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/
