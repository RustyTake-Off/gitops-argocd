# gitops-argocd

Remember to look around all the folders, files and change things to your own liking.

## [Projects](https://github.com/RustyTake-Off/projects)

Create a cluster, bootstrap [ArgoCD](https://argo-cd.readthedocs.io/) and see how GitOps works with this tool.

## Prerequisites

* GitHub Repository

* Kubernetes Cluster ([Kind](https://kind.sigs.k8s.io/), [Minikube](https://minikube.sigs.k8s.io/), AKS or other)

## Install ArgoCD

Install ArgoCD with bellow command.

```bash
kubectl apply -k ./argocd/base
```

or

```bash
kubectl create namespace argocd
```

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

## Create projects and applications

You can create projects and applications by logging in to ArgoCD and doing it manually, you can also do declaratively.

Files under **argocd directory** create projects and applications.

Run bellow command to apply them.

```bash
kubectl apply -k ./deployments/applications/base
```

## Log into the ArgoCD server

Create a port-forward like so:

```bash
kubectl port-forward -n argocd service/argocd-server 8080:443
```

Open <https://localhost:8080/> in your browser.

Get the secret that stores the password and decode it with the bellow command.

```bash
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 --decode
```
