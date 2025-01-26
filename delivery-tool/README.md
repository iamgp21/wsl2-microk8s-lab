### Delivery tool Used:
We will be using ArgoCD as a kubernetes Native Contineous Delivery tool to deploy any applications/helm chart etc on our local microk8s kubernetes cluster. 

[Helm Chart Source Code](https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd)

### Pre-requisites:
- MicroK8s creates a group to enable seamless usage of commands which require admin privilege. To add your current user to the group and gain access to the .kube caching directory, run the following three commands:

```
sudo usermod -a -G microk8s $USER
mkdir -p ~/.kube
chmod 0700 ~/.kube
```
*NOTE* : Reboot the machine for group changes to take effect.

- Requirement of Github Self hosted Runner: Login to your github accound and follow [Adding self hosted runner](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/adding-self-hosted-runners?ref=goatreview.com)

- Under `delivery-tool/chart` directory run below command to Add argo helm repo and pull it: 

```
helm repo add argo https://argoproj.github.io/argo-helm
/snap/bin/microk8s helm pull argo/argo-cd
tar -zxvf argo-cd-7.3.9.tgz
rm -rf argo-cd-7.3.9.tgz
```
### Temporary Password:

Once the github action deploys argocd on microk8s cluster run below command on your machine to get admin user password and login to http://`Argo-cd-server-Load-Balancer-service-IP`:80

`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`