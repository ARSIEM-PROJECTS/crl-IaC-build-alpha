# crl-IaC-build-alpha project

This project should be hosted using Kubernetes or a similar container orchestation platform which is vendor neutral. Git may then be used to share repositories such as Gitlab, Github and other git platforms to be branched containing some form of CI/CD which automates the building of applications such as Gitlab runners, Github Actions or self hosted Jenkins. Repositories may use IaC tools such as Terraform, Ansible or whatever is needed for building applications or simply use the CI/CD process to complete application builds. Each repository should have the required Github [SECRET](https://docs.github.com/en/actions/security-guides/encrypted-secrets) or Gitlab external [SECRETS](https://docs.gitlab.com/ee/ci/secrets/), or other methods to allow authentication the the platform hosting Kubernetes such as Azure, AWS or other cloud provider and have the needed [credentials](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/) for the `~\.kube\config` as shown below. 

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




