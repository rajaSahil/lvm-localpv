
#  OpenEBS LocalPV Provisioner

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
![Chart Lint and Test](https://github.com/openebs/lvm-localpv/workflows/Chart%20Lint%20and%20Test/badge.svg)
![Release Charts](https://github.com/openebs/lvm-localpv/workflows/Release%20Charts/badge.svg?branch=develop)

A Helm chart for openebs lvm localpv provisioner. This chart bootstraps OpenEBS LVM LocalPV provisioner deployment on a [Kubernetes](http://kubernetes.io) cluster using the  [Helm](https://helm.sh) package manager.


**Homepage:** <http://www.openebs.io/>

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| pawanpraka1 | pawan@mayadata.io |  |
| prateekpandey14 | prateek.pandey@mayadata.io |  |
| iyashu | yashpal.c1995@gmail.com |  |


## Get Repo Info

```console
helm repo add openebs-lvmlocalpv https://openebs.github.io/lvm-localpv
helm repo update
```

_See [helm repo](https://helm.sh/docs/helm/helm_repo/) for command documentation._

## Install Chart

Please visit the [link](https://openebs.github.io/lvm-localpv/) for install instructions via helm3.

```console
# Helm
$ helm install [RELEASE_NAME] openebs-lvmlocalpv/lvm-localpv
```

**Note:** If moving from the operator to helm
- Make sure the namespace provided in the helm install command is same as `LVM_NAMESPACE` (by default it is `openebs`) env in the controller statefulset.
- Before installing, clean up the stale statefulset and daemonset from `kube-system` namespace using the below commands
```sh
kubectl delete sts openebs-lvm-controller -n kube-system
kubectl delete ds openebs-lvm-node -n kube-system
```


_See [configuration](#configuration) below._

_See [helm install](https://helm.sh/docs/helm/helm_install/) for command documentation._

## Uninstall Chart

```console
# Helm
$ helm uninstall [RELEASE_NAME]
```

This removes all the Kubernetes components associated with the chart and deletes the release.

_See [helm uninstall](https://helm.sh/docs/helm/helm_uninstall/) for command documentation._

## Upgrading Chart

```console
# Helm
$ helm upgrade [RELEASE_NAME] [CHART] --install
```

## Configuration

The following table lists the configurable parameters of the OpenEBS LVM Localpv chart and their default values.

| Parameter| Description| Default|
| -| -| -|
| `imagePullSecrets`| Provides image pull secrect| `""`|
| `lvmPlugin.image.registry`| Registry for openebs-lvm-plugin image| `""`|
| `lvmPlugin.image.repository`| Image repository for openebs-lvm-plugin| `openebs/lvm-driver`|
| `lvmPlugin.image.pullPolicy`| Image pull policy for openebs-lvm-plugin| `IfNotPresent`|
| `lvmPlugin.image.tag`| Image tag for openebs-lvm-plugin| `0.5.0`|
| `lvmNode.driverRegistrar.image.registry`| Registry for csi-node-driver-registrar image| `k8s.gcr.io/`|
| `lvmNode.driverRegistrar.image.repository`| Image repository for csi-node-driver-registrar| `sig-storage/csi-node-driver-registrar`|
| `lvmNode.driverRegistrar.image.pullPolicy`| Image pull policy for csi-node-driver-registrar| `IfNotPresent`|
| `lvmNode.driverRegistrar.image.tag`| Image tag for csi-node-driver-registrar| `v1.2.0`|
| `lvmNode.updateStrategy.type`| Update strategy for lvmnode daemonset | `RollingUpdate` |
| `lvmNode.kubeletDir`| Kubelet mount point for lvmnode daemonset| `"/var/lib/kubelet/"` |
| `lvmNode.annotations` | Annotations for lvmnode daemonset metadata| `""`|
| `lvmNode.podAnnotations`| Annotations for lvmnode daemonset's pods metadata | `""`|
| `lvmNode.resources`| Resource and request and limit for lvmnode daemonset containers | `""`|
| `lvmNode.labels`| Labels for lvmnode daemonset metadata | `""`|
| `lvmNode.podLabels`| Appends labels to the lvmnode daemonset pods| `""`|
| `lvmNode.nodeSelector`| Nodeselector for lvmnode daemonset pods| `""`|
| `lvmNode.tolerations` | lvmnode daemonset's pod toleration values | `""`|
| `lvmNode.securityContext` | Security context for lvmnode daemonset container | `""`|
| `lvmController.resizer.image.registry`| Registry for csi-resizer image| `k8s.gcr.io/`|
| `lvmController.resizer.image.repository`| Image repository for csi-resizer| `sig-storage/csi-resizer`|
| `lvmController.resizer.image.pullPolicy`| Image pull policy for csi-resizer| `IfNotPresent`|
| `lvmController.resizer.image.tag`| Image tag for csi-resizer| `v1.1.0`|
| `lvmController.snapshotter.image.registry`| Registry for csi-snapshotter image| `k8s.gcr.io/`|
| `lvmController.snapshotter.image.repository`| Image repository for csi-snapshotter| `sig-storage/csi-snapshotter`|
| `lvmController.snapshotter.image.pullPolicy`| Image pull policy for csi-snapshotter| `IfNotPresent`|
| `lvmController.snapshotter.image.tag`| Image tag for csi-snapshotter| `v4.0.0`|
| `lvmController.snapshotController.image.registry`| Registry for snapshot-controller image| `k8s.gcr.io/`|
| `lvmController.snapshotController.image.repository`| Image repository for snapshot-controller| `sig-storage/snapshot-controller`|
| `lvmController.snapshotController.image.pullPolicy`| Image pull policy for snapshot-controller| `IfNotPresent`|
| `lvmController.snapshotController.image.tag`| Image tag for snapshot-controller| `v4.0.0`|
| `lvmController.provisioner.image.registry`| Registry for csi-provisioner image| `k8s.gcr.io/`|
| `lvmController.provisioner.image.repository`| Image repository for csi-provisioner| `sig-storage/csi-provisioner`|
| `lvmController.provisioner.image.pullPolicy`| Image pull policy for csi-provisioner| `IfNotPresent`|
| `lvmController.provisioner.image.tag`| Image tag for csi-provisioner| `v2.1.0`|
| `lvmController.updateStrategy.type`| Update strategy for lvm localpv controller statefulset | `RollingUpdate` |
| `lvmController.annotations` | Annotations for lvm localpv controller statefulset metadata| `""`|
| `lvmController.podAnnotations`| Annotations for lvm localpv controller statefulset's pods metadata | `""`|
| `lvmController.resources`| Resource and request and limit for lvm localpv controller statefulset containers | `""`|
| `lvmController.labels`| Labels for lvm localpv controller statefulset metadata | `""`|
| `lvmController.podLabels`| Appends labels to the lvm localpv controller statefulset pods| `""`|
| `lvmController.nodeSelector`| Nodeselector for lvm localpv controller statefulset pods| `""`|
| `lvmController.tolerations` | lvm localpv controller statefulset's pod toleration values | `""`|
| `lvmController.securityContext` | Seurity context for lvm localpv controller statefulset container | `""`|
| `rbac.pspEnabled` | Enable PodSecurityPolicy | `false` |
| `serviceAccount.lvmNode.create` | Create a service account for lvmnode or not| `true`|
| `serviceAccount.lvmNode.name` | Name for the lvmnode service account| `openebs-lvm-node-sa`|
| `serviceAccount.lvmController.create` | Create a service account for lvm localpv controller or not| `true`|
| `serviceAccount.lvmController.name` | Name for the lvm localpv controller service account| `openebs-lvm-controller-sa`|
| `analytics.enabled` | Enable or Disable google analytics for the controller| `true`|

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
helm install <release-name> -f values.yaml openebs/lvm-localpv
```

> **Tip**: You can use the default [values.yaml](values.yaml)
