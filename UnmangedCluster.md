# Unmanged Cluster
`unmanaged-cluster` provides single-node, static, Tanzu clusters. This cluster comes up with multiple packages like velero, harbor, fluent-bit etc([complete list](https://github.com/vmware-tanzu/community-edition/tree/main/addons/packages)).

## Setup
### Prerequisites 
- Installed Docker 
- Installed kubectl
- [Installed TCE](https://tanzucommunityedition.io/docs/v0.11/cli-installation/)

```
tanzu version
```
## Cluster Creation
```
tanzu unmanaged-cluster create CLUSTER_NAME
```
Once the above command ran it will fetch the Kind image, install kapp-controller, package repository and CNI(calico) after which cluster will up.

### Cluster version
```
tanzu unmanaged-cluster version
```
### To check the list of clusters.
```
tanzu unmanaged-cluster ls
```
### Check the pods
```
kubectl get pods -A
```
### Check the list of repositories
```
tanzu package repository list -A
```
### Available packages
```
tanzu package available list
```

## Let's Install a package 
We are installing fluent-bit which is an open source Log Processor and Forwarder which allows you to collect any data like metrics and logs from different sources.
### List down the available version for the package
```
tanzu package available list fluent-bit.community.tanzu.vmware.com
```
### Installing the package
```
tanzu package install fluent-bit --package-name fluent-bit.community.tanzu.vmware.com --version 1.7.5
```
### To see the logs Processed by Fluent bit
```
kubectl get pods -n fluent-bit 
kubectl logs pod_name -n fluent-bit
```
### Deleting the package
```
tanzu package installed delete fluent-bit
```

## Deleting the cluster
```
tanzu unmanaged-cluster delete CLUSTER_NAME
```
