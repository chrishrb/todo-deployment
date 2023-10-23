# Todo app deployment

## Getting started

1. Setup kubernetes cluster and install ArgoCD (see https://argo-cd.readthedocs.io/en/stable/getting_started/)
    ```bash
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

    # port forward ui
    kubectl port-forward svc/argocd-server -n argocd 8080:443
    ```

2. Setup ArgoCD
    ```bash
    kubectl apply -f bootstrap/argocd.yaml
    ```
