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

Things to note:
- AppProjects place some restrictions on which repositories can be deployed to which clusters and namespaces and some other features (like sync windows).
- ArgoCD comes with an AppProject `default`; any application without an explicit `project` attribute in its spec will be placed here. This AppProject does not impose any restrictions.
- ArgoCD is - by OpenShift's default operator setup - not allowed to create cluster-level resources such as namespaces. Hence you either need to change that setting (out of scope for this documentation) or manually create such resources (e.g. using `oc new-project` which creates a namespace).

## Deploy an ArgoCD Application in an AppProject

```bash
# Create the OC project & namespace
oc new-project hello
# Create the AppProject called "demo"
kubectl apply -f argocd/proj-demo.yaml
# Add the application "hello", which is a part of that project
kubectl apply -f argocd/app-hello.yaml
```

You can follow the creation of the resources in [ArgoCD](https://argocd.apps-crc.testing/applications/argocd/hello?view=tree&resource=), in the event console (`kubectl get events -A -w`) or in the [OpenShift Cluster Console](https://console-openshift-console.apps-crc.testing/k8s/ns/hello/apps~v1~Deployment). 
As soon as the pods are stable, you should be able to get responses from different pods under [hello.apps-crc.testing](https://hello.apps-crc.testing/).

