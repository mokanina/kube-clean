# kube-clean
Helm chart deploying cronjob that cleans failed pods in specified namespaces. It was
inspired from the following [discussion/answer](https://stackoverflow.com/a/72872547/15045604)
in stackoverflow.


## Prerequisites
- Before you can install the `kube-clean` chart make sure that you have:
  - `helm` version 3 installed on your machine (see also [Installing Helm](https://helm.sh/docs/intro/install/).
  - [Optional] `kubectl` in order to verify that pods are running.

## Installation
In order to release the `kube-clean` helm chart in a dedicated namespace simply run:
```bash
cd /path/to/kube-clean/
helm install kube-clean ./ --namespace=kube-clean --create-namespace --debug
```

After the installation is verify your release with
```bash
helm list -n kube-clean
```
or
```bash
kubectl -n kube-clean get all
```