# crl-IaC-build-alpha project

Developing IaC method to automate the creation of linux containers when needed for range utilizing Github Actions. 

## Building Azure Kubernetes Service (AKS) for hosting linux containerized cyber range

* [quick-kubernetes-deploy-cli](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli)
* [manage-resource-groups-cli](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli)

### AKS Resource group

The purpose of using AKS for the building of a cyber range is to use Kubernetes orchestation which could later be migrated to other cloud architectures if needed such as AWS. This effort allows builds to be vendor neutral. 

```bash
az group create --name AKSResourceGroup --location eastus
```

To later retrieve information on this created resource group use the following command:

```bash
az group show --resource-group AKSResourceGroup
```

If this group needs to be deleted later use the following command:

```bash
az group delete --name exampleGroup

```

### AKS Cluster
* [Kubernetes Cluster Intro](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/)

Create a cluster

```bash
az aks create -g AKSResourceGroup -n myAKSCluster --enable-managed-identity --node-count 1 --enable-addons monitoring --enable-msi-auth-for-monitoring  --generate-ssh-keys

```
#### Stopping and Starting Kubernetes Cluster with az cli

```bash

az aks stop --name myAKSCluster --resource-group AKSResourceGroup
```

```bash
 az aks show --name myAKSCluster --resource-group AKSResourceGroup | grep powerState -A 2
```



### Install kubectl for managing Kubernetes

```bash
az aks install-cli

```

### Get credentials for connecting to Cluster
Grab credentials for kubectl authentication which will be saved to `~/.kube/config` on your local computer.

```bash
 az aks get-credentials --resource-group AKSResourceGroup --name myAKSCluster
```

### kubectl
* [kubectl ref](https://kubernetes.io/docs/reference/kubectl/)

```bash
kubectl get nodes
```




