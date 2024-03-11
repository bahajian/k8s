# Kind Kubernetes
Befor installing the Kind application, we need to install the Docker desktop on local machine.
If you are using the Linux local machine, you can use install the Docker application as well.
After installing the Docker, need to install the Kind application.

### Linux installation

```
apt install sudo
sudo usermod -aG sudo <username>
```
## 1-Set up Docker's apt repository.

### Add Docker's official GPG key:

```
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### Add the repository to Apt sources:

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```

## 2-Install the Docker packages.

```
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## 3-Verify that the installation is successful by running the hello-world image:
```
sudo docker run hello-world
```

# Install kubectl binary with curl on Linux

```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```



```
https://github.com/kubernetes-sigs/kind/releases/
```

# Install kind on Linux
```
https://github.com/kubernetes-sigs/kind/releases/
```
### Linux

```
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-$(uname)-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-$(uname)-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```


---------------------

kind --version




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

```
export KUBECONFIG=$(pwd)/kubeconfig.yaml
kind get kubeconfig --name my-cluster > kubeconfig.yaml
```
#### Sometimes when you reboot the machine, the cluster doesn't come up because other essential services need to start first. 
#### You can add a delay before starting Docker or the cluster to ensure these services are ready.

need to use editor like vi or nano to edit the file :
```
nano /lib/systemd/system/docker.service
```
then add these two lines at the first beginig of [Service] section.
```
RequiresMountsFor=/mnt/foo /mnt/bar
ExecStartPre=/bin/sleep 30
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

kubectl get nodes -v=10
```
Sometimes, it is necessary to introduce a delay before starting the Docker engine. To implement this delay, execute the following command and add the service configuration at the beginning of the file.

sudo nano /etc/systemd/system/multi-user.target.wants/docker.service
```
[Service]
ExecStartPre=/bin/sleep 10
```
https://stackoverflow.com/questions/61029037/how-to-connect-to-k8s-cluster-of-docker-desktop-on-another-machine

https://kind.sigs.k8s.io/docs/user/ingress
https://mjpitz.com/blog/2020/10/21/local-ingress-domains-kind/



docker ps
docker ps -a
docker logs giada-control-plane

docker network ls
docker network inspect <network_name>

kubectl get nodes -o wide
