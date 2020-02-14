In this section, we will import a Tekton Pipeline to build and deploy the
demo Nodejs app called [MyApp](https://github.com/ncskier/myapp).

## Open the Tekton Dashboard Import Tekton resources page

https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/#/importresources

## Import the MyApp Tekton resources

The Tekton resources are defined in the
[`tekton/`](https://github.com/ncskier/myapp/tree/master/tekton) directory of
MyApp. Import these Tekton resources into the `default` Namespace by
filling in the form with the following information:

Repository URL: `https://github.com/ncskier/myapp`{{copy}}

Namespace: `default`

Repository directory: `tekton/`{{copy}}

Service Account `tekton-dashboard`

The form should look like the following:

![Import Tekton resources screenshot.](https://raw.githubusercontent.com/ncskier/katacoda/master/tekton-dashboard/images/import-tekton-resources.png)

Click the `Import and Apply` button.

## View the progress importing the Tekton resources

The Dashboard creates a PipelineRun to import the specified Tekton resources.

Click on the `View status of this run` link to view the status of importing the
Tekton resources for MyApp.

![View status of importing Tekton resources screenshot.](https://raw.githubusercontent.com/ncskier/katacoda/master/tekton-dashboard/images/view-status-of-pipeline0.png)
