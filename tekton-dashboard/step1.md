## Install the Tekton Dashboard Prerequisites

- Tekton Pipelines `kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml`{{execute}}
- Tekton Triggers `kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml`{{execute}}

## Install the Tekton Dashboard

`kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/release.yaml`{{execute}}

Verify the dashboard pod is running `kubectl get pods -n tekton-pipelines`{{execute}}

## Expose the Tekton Dashboard

### Install Ingress controller

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/mandatory.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/static/provider/cloud-generic.yaml
```{{execute}}

This installs the nginx ingress controller into the `ingress-nginx` namespace:
```bash
kubectl get pods -n ingress-nginx
```{{execute}}

### Create Ingress for the Tekton Dashboard
View Tekton Dashboard service `kubectl get svc tekton-dashboard -n tekton-pipelines`{{execute}}
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

View the ingress was created `kubectl get ingress -n tekton-pipelines`{{execute}}

## Open the Dashboard
https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/
