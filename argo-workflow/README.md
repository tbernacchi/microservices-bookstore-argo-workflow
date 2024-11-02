<div align=>
	<img align="center" src=../.github/assets/img/argo.png>
</div> 

## argo-workflow 

To install argo-workflow I've followed the [documentation](https://argo-workflows.readthedocs.io/en/latest/quick-start/)

```
kubectl apply -n argo -f https://github.com/argoproj/argo-workflows/releases/download/v3.5.8/install.yaml
```

I've used this ingress `ingress-argo-workflow.yaml` and adjust the deployment to meet my needs to access the UI on `mykubernetes.com/argo`: 

```
kubectl edit deploy/argo-server -n argo
```

```
- args:
- --auth-mode=server
  env:
  - name: BASE_HREF
    value: /argo/
```


## Service account + Workflow templates

Argo Workflows need a service account in the respective namespace where the workloads and builds it's going to run in order to work properly. This service account needs some permissions to manage workflows, interact with pods and etctera. More info you can find [here](https://argo-workflows.readthedocs.io/en/latest/service-accounts/).

* The `rbac.yaml` creates a `ServiceAccount` with respective `Role` and `RoleBinding`; 
* The `workflow` directory contains all the workflows template files for each application.


# argo-cli
https://argo-workflows.readthedocs.io/en/latest/walk-through/argo-cli/ 
https://github.com/argoproj/argo-workflows/releases/ 

Example:

```
argo submit --from workflowtemplate/template-que-funciona -p repo="https://github.com/tbernacchi/infra-dev-challenge.git" -p revision="main" -p dockerfile-path="details" -p oci-image="ambrosiaaaaa/my-details-image" -p oci-tag="v0.0.2" -p oci-registry="docker.io" -p push-image="true" -n playground
```

## argo-cd

To install argo-cd I've followed the [https://argo-cd.readthedocs.io/en/stable/getting_started/](https://argo-cd.readthedocs.io/en/stable/getting_started/).

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
For this installation I've managed the UI through nginx-ingress to access on `mykubernetes.com/argocd`.

If the Argo CD UI is available under a non-root path (e.g. /argo-cd instead of /) then the UI path should be configured in the API server. To configure the UI path add the --basehref flag into the argocd-server deployment command:

I've use the `ingress-argocd.yaml`.

```
kubectl edit ing/argocd-server-ingress -n argocd
```

```
containers:
- args:
  - /usr/local/bin/argocd-server
  - --basehref
  - /argocd
```

Reference:
[https://argo-cd.readthedocs.io/en/latest/operator-manual/ingress/](https://argo-cd.readthedocs.io/en/latest/operator-manual/ingress/)

UI password: 

```
kubectl get secret/argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 --decode
```

# argo-rollouts

To enable the argo-rollouts on the UI I've use this extension: [https://github.com/argoproj-labs/rollout-extension](https://github.com/argoproj-labs/rollout-extension)

```
helm repo add argo-rollouts https://argoproj.github.io/argo-helm -n argo-rollouts
helm repo update
helm install argo-rollouts argo/argo-rollouts -n argo-rollouts --set dashboard.enabled=true
```

```
kubectl edit deployment argocd-server -n argocd
```

```

apiVersion: apps/v1
kind: Deployment
metadata:
  name: argocd-server
  namespace: argocd
spec:
  template:
    spec:
      initContainers:
        - name: rollout-extension
          image: quay.io/argoprojlabs/argocd-extension-installer:v0.0.8
          env:
          - name: EXTENSION_URL
            value: https://github.com/argoproj-labs/rollout-extension/releases/download/v0.3.6/extension.tar
          volumeMounts:
            - name: extensions
              mountPath: /tmp/extensions/
          securityContext:
            runAsUser: 1000
            allowPrivilegeEscalation: false
      containers:
        - name: argocd-server
          volumeMounts:
            - name: extensions
              mountPath: /tmp/extensions/
      volumes:
        - name: extensions
          emptyDir: {}
```

