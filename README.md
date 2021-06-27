
# Vagrantfile and Scripts to Automate Kubernetes Setup using Kubeadm

### The Vagrant file and the scripts are forked from https://github.com/scriptcamp/vagrant-kubeadm-kubernetes.git. I thank the team for the setup and found that this is best and easy setup

>## Documentation

Refer this link for documentation: https://devopscube.com/kubernetes-cluster-vagrant/


>## Prerequisites

### System Requirements
1. Working Vagrant setup
2. 8 Gig + RAM workstation as the Vms use 3 vCPUS and 4+ GB RAM

### Software Requirements
1. Oracle Virtual Box (This is required in case of Windows 10 Home. For other editions of Windows, Hyper-V can be configured) - https://www.virtualbox.org/
2. Vagrant - https://www.vagrantup.com/
 
>## Usage/Examples

To provision the cluster, execute the following commands.

```shell
git clone https://github.com/aruns1975/kubernates.git

cd kubernetes

git checkout vagrant-from-start

vagrant up
```
> Virtual machines details
- master-node (10.0.0.10)
- worker-node01 (10.0.0.11)
- worker-node02 (10.0.0.12)

> ##Install kubectl on the localmachine

- https://kubernetes.io/docs/tasks/tools/
- https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

>## Configure kubectl to access the vagrant kubernetes cluster just created.

```shell
cd configs
export KUBECONFIG=$(PWD)/config
```

or you can copy the config file to .kube directory.
 - For linux
```shell
cp config ~/.kube/
```
- For windows
```batch
copy config %HOME%/.kube/
```

>## Kubernetes Dashboard URL

https://10.0.0.10:30002/


>## Kubernetes login token

Vagrant up will create the admin user token and saves in the configs directory.

```shell
cd vagrant-kubeadm-kubernetes
cd configs
cat token
```
>## It also deploys a sample nginx server

http://10.0.0.10:30003

>## To setup the load balancer (wo ingress controller), please follow the steps from the following url

- https://metallb.universe.tf/installation/
- https://metallb.universe.tf/configuration/
- https://metallb.universe.tf/usage/


>## To shutdown the cluster, 

```shell
vagrant halt
```

>## To restart the cluster,

```shell
vagrant up
```

>## To destroy the cluster, 

```shell
vagrant destroy -f
```

>## More websites
```
https://www.itwonderlab.com/en/ansible-kubernetes-vagrant-tutorial/
https://www.itwonderlab.com/en/installating-kubernetes-dashboard/
```
