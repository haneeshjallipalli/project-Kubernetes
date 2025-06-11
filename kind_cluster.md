### 🔧 **1. Install Prerequisites**

#### a. **Install `kind`**

```bash
# Linux/macOS:
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# macOS with Homebrew:
brew install kind
```

#### b. **Install `kubectl`**

```bash
# Download latest version:
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Make it executable and move to path:
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

> 🧪 Verify installation:

```bash
kind version
kubectl version --client
```

---

### 🚀 **2. Create a Kubernetes Cluster using `kind`**

```bash
kind create cluster --name my-cluster
```

Optional: Create with custom config (e.g., multi-node cluster):

```yaml
# kind-config.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
```

```bash
kind create cluster --name my-cluster --config kind-config.yaml
```

---

### 📋 **3. Verify Cluster Status**

```bash
kubectl cluster-info --context kind-my-cluster
kubectl get nodes
```

---

### 🧹 **4. Delete Cluster**

```bash
kind delete cluster --name my-cluster
```
