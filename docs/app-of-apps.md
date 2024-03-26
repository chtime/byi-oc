# Setup Windows

1. Install argocd operator manually via Openshift UI
2. ArgoCD namespace 
    ```bash
    kubectl create ns argocd
    ```
3. ArgoCD instance 
    ```bash
    kubectl apply -f argocd\\argocd-instance.yaml
    ```
4. Login ArgoCD (https://argocd.apps-crc.testing/)
    ```bash
    kubectl -n argocd get secret argocd-instance-cluster -o jsonpath='{.data.admin\.password}' | base64 -d
    ```
5. Dev namespace
    ```bash
    kubectl create namespace dev
    kubectl label namespace dev argocd.argoproj.io/managed-by=argocd
    ```
6. Deploy app-of-apps
    ```bash
    kubectl apply -f app-of-apps\\application.yaml
    ```
