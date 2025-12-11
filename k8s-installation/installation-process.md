🚀 Complete Kubernetes Setup on Ubuntu (Docker, kubectl, Minikube)This guide walks you through the complete process of installing Docker, kubectl, and Minikube on Ubuntu 20.04/22.04, followed by a thorough cleanup/uninstallation procedure.🛠️ I. Prerequisites & Initial SetupBefore starting, ensure your system is up-to-date.1. Update PackagesBashsudo apt update
sudo apt upgrade -y
2. Install Required DependenciesBashsudo apt install -y apt-transport-https ca-certificates curl gnupg
🐳 II. Docker Installation and Configuration (Container Runtime)Docker will serve as the container runtime for Minikube.1. Install Docker EngineBash# Install Docker Engine
sudo apt install docker.io -y

# Start and enable Docker service
sudo systemctl start docker
sudo systemctl enable docker
2. Configure Docker Access (Run Without sudo)Adding your user to the docker group allows you to run Docker commands without prepending sudo.Bash# Add your user to the docker group
sudo usermod -aG docker $USER

# Apply the group change without logging out (recommended)
newgrp docker
Note: You may need to log out and log back in for these changes to take full effect in all terminal sessions.⎈ III. Kubernetes Tools Installation (kubectl & Minikube)These tools are essential for managing and running your local Kubernetes cluster.1. Install kubectl (Kubernetes Command-Line Tool)We'll use Snap for a quick and reliable installation of kubectl.Bash# Install kubectl via Snap
sudo snap install kubectl --classic

# Verify installation
kubectl version --client
2. Install Minikube (Local Kubernetes Cluster)Minikube sets up a single-node cluster environment, perfect for development and learning.Bash# Download the Minikube binary
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# Install Minikube to your system path
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Verify installation
minikube version
▶️ IV. Start the Local Kubernetes ClusterWe will start Minikube using the Docker driver.1. Start Minikube ClusterThe --driver=docker option tells Minikube to use Docker as the Virtual Machine/Host environment.Bashminikube start --driver=docker
Tip: If you encounter permission issues (especially right after the Docker group change), you might need to use minikube start --driver=docker --force temporarily, but ensure the Docker group change is properly applied afterward.2. Cluster OverviewOnce the cluster is running, kubectl automatically uses the configuration provided by Minikube.💻 V. Basic Operations and Management1. Key Status CommandsCommandDescriptionminikube statusCheck the current status of the Minikube VM/Cluster.kubectl get nodesList the nodes in the cluster (Minikube will show one).kubectl cluster-infoDisplay connection details for the master and services.kubectl config viewView the generated kubeconfig file details.2. Access the Kubernetes DashboardMinikube provides a convenient way to launch the Web UI.Bashminikube dashboard
This command will automatically open the Kubernetes Dashboard in your web browser.🗑️ VI. Complete Uninstallation and CleanupFollow these steps to fully remove Minikube, kubectl, and Docker components.1. Stop and Delete Minikube ClusterAlways stop and delete the cluster first to free resources.Bashminikube stop
minikube delete
2. Remove Minikube and kubectl FilesBash# Remove Minikube binary
sudo rm -f /usr/local/bin/minikube

# Remove kubectl installed via Snap
sudo snap remove kubectl

# Remove local configuration directories
rm -rf ~/.minikube ~/.kube
3. Remove Docker Engine (Optional)If you wish to remove Docker completely:Bash# Stop and disable Docker service
sudo systemctl stop docker
sudo systemctl disable docker

# Uninstall Docker packages
sudo apt purge docker.io -y

# Remove the docker group and configuration (optional)
sudo groupdel docker
rm -rf /var/lib/docker
4. Final VerificationCheck if the binaries are still present.Bashwhich minikube
which kubectl
Expected Output: Both commands should return no output if the cleanup was successful.
