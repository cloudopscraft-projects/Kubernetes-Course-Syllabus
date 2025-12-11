Here’s a clean and well-structured **README.md** version of your Kubernetes setup guide. It includes proper markdown formatting, headings, and syntax highlighting for readability.  

***

```markdown
# 🚀 Kubernetes Setup on Ubuntu

This guide walks you through installing **Docker**, **kubectl**, and **Minikube** on **Ubuntu**, along with a full cleanup/uninstallation process.

---

## ✅ 1. Install Docker on Ubuntu

**Update package lists**
```
sudo apt update
```

**Install Docker Engine**
```
sudo apt install docker.io -y
```

**Start Docker service**
```
sudo systemctl start docker
```

**Enable Docker to start at boot**
```
sudo systemctl enable docker
```

---

## ✅ 2. Add User to Docker Group (Run Docker Without `sudo`)

**Create docker group (if it doesn’t exist)**
```
sudo groupadd docker
```

**Add your user to docker group**
```
sudo usermod -aG docker $USER
```

**Apply group changes**
- Option 1: Logout and login again  
- Option 2:
  ```
  newgrp docker
  ```

---

## ✅ 3. Install Kubernetes Dependencies

**Install required packages**
```
sudo apt install -y apt-transport-https ca-certificates curl
```

**Add Kubernetes GPG key**
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

**Add Kubernetes APT repository**
```
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

---

## ✅ 4. Install kubectl (Using Snap)

**Install kubectl**
```
sudo snap install kubectl --classic
```

**Verify installation**
```
kubectl version --client
```

---

## ✅ 5. Install Minikube

**Download Minikube binary**
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

**Install Minikube**
```
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

**Verify installation**
```
minikube version
```

---

## ✅ 6. Start Minikube (Using Docker Driver)

**Start Minikube**
```
minikube start --driver=docker
```

**If permission issues occur**
```
minikube start --driver=docker --force
```

---

## ✅ 7. Basic Kubernetes Commands

| Command | Description |
|----------|--------------|
| `minikube status` | Check cluster status |
| `kubectl cluster-info` | Display cluster info |
| `kubectl config view` | View kubeconfig |
| `kubectl get nodes` | List cluster nodes |
| `kubectl get pods` | List running pods |
| `minikube dashboard` | Open Kubernetes Dashboard |

---

## 🗑️ Uninstallation / Cleanup

### 1. Stop & Delete Minikube
```
minikube stop
minikube delete
```

### 2. Remove Minikube Binary
```
sudo rm -f /usr/local/bin/minikube
```

### 3. Remove Minikube & kubectl Configs
```
rm -rf ~/.minikube
rm -rf ~/.kube
```

---

## 🗑️ Remove kubectl (Snap)
```
sudo snap remove kubectl
```

---

## 🗑️ Remove Kubernetes APT Sources (Optional)
```
sudo rm -f /etc/apt/sources.list.d/kubernetes.list
sudo apt-key del "$(apt-key list | grep -B 1 'Google Cloud Packages' | head -n 1 | awk '{print $2}')"
sudo apt update
```

---

## ✅ Verify Cleanup
```
which minikube
which kubectl
```
> Both commands should return **no output** if uninstalled successfully.

---

## 🧩 Notes
- Ensure **Virtualization** is enabled in BIOS for Minikube.  
- If using **VM-based drivers**, consider installing `virtualbox` or `qemu`.  
- Make sure your user has access to Docker without `sudo` before running Minikube.

---
```

***

Would you like me to include a **table of contents** with links for quick navigation inside the README?
