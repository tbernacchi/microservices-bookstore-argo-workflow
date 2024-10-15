## Service account + Workflow templates

Argo Workflows need a service account in the respective namespace where the workloads and builds it's going to run in order to work properly. This service account will have the necessary permissions to manage workflows, interact with pods and etctera. More info you can find [here](https://argo-workflows.readthedocs.io/en/latest/service-accounts/).

#

The `rbac.yaml` creates a `ServiceAccount` with respective `Role` and `RoleBinding` and the `workflow` directory contains all the workflows template files for each application.
