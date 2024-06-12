# everflow-jh

Azure Devops Pipeline - azure-pipelines-dotnet-app.yml

**the pipeline has comments on some of the sections to explain

 - Pipeline created to build the docker image and push this to an azure registery, which there would be a connection setup for in azure devops
 - The pipeline will be triggered by commits made to main, build/ and release/ branches
 - It will run each task within a container itself on the an azure agent vm
 - it will also have the ability to connect to a vault (hashicorp vault used as example) - this is so it can grab sensitive data like potential hosts, connection credentials, spn connection details to aks cluster, and any values you might want to use during the helm deployment of the app
 - The pipeline will deploy to a test environment and then to a production env if this succeeds

Ansible playbooks

This can be a good way to manage and manipulate potential difficult apps 

- instead of putting the code into the pipeline to connect an aks cluster, i have implemented this into an ansible playbook which is called via the stage in the pipeline - the env is determined via vault variables
- The playbook will use the securefiles defined in azure devops to connect to vault, and then get the required SPN details needed to connect to the AKS cluster you are deploying to.
- it will also pull an app secret values in case you want to amend helm values for the deployment
- it will then deploy the app via helm command

Helm Charts

This is just an example helm charts that has been created for the app, which will be used to deploy the app 

would would do with more time:
- complete helm charts for application and amend this as required
- demonstrate terraform codeing to create the AKS cluster, all the networking, nsg's, node pools, taints, tollerations etc.
- add more testing of the image build, github workflows would be good to run after a commit, and same for helm commands, do helm lint to test the run first.


