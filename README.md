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

## Values
The `values.yaml` files have the following meaning:

| Parameter                            | Description                                                 | Type      | Default            |
|--------------------------------------|-------------------------------------------------------------|-----------|--------------------|
| `targetNamespaces`                   | namespaces that should be cleaned                           | `array`   | `["default"]`      |
|--------------------------------------|-------------------------------------------------------------|-----------|--------------------|
| `cronJob.schedule`                   | `CronJobSpec` for set the schedule of the CronJob           | `string`  | `@daily`           |
| `cronJob.successfulJobsHistoryLimit` | `CronJobSpec` for number of successful jobs to keep         | `integer` | `1`                |
| `cronJob.failedJobsHistoryLimit`     | `CronJobSpec` for number of failed jobs to keep             | `integer` | `1`                |
|--------------------------------------|-------------------------------------------------------------|-----------|--------------------|
| `pods.image.repository`              | `PodSpec` for the image repository                          | `string`  | `bitnami/kubectl`  |
| `pods.image.tag`                     | `PodSpec` for overwriting the image tag                     | `string`  | Chart `appVersion` |
| `pods.image.pullPolicy`              | `PodSpec` for the image pull policy                         | `string`  | `IfNotPresent`     |
| `pods.restartPolicy`                 | `PodSpec` for pod restarting policy on failure              | `string`  | `OnFailure`        |
| `pods.resources`                     | `PodSpec` for resource request and limit for CPU and memory | `map`     | See `values.yaml`  |
| `pods.seurityContext`                | `PodSpec` for defining security context of the pod          | `map`     | See `values.yaml`  |
| `pods.annotations`                   | `PodSpec` for defining annotations of the pod               | `map`     | `{}`               |
| `pods.nodeSelector`                  | `PodSpec` for defining nodeSelector to deploy the pod on    | `map`     | `{}`               |
| `pods.tolerations`                   | `PodSpec` for defining tolerations to deploy the pod on     | `array`   | `[]`               |
| `pods.affinity`                      | `PodSpec` for defining affinity to deploy the pod on        | `map`     | `{}`               |
