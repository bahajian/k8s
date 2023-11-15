# Kind Kubernetes
Befor installing the Kind application, we need to install the Docker desktop on local machine.
If you are using the Linux local machine, you can use install the Docker application as well.
After installing the Docker, need to install the Kind application.

### Linux installation

```
apt-get install sudo
sudo usermod -aG sudo <username>

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client




```



```

#linux:
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
sudo chmod +x /usr/local/bin/kind




#macOs:
[ $(uname -m) = x86_64 ]&& curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-darwin-amd64
or:
[ $(uname -m) = arm64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-darwin-arm64
chmod +x ./kind
mv ./kind /usr/local/bin/kind
sudo chown -R /usr/local


#Windows:
curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.20.0/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\Kind\kind.exe


---------------------

kind --version



```
:smile:
### 01- Create Kubernetes Cluster using Kind:

```
kind create cluster --name my-cluster
```
```
kind create cluster --image=[image]
```

To use a custom node image for the cluster, use the --image option:

```
kind create cluster --name=<ClusterName> --config=wconfig.yaml
kind create cluster --name=giada --config=kind-config.yaml
```

Getting the cluster list:

```

kubectl get nodes
kind get clusters
kubectl cluster-info --context kind-ibstorm
kubectl cluster-info --context kind-[cluster-name]
kind delete cluster
kind delete cluster --name [cluster-name]

```

### 02- Apply the ingress NGINX controller with the following command:

The command creates multiple Kubernetes objects. In this configuration, ingress works as the cluster's reverse proxy and load balancer.
```
kubectl apply -f deploy.yaml
```

## 03- Deploy a Service Locally:

When you finish setting up the cluster, test it by deploying a service. The example below shows how to deploy a simple HTTP echo server.


```
kubectl apply -f test-deployment.yaml

kubectl port-forward service/test-service 5678:5678

curl localhost:5678

export KUBECONFIG=$(pwd)/kubeconfig.yaml
kind get kubeconfig --name my-cluster > kubeconfig.yaml

```

### 04- Kubernetes kind Cheat Sheet

```
kind create cluster
kind create cluster --name=[cluster-name]
kind create cluster --image=[image]
kind create cluster --config=[config-yaml]
kind create cluster --wait [time-interval]
kind get clusters
kubectl cluster-info --context kind-[cluster-name]
kind load docker-image [docker-image-name]
kind load image-archive [tar-archive-location]
kind export logs
kind delete cluster --name [cluster-name]
```

https://phoenixnap.com/kb/kubernetes-kind

### 05- Kubectl command

```
kubectl config view --minify
kubectl config view --raw

```
https://stackoverflow.com/questions/61029037/how-to-connect-to-k8s-cluster-of-docker-desktop-on-another-machine

https://kind.sigs.k8s.io/docs/user/ingress
https://mjpitz.com/blog/2020/10/21/local-ingress-domains-kind/
