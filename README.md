# argocd-config
ArgoCD on Pi4 with existing [k3s](https://github.com/alexellis/k3sup) cluster

## install ArgoCD in k3s
kubectl create namespace argocd
For Pi there is no ARM image built 
I have used `rdelprete/argocd-arm64:v2.1.3` and replaced images within https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

## Apply Application deployment 
Apply ArgoCD `kubectl apply -n argocd -f install.yaml`

Apply Application e.g. `monitoring-deploy.yaml` `kubectl apply -f monitoring-deploy.yaml` this will create the namespace as its included in the example deployment.

## access ArgoCD UI from local machine
- kubectl get svc -n argocd
- kubectl port-forward svc/argocd-server 8080:443 -n argocd

![image](https://user-images.githubusercontent.com/20583399/150231335-ca9d08c5-855c-4fae-9930-6f3a92fda117.png)


## login with admin user and below token (as in documentation):
- kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

`note: you can change and delete init password`

Links

- Nana Janashia Config repo: https://gitlab.com/nanuchi/argocd-app-config
- Install ArgoCD: https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd
- Login to ArgoCD: https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli
- ArgoCD Configuration: https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/
