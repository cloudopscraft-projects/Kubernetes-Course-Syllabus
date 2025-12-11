🚀 Kubernetes Setup on Ubuntu (Docker, kubectl, Minikube)

This guide explains how to install Docker, kubectl, and Minikube on Ubuntu, along with explanations for each step and clean uninstall instructions.

✅ 1. Install Docker on Ubuntu
Update package lists
sudo apt update


Refreshes local package index and ensures latest versions.

Install Docker Engine
sudo apt install docker.io -y


Installs Docker from Ubuntu’s repository.

Start Docker service
sudo systemctl start docker

Enable Docker at system boot
sudo systemctl enable docker

✅ 2. Add User to Docker Group (Run Docker Without sudo)
Create docker group (if it doesn’t exist)
sudo groupadd docker

Add your user to docker group
sudo usermod -aG docker $USER

Apply new group membership

Option 1: Logout & Login
Option 2:

newgrp docker

✅ 3. Install Kubernetes Dependencies
Install required packages
sudo apt install -y apt-transport-https ca-certificates curl

Add Kubernetes GPG key
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

Add Kubernetes APT repository
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" \
| sudo tee /etc/apt/sources.list.d/kubernetes.list

✅ 4. Install kubectl (Using Snap)
Install kubectl
sudo snap install kubectl --classic

Verify installation
kubectl version --client

✅ 5. Install Minikube
Download Minikube binary
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

Install Minikube
sudo install minikube-linux-amd64 /usr/local/bin/minikube

Verify version
minikube version

✅ 6. Start Minikube (Using Docker Driver)
Start Minikube
minikube start --driver=docker

If you face permission issues
minikube start --driver=docker --force

✅ 7. Basic Kubernetes Commands
Check cluster status
minikube status

Cluster information
kubectl cluster-info

View kubeconfig
kubectl config view

List nodes
kubectl get nodes

List pods
kubectl get pods

Open Kubernetes Dashboard
minikube dashboard

🗑️ Uninstall / Cleanup Guide
1. Stop Minikube
minikube stop
minikube delete

2. Remove Minikube binary
sudo rm -f /usr/local/bin/minikube

Delete Minikube & kube config
rm -rf ~/.minikube
rm -rf ~/.kube

🗑️ Remove kubectl (Snap)
sudo snap remove kubectl

🗑️ Remove Kubernetes APT sources (Optional)
sudo rm -f /etc/apt/sources.list.d/kubernetes.list
sudo apt-key del "$(apt-key list | grep -B 1 'Google Cloud Packages' | head -n 1 | awk '{print $2}')"
sudo apt update

✅ Verification After Cleanup
which minikube
which kubectl


Both commands should return nothing if uninstalled successfully.
