````markdown
# 🚀 Kubernetes Setup on Ubuntu

This guide walks you through installing **Docker**, **kubectl**, and **Minikube** on **Ubuntu**, along with a full cleanup/uninstallation process.

---

## ✅ 1. Install Docker on Ubuntu

**Update package lists**
```bash
sudo apt update
````

**Install Docker Engine**

```bash
sudo apt install docker.io -y
```

**Start Docker service**

```bash
sudo systemctl start docker
```

**Enable Docker to start at boot**

```bash
sudo systemctl enable docker
```

---

## ✅ 2. Add User to Docker Group (Run Docker Without `sudo`)

**Create docker group (if it doesn’t exist)**

```bash
sudo groupadd docker
```

**Add your user to docker group**

```bash
sudo usermod -aG docker $USER
```

**Apply group changes**

Option 1: Logout and login again
Option 2:

```bash
newgrp docker
```

---

## ✅ 3. Install Kubernetes Dependencies

**Install required packages**

```bash
sudo apt install -y apt-transport-https ca-certificates curl
```

**Add Kubernetes GPG key**

```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

**Add Kubernetes APT repository**

```bash
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

---

## ✅ 4. Install kubectl (Using Snap)

**Install kubectl**

```bash
sudo snap install kubectl --classic
```

**Verify installation**

```bash
kubectl version --client
```

---

## ✅ 5. Install Minikube

**Download Minikube binary**

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

**Install Minikube**

```bash
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

**Verify installation**

```bash
minikube version
```

---

## ✅ 6. Start Minikube (Using Docker Driver)

**Start Minikube**

```bash
minikube start --driver=docker
```

**If permission issues occur**

```bash
minikube start --driver=docker --force
```

---

## ✅ 7. Basic Kubernetes Commands

| Command                | Description               |
| ---------------------- | ------------------------- |
| `minikube status`      | Check cluster status      |
| `kubectl cluster-info` | Display cluster info      |
| `kubectl config view`  | View kubeconfig           |
| `kubectl get nodes`    | List cluster nodes        |
| `kubectl get pods`     | List running pods         |

---

## 🗑️ Uninstallation / Cleanup

### 1. Stop & Delete Minikube

```bash
minikube stop
minikube delete
```

### 2. Remove Minikube Binary

```bash
sudo rm -f /usr/local/bin/minikube
```

### 3. Remove Minikube & kubectl Configs

```bash
rm -rf ~/.minikube
rm -rf ~/.kube
```

---

## 🗑️ Remove kubectl (Snap)

```bash
sudo snap remove kubectl
```

---

## 🗑️ Remove Kubernetes APT Sources (Optional)

```bash
sudo rm -f /etc/apt/sources.list.d/kubernetes.list
sudo apt-key del "$(apt-key list | grep -B 1 'Google Cloud Packages' | head -n 1 | awk '{print $2}')"
sudo apt update
```

---

## ✅ Verify Cleanup

```bash
which minikube
which kubectl
```

> Both commands should return **no output** if uninstalled successfully.

```

