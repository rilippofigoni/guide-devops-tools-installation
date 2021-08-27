## GUIDE TO INSTALL VARIOUS DEVOPS TOOLS ON POP_OS & (debian based distros)

###  1 - INSTALL KUBECTL (Kubernetes)

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
