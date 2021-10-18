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

### 7 - JENKINS

##### install Java with apt command

```bash
sudo apt install openjdk-11-jre-headless

java --version
```

#### Install Jenkins via its official repository

```bash
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
```

```bash
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

```bash
 sudo apt update && sudo apt install jenkins
```

#### Jenkins should start automatically. To confirm this, run the command:

```bash
sudo systemctl status jenkins
```

`sudo systemctl status jenkins`

`● jenkins.service - LSB: Start Jenkins at boot time`
     `Loaded: loaded (/etc/init.d/jenkins; generated)`
     `Active: active (exited) since Thu 2021-09-02 12:15:10 CEST; 1min 37s ago`
       `Docs: man:systemd-sysv-generator(8)`
    `Process: 18074 ExecStart=/etc/init.d/jenkins start (code=exited, status=0/SUCCESS)`

`set 02 12:15:08 pop-os systemd[1]: Starting LSB: Start Jenkins at boot time...`
`set 02 12:15:08 pop-os jenkins[18074]: Correct java version found`
`set 02 12:15:08 pop-os jenkins[18074]:  * Starting Jenkins Automation Server jenkins`
`set 02 12:15:09 pop-os su[18115]: (to jenkins) root on none`
`set 02 12:15:09 pop-os su[18115]: pam_unix(su-l:session): session opened for user jenkins by (uid=0)`
`set 02 12:15:09 pop-os su[18115]: pam_unix(su-l:session): session closed for user jenkins`
`set 02 12:15:10 pop-os jenkins[18074]:    ...done.`
`set 02 12:15:10 pop-os systemd[1]: Started LSB: Start Jenkins at boot time.`

#### Configure Jenkins with GUI

http://localhost:8080 (or IP local)

#### To find password:

```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```

#### After follow instructions on :

https://www.linuxtechi.com/install-configure-jenkins-ubuntu-20-04/





### 8 -  MINIKUBE

#### Download minikube

You need to download the minikube binary. I will put the binary under /usr/local/bin directory since it is inside $PATH.

`wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
`chmod +x minikube-linux-amd64`
`sudo mv minikube-linux-amd64 /usr/local/bin/minikube`
`Confirm version installed`

`$ minikube version`
`minikube version: v1.9.2`
`commit: 93af9c1e43cab9618e301bc9fa720c63d5efa393`

#### Starting minikube
Now that components are installed, you can start minikube. VM image will be downloaded and configure d for Kubernetes single node cluster.

`$ minikube start`
`Starting local Kubernetes v1.10.0 cluster...`
`Starting VM...`
`Downloading Minikube ISO`
`150.53 MB / 150.53 MB [============================================] 100.00% 0s`
`Getting VM IP address...`
`Moving files into cluster...`
`Downloading kubeadm v1.10.0`
`Downloading kubelet v1.10.0`
`Finished Downloading kubeadm v1.10.0`
`Finished Downloading kubelet v1.10.0`
`Setting up certs...`
`Connecting to cluster...`
`Setting up kubeconfig...`
`Starting cluster components...`
`Kubectl is now configured to use the cluster.`
`Loading cached images from config file.`

Wait for the download and setup to finish then confirm that everything is working fine.

#### Minikube Basic operations

To check cluster status, run:

`$ kubectl cluster-info`

`Kubernetes master is running at https://192.168.39.117:8443`
`KubeDNS is running at https://192.168.39.117:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy`

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
Note that Minikube configuration file is located under ~/.minikube/machines/minikube/config.json

To View Config, use:

`$ kubectl config view`

`apiVersion: v1`
`clusters:`

- `cluster:`
    `certificate-authority: /home/jmutai/.minikube/ca.crt`
    `server: https://192.168.39.117:8443`
  `name: minikube`
    `contexts:`
- `context:`
    `cluster: minikube`
    `user: minikube`
  `name: minikube`
    `current-context: minikube`
    `kind: Config`
    `preferences: {}`
    `users:`
- `name: minikube`
  `user:`
    `client-certificate: /home/jmutai/.minikube/client.crt`
    `client-key: /home/jmutai/.minikube/client.key`
  `To check running nodes:`

`$ kubectl get nodes`
`NAME       STATUS    ROLES     AGE       VERSION`
`minikube   Ready     master    13m       v1.10.0`

#### Access minikube VM using ssh:

`$ minikube ssh`

`$ sudo su -`
`To stop a running local kubernetes cluster, run:`

`$ minikube stop`
`To delete a local kubernetes cluster, use:`

`$ minikube delete`ls -ltra



#### Enable Kubernetes Dashboard

Kubernete ships with a web dashboard which allows you to manage your cluster without interacting with a command line. The dashboard addon is installed and enabled by default on minikube.

`$ minikube addons list`

- `addon-manager: enabled`
- `coredns: disabled`
- `dashboard: enabled`
- `default-storageclass: enabled`
- `efk: disabled`
- `freshpod: disabled`
- `heapster: disabled`
- `ingress: disabled`
- `kube-dns: enabled`
- `metrics-server: disabled`
- `registry: disabled`
- `registry-creds: disabled`
- `storage-provisioner: enabled`
`To open directly on your default browser, use:`

`$ minikube dashboard`
`To get the URL of the dashboard`

`$ minikube dashboard --url`
`http://192.168.39.117:30000`
