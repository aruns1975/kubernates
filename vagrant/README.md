# The vagrant image created with the image of ubuntu 20.4 LTS and kubectl, kubeadm, kubelet and docker-ce

## to use the vagrant, download oracle virtual vox and vagrant

> Creating the Master and worker 

### Create folder kubernetes-setup
### Copy the vagrantfile to the kubernetes-setup folder
### From the folder kubernetes-setup run vagrant up
#### This creates three image files in the name of kubernetes-server, kubernetes-worker1 and kubernetes-worker2
### Login into kubernetes-server using the following command
>  To start the kubernestes server
```
sudo kubeadm init --pod-network-cidr=192.168.29.0/24 --apiserver-advertise-address=192.168.29.100
```
> Copy the kubeadm join command generated from the previous steps

> Run the steps provided during the execution of the previous steps
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

> To setup the network
```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

> Incase if the kubectl join command is not copied or lost, use the below command
```
kubeadm token create --print-join-command
```
> Use kubectl get nodes to check the nodes
```
kubectl get nodes
```
> From the worker nodes issues the kubeadm join command

> TO install the dash board
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.2.0/aio/deploy/recommended.yaml
```


# Kubernetes Installation on Ubuntu 20.04

Get the detailed information about the installation from the below-mentioned websites of **Docker** and **Kubernetes**.

[Docker](https://docs.docker.com/)

[Kubernetes](https://kubernetes.io/)

### Set up the Docker and Kubernetes repositories:

> Download the GPG key for docker

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

> Add the docker repository

```bash
# Docker has release the repository for Ubuntu 20.04 Focal LTS.
# we can get the latest release versions from https://docs.docker.com

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

```

> Add the GPG key for kubernetes

```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

> Add the kubernetes repository

**Check for the latest release in https://packages.cloud.google.com/apt/dists**

```bash
cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

> Update the repository

```bash
# Update the repositiries
sudo apt-get update
```

> Install Docker and Kubernetes packages.

**Note that if you want to use a newer version of Kubernetes, change the version installed for kubelet, kubeadm, and kubectl and be sure that all three use the same version.
These version should support the Docker CE version.**

```bash
# Use the same versions to avoid issues with the installation.
sudo apt-get install -y docker-ce=5:20.10.7~3-0~ubuntu-$(lsb_release -cs) kubelet=1.21.1-00 kubeadm=1.21.1-00 kubectl=1.21.1-00
```


> To hold the versions so that the versions will not get accidently upgraded.

```bash
sudo apt-mark hold docker-ce kubelet kubeadm kubectl
```

> Enable the iptables bridge

```bash
#Set a value in the sysctl file , to allow proper network settings for Kubernetes on all the servers.
echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf

#To make the changes to take immediate effect for the iptables
sudo sysctl -p
```


