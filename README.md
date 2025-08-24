# Kubernetes-Homelab
This repository contains yaml resources ready to be applied in the cluster, hence 
resources on the cluster are tracked and versioned just like plain old software.

### Prerequisites
In order to setup an identical copy of this cluster on your own premises, please, make 
sure to follow these instructions (linux, ubuntu) or to adapt them to your environment.

#### Installing kubectl, k3s
You should be able to install **k3s**, **kubectl** and start your local cluster
by running the following commands, as long as you have a linux distribution
that supports snapcraft (canonical package manager).
```bash
sudo snap install kubectl --classic
curl -sfL https://get.k3s.io/ | sh -
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $(id -u):$(id -g) ~/.kube/config
sudo systemctl enable k3s
```

#### Installing helm, flux
**Helm** is the package manager for kubernetes, and will allow you to donwload and install 
existing ready-to-deploy solutions called "charts". In order to treat helm installations
just like any other resource on the cluster, we will use **flux**, which is an extension for 
kubernetes that allows it to work with custom objects designed to model helm events just 
like `helm install`, `helm upgrade` etc...
```
sudo snap install helm --classic
sudo snap install flux --classic
flux install
```