## GUIDE TO INSTALL VARIOUS DEVOPS TOOLS ON POP_OS & (debian based distros)

###  1 - INSTALL KUBECTL (Kubernetes - K8S)

#### Install using native package management Debian-based distributions:

1. ***Update the apt package index and install packages needed to use the Kubernetes apt repository:***

`sudo apt-get update`
`sudo apt-get install -y apt-transport-https ca-certificates curl`

2. ***Download the Google Cloud public signing key:***

`sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg`

3. ***Add the Kubernetes apt repository:***

`echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list`

4. ***Update apt package index with the new repository and install kubectl:***

`sudo apt-get update`
`sudo apt-get install -y kubectl`



### 2 - INSTALL K3D

#### Install current latest release:

-  `wget -q -O - https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash`
- `curl -s https://raw.githubusercontent.com/rancher/k3d/main/install.sh | bash`

#### Installation script download:

https://raw.githubusercontent.com/rancher/k3d/main/install.sh

### 2.1 - CREATE A SIMPLE CLUSTER with K3D


>Let’s create a simple cluster with 1 loadbalancer and 1 node (with role of server and agent) with name “dev”:

`k3d cluster create dev --port 8080:80@loadbalancer --port 8443:443@loadbalancer`

`INFO[0000] Prep: Network                                
INFO[0000] Created network 'k3d-dev' (3e153fa11d3c515c0e1246fe7a945edc226b2bc2ec4bddc5798d5541d94ab50c) 
INFO[0000] Created volume 'k3d-dev-images'              
INFO[0001] Creating node 'k3d-dev-server-0'             
INFO[0003] Pulling image 'docker.io/rancher/k3s:v1.21.3-k3s1' 
INFO[0023] Creating LoadBalancer 'k3d-dev-serverlb'     
INFO[0026] Pulling image 'docker.io/rancher/k3d-proxy:4.4.8' 
INFO[0036] Starting cluster 'dev'                       
INFO[0036] Starting servers...                          
INFO[0036] Starting Node 'k3d-dev-server-0'             
INFO[0042] Starting agents...                           
INFO[0042] Starting helpers...                          
INFO[0042] Starting Node 'k3d-dev-serverlb'             
INFO[0043] (Optional) Trying to get IP of the docker host and inject it into the cluster as 'host.k3d.internal' for easy access 
INFO[0046] Successfully added host record to /etc/hosts in 2/2 nodes and to the CoreDNS ConfigMap 
INFO[0046] Cluster 'dev' created successfully!          
INFO[0046] --kubeconfig-update-default=false --> sets --kubeconfig-switch-context=false 
INFO[0046] You can now use it like this:                
kubectl config use-context k3d-dev
kubectl cluster-info`

`❯ kubectl get nodes
NAME               STATUS   ROLES                  AGE     VERSION
k3d-dev-server-0   Ready    control-plane,master   6m48s   v1.21.3+k3s1`

### 3 - INSTALL DOCKER 

#### Install Docker from Ubuntu/Pop_OS Repository

```
sudo apt install docker.io
```

```
sudo systemctl enable --now docker
```

```
sudo docker run hello-world
```

#### Add user to sudo group

`sudo usermod -aG docker ${USER}`

`su - ${USER}`

`id -nG`



### 4 - INSTALL HELM3

#### Install from console :

`curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3`

`sudo chmod 700 get_helm.sh`

`sudo ./get_helm.sh`

#### Test version :

`helm version`

`version.BuildInfo{Version:"v3.6.3", GitCommit:"d506314abfb5d21419df8c7e7e68012379db2354", GitTreeState:"clean", GoVersion:"go1.16.5"}`

#### Alternative :

`curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash`

#### From repository

```fallback
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```
### 5 - INSTALL TERRAFORM

#### From Official Repository :

`sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl`

`curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -`

`sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"`

`sudo apt-get update `

`sudo apt-get install terraform`

#### Test :

`terraform -help`



### 6 - AWS CLIENT

#### **For the latest version of the AWS CLI,** use the following command block:

`curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install`

#### TEST :

`aws --version`` aws-cli/2.1.29 Python/3.7.4 Linux/4.14.133-113.105.amzn2.x86_64 botocore/2.0.0`

#### CONFIGURE :

`aws configure`

`AWS Access Key ID [None]:` 
