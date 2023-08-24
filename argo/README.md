
# ArgoCD
A declarative, GitOps continuous delivery tool for Kubernetes.<br>
We use ArgoCD to automate the deployments in specified target environments.

### This chart is made up of 3 main chart dependencies:

- `ArgoCD` from [official ArgoCD chart](https://github.com/argoproj/argo-helm/tree/master/charts/argo-cd)
- `Argocd-image-updater`: which is a plugin to argocd to allow automatic image updates.  Refer to this [official documentation](https://github.com/argoproj-labs/argocd-image-updater/blob/master/docs/configuration/images.md)
- `Argocd-notifications` : allows us to send notifications on slack. Refer to this [official documentation](https://argocd-notifications.readthedocs.io/en/latest/)

### Argocd deployed projects:
> **Command**: `kubectl -n argocd get appprojects.argoproj.io`
- [irembopay](https://github.com/Irembo/charts/blob/master/stable/argo/templates/irembopay-argo-appproject.yaml)

### Argocd deployed applications:
> **Command**: `kubectl -n argocd get applications.argoproj.io`
- [irembopay](https://github.com/Irembo/charts/blob/master/stable/argo/templates/irembogov-integration-service-argo-application.yaml)


# Argo install/upgrade
- `helm upgrade -i argo -n argocd . -f values-{env}.yaml`

`Run argocd in uat environment`

```
# for uat
# Make sure you are in the chart directory
helm dependency update
helm upgrade -i argo -n argocd . -f values.yaml
```
<br/>

`Run argocd in production environment`

```
# for production
# Make sure you are in the chart directory
helm dependency update
helm upgrade -i argo -n argocd . -f values-production.yaml
```



# Get password
- `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`

# Useful links
[ArgoCD declarative setup](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)

Adding a service to argocd:
- [How to create an argo project](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#projects)
- [How to create an argo application](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#applications)
- [How to enable auto deployment](https://www.notion.so/irembo/ArgoCD-auto-deployment-with-argocd-image-updater-4cb616d6813e43bc96f644c1115fcb23#25f606fc47b44a3f956c42427519526c)
