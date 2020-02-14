## Create a PipelineRun to run MyApp's Pipeline

```bash
cat << EOF | kubectl apply -f -
apiVersion: tekton.dev/v1alpha1
kind: PipelineRun
metadata:
  name: myapp
spec:
  pipelineRef:
    name: myapp
  resources:
    - name: source
      resourceSpec:
        type: git
        params:
          - name: revision
            value: master
          - name: url
            value: https://github.com/ncskier/myapp
EOF
```{{execute}}

## Monitor the PipelineRun logs
https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/#/namespaces/default/pipelineruns/myapp

## Open the Deployed App
https://[[HOST_SUBDOMAIN]]-4000-[[KATACODA_HOST]].environments.katacoda.com/
