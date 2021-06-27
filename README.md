
# Vagrantfile and Scripts to Automate Kubernetes Setup using Kubeadm

### The Vagrant file and the scripts are forked from https://github.com/scriptcamp/vagrant-kubeadm-kubernetes.git. I thank the team for the setup and found that this is best and easy setup

>## Documentation

Refer this link for documentation: https://devopscube.com/kubernetes-cluster-vagrant/


>## Prerequisites

1. Working Vagrant setup
2. 8 Gig + RAM workstation as the Vms use 3 vCPUS and 4+ GB RAM
 
>## Usage/Examples

To provision the cluster, execute the following commands.

```shell
git clone https://github.com/aruns1975/vagrant-kubeadm-kubernetes.git
cd vagrant-kubeadm-kubernetes
vagrant up
```

>## Set Kubeconfig file varaible.

```shell
cd vagrant-kubeadm-kubernetes
cd configs
export KUBECONFIG=$(PWD)/config
```

or you can copy the config file to .kube directory.

```shell
cp config ~/.kube/
```

>## Kubernetes Dashboard URL

```shell
https://10.0.0.10:30002/
```

>## Kubernetes login token

Vagrant up will create the admin user token and saves in the configs directory.

```shell
cd vagrant-kubeadm-kubernetes
cd configs
cat token
```
>## It also deploys a sample nginx server

```
http://10.0.0.10:30003
```
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
