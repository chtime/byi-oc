# Prerequisites

1. Using the cluster admin credentials, login and browse to the operators
2. Install the [ArgoCD Operator](https://console-openshift-console.apps-crc.testing/operatorhub/all-namespaces?keyword=argocd&details-item=argocd-operator-community-operators-openshift-marketplace&channel=alpha&version=0.8.0)
    - It may be beneficial to customize the "Installed Namespace" to match ArgoCDs default documentation examples: "argocd".
    - The following examples (particularly the resource definitions straight from yaml) will also expect the namespace to be "argocd".
3. Start an ArgoCD instance, either by navigating to Operators > Installed Operators > Argo CD > Argo CD > Create ArgoCD or by deploying the following yaml:
```bash 
kubectl apply -f argocd/argocd-instance.yaml
```
4. You can follow the creation using `kubectl -n argocd get all`.
5. Eventually, you should be able to access [ArgoCDs web UI](https://argocd.apps-crc.testing).
6. Get argo's admin password:
```bash
kubectl -n argocd get secret argocd-instance-cluster -o jsonpath='{.data.admin\.password}' | base64 -d
```
7. Using this password and the user "admin" you can now login and create applications.

# Usage

You can also refer to the official [operator examples on GitHub](https://github.com/argoproj-labs/argocd-operator).



```bash
oc new-project hello
# once the operator is available, deploy an ArgoCD instance.
kubectl apply -f https://github.com/chtime/byi-oc/argocd/hello/argo-app.yaml
```
