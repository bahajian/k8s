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

#linux:
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-linux-amd64
chmod +x ./kind
sudo chmod +x /usr/local/bin/kind
sudo mv ./kind /bin/kind



#macOs:
[ $(uname -m) = x86_64 ]&& curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-darwin-amd64
or:
[ $(uname -m) = arm64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-darwin-arm64
chmod +x ./kind
mv ./kind /usr/local/bin/kind
sudo chown -R /usr/local

#Windows:
curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.14.0/kind-windows-amd64
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
kind create cluster --name=nodes-test --config=workerNodes.yaml
```

Getting the cluster list:

```
kubectl get nodes
kind get clusters
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
