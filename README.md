# Kind Kubernetes
Befor installing the Kind application, we need to install the Docker desktop on local machine.
If you are using the Linux local machine, you can use install the Docker application as well.
After installing the Docker, need to install the Kind application.
```
# For Debian/Ubuntu
sudo apt-get update && sudo apt-get install -y kubectl

# For Red Hat/Fedora
sudo dnf install -y kubectl

# For other distributions or to use the latest version, follow instructions on the official kubectl website: https://kubernetes.io/docs/tasks/tools/install-kubectl/
--------------------

# Download the kind binary
sudo curl -Lo /usr/local/bin/kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64

# Make it executable
sudo chmod +x /usr/local/bin/kind

---------------------

kind --version



```

### 01- Create Kubernetes Cluster using Kind:

```
kind create cluster --name my-cluster
```
Getting the cluster list:

```
eksctl get clusters
eksctl delete cluster node-server
```

### 02- Create & Associate IAM OIDC Provider for the EKS Cluster:

```
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster node-server\
    --approve
```

