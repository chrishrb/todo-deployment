<br />
<div align="center">
  <a href="https://www.github.com/chrishrb/todo-app">
    <img src="docs/logo.png" alt="Logo" height="80">
    <img src="docs/kubernetes.png" alt="Logo" height="80">
  </a>

  <h3 align="center">ToDo List</h3>

  <p align="center">
    An awesome way to track your todos
  </p>
</div>

## Getting started

1. Setup K3D if you are developing local
    ```bash
    k3d cluster create default
    k3d node edit k3d-default-serverlb --port-add 8080:80
    ```

2. Configure ingress (and `/etc/hosts` / add dns entries)
    ```bash
    kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.2/deploy/static/provider/cloud/deploy.yaml
    sudo vim /etc/hosts

    # add these entries to /etc/hosts -->
    127.0.0.1       dev.todo.local
    127.0.0.1       prod.todo.local
    # <--
    ```

3. Setup ArgoCD (see https://argo-cd.readthedocs.io/en/stable/getting_started/) and create namespaces
    ```bash
    kubectl apply -f manifests/namespaces/kustomization.yaml
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    kubectl apply -f bootstrap/argocd.yaml

    ```

4. Check in ArgoCD GUI if everything is in status `Synced`
    ```bash
    kubectl port-forward svc/argocd-server -n argocd 8080:443
    ```

5. Go to http://dev.todo.local:8080 or http://prod.todo.local:8080/

## Todos

- [ ] put all resources under control of argocd
- [ ] generate secrets
