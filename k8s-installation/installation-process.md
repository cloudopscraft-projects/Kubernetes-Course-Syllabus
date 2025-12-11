1. Install Docker on Ubuntu
Update package lists
sudo apt update

Install Docker Engine
sudo apt install docker.io -y

Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker

2. Run Docker Without sudo
Create Docker group (if not already present)
sudo groupadd docker

Add your user to the Docker group
sudo usermod -aG docker $USER

Apply the new group membership

Log out and log back in, or run:

newgrp docker

3. Install Kubernetes Dependencies
Install required packages
sudo apt install -y apt-transport-https ca-certificates curl

Add Kubernetes GPG key
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

Add Kubernetes APT repository
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | \
sudo tee /etc/apt/sources.list.d/kubernetes.list

4. Install kubectl (Snap Method)
Install kubectl
sudo snap install kubectl --classic

Verify installation
kubectl version --client

5. Install Minikube
Download Minikube binary
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

Install Minikube
sudo install minikube-linux-amd64 /usr/local/bin/minikube

Verify installation
minikube version

6. Start Minikube (Using Docker Driver)
Start Minikube
minikube start --driver=docker

If permission issues occur
minikube start --driver=docker --force

7. Basic Kubernetes Commands
Description	Command
Check Minikube status	minikube status
Cluster information	kubectl cluster-info
View kubeconfig	kubectl config view
List nodes	kubectl get nodes
List pods	kubectl get pods
Open Kubernetes Dashboard	minikube dashboard
Uninstall / Cleanup
Stop and delete Minikube
minikube stop
minikube delete

Remove Minikube binary
sudo rm -f /usr/local/bin/minikube

Remove Minikube & kube config directories
rm -rf ~/.minikube
rm -rf ~/.kube

Remove kubectl (Snap)
sudo snap remove kubectl

Remove Kubernetes APT sources (optional)
sudo rm -f /etc/apt/sources.list.d/kubernetes.list
sudo apt-key del "$(apt-key list | grep -B 1 'Google Cloud Packages' | head -n 1 | awk '{print $2}')"
sudo apt update

Verify Cleanup
which minikube
which kubectl


If both commands return nothing, uninstall was successful.
