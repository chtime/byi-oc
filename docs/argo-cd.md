# Prerequisites

1. Using the cluster admin credentials, login and browse to the operators
2. Install the [ArgoCD Operator](https://console-openshift-console.apps-crc.testing/operatorhub/all-namespaces?keyword=argocd&details-item=argocd-operator-community-operators-openshift-marketplace&channel=alpha&version=0.8.0)

# Usage

You can also refer to the official [operator examples on GitHub](https://github.com/argoproj-labs/argocd-operator).

```bash
oc new-project hello
kubectl apply -f https://github.com/chtime/byi-oc/argocd/hello/argo-app.yaml
```
