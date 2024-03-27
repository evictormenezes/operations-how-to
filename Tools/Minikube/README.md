# Setting Up Kubernetes on WSL2

This guide walks you through setting up Kubernetes on your local system using WSL2, Docker, Minikube, and Kubectl. By following these steps, you'll be able to run Kubernetes locally, enabling you to test and develop against a Kubernetes environment on your own machine.
---
## Table of Contents

- [List Available Distros](#list-available-distros)
- [Install Ubuntu](#install-ubuntu)
- [Enable systemd for WSL2](#enable-systemd-for-wsl2)
- [Installing Docker](#installing-docker)
- [Install Minikube](#install-minikube)
- [Install Kubectl](#install-kubectl)
- [Running Minikube](#running-minikube)
- [Conclusion](#conclusion)
---
## List Available Distros

Before starting, let's check the available Linux distributions that can be installed with WSL2.
```
    powershell: wsl --list --online
```

## Install Ubuntu

In this guide, we will use Ubuntu. Install it using the following command:
```
    powershell: wsl --install -d Ubuntu
```

## Enable systemd for WSL2

Systemd needs to be enabled for WSL2. Here's how:

1. Open the WSL configuration file.
```
    powershell: sudo vi /etc/wsl.conf
```

2. Ensure the file contains the following:
```
    [boot]
    systemd=true
```

3. If changes were made, restart WSL2:
```
    powershell: wsl --shutdown
    powershell: wsl
```

## Installing Docker
```
    $ sudo apt update && sudo apt upgrade -y
    $ sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    $ sudo apt-get update -y
    $ sudo apt-get install -y docker-ce
    $ sudo usermod -aG docker $USER && newgrp docker
```

## Install Minikube

### Download the latest Minikube
```
    $ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

### Make it executable
```
    $ chmod +x ./minikube
```

### Move it to your user's executable PATH
```
    $ sudo mv ./minikube /usr/local/bin/
```

### Set the driver version to Docker
```
    $ minikube config set driver docker
```

## Install Kubectl

### Download the latest Kubectl
```
    $ curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

### Make it executable
```
    $ chmod +x ./kubectl
```

### Move it to your user's executable PATH
```
    $ sudo mv ./kubectl /usr/local/bin/
```

## Running Minikube
```
    $ minikube start
    $ kubectl config use-context minikube
    $ minikube start
    $ kubectl get pods -A
```

You have successfully installed and configured Kubernetes on the local system using WSL2.
