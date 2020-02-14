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

Click on the following link to go directly to the `myapp` PipelineRun
logs page:
https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/#/namespaces/default/pipelineruns/myapp

Or navigate to the `myapp` PipelineRun in the `default` Namespace's PipelineRuns
list.

*Make sure the `default` Namespace is selected in the Namespace dropdown.*

![Navigate to MyApp PipelineRun screenshot.](https://raw.githubusercontent.com/ncskier/katacoda/master/tekton-dashboard/images/navigate-to-myapp-pipelinerun.png)

![View the running PipelineRun logs for MyApp screenshot.](https://raw.githubusercontent.com/ncskier/katacoda/master/tekton-dashboard/images/myapp-pipelinerun-logs-running.png)

## Open the Deployed App

Verify both the `build` and `deploy` tasks have passed.

![View the completed PipelineRun logs for MyApp screenshot.](https://raw.githubusercontent.com/ncskier/katacoda/master/tekton-dashboard/images/view-myapp-pipelinerun-logs.png)

MyApp will be running on port `3000`. Click on the following link to open the
app:
https://[[HOST_SUBDOMAIN]]-3000-[[KATACODA_HOST]].environments.katacoda.com/
