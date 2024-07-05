# kubernetes

https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/




ON UBUNTU

sudo apt-get update -y
sudo apt-get install -y apt-transport-https
sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
vi /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
apt-get update -y
apt-get install docker.io -y
systemctl enable docker
systemctl start docker
usermod -a -G docker ubuntu
apt-get install -y kubelet kubeadm kubectl kubernetes-cni
sudo dpkg -i --force-overwrite /var/cache/apt/archives/kubernetes-cni_0.7.5-00_amd64.deb
vi /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
makefileCopy codeEnvironment="cgroup-driver=systemd/cgroup-driver=cgroupfs"





sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo sh -c 'echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list'
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl docker.io
sudo systemctl start docker
sudo systemctl enable docker




sudo apt-get update && sudo apt-get install -y 
sudo apt-get install -y docker.io
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archives-archive-keyring.gpg
https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg]
https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee/etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl


sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get update && sudo apt-get install -y kubelet=1.20.0-00 kubeadm=1.20.0-00 kubectl=1.20.0-00 docker.io
sudo systemctl start docker && sudo systemctl enable docker


sudo su
apt-get update 
apt-get install -y docker.io
apt-get update && apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
apt-get update
apt-get install -y kubelet kubeadm kubectl 
nano /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
Environment=”cgroup-driver=systemd/cgroup-driver=cgroupfs”





sudo apt update
sudo apt upgrade -y
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo add-apt-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo swapoff -a
sudo apt update
sudo apt install -y kubelet kubeadm kubectl






vi kubernetes.sh

sudo yum install -y docker
sudo systemctl enable docker
sudo systemctl start docker
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/
enabled=1
gpgcheck=1
gpgkey=https://pkgs.k8s.io/core:/stable:/v1.28/rpm/repodata/repomd.xml.key
exclude=kubelet kubeadm kubectl cri-tools kubernetes-cni
EOF
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
sudo systemctl enable --now kubelet
VER=$(curl -s https://api.github.com/repos/Mirantis/cri-dockerd/releases/latest|grep tag_name | cut -d '"' -f 4|sed 's/v//g')
wget https://github.com/Mirantis/cri-dockerd/releases/download/v${VER}/cri-dockerd-${VER}.amd64.tgz
tar xvf cri-dockerd-${VER}.amd64.tgz
sudo mv cri-dockerd/cri-dockerd /usr/local/bin/
wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.service
wget https://raw.githubusercontent.com/Mirantis/cri-dockerd/master/packaging/systemd/cri-docker.socket
sudo mv cri-docker.socket cri-docker.service /etc/systemd/system/
sudo sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
sudo systemctl daemon-reload
sudo systemctl enable cri-docker.service
sudo systemctl enable --now cri-docker.socket
sudo kubeadm config images pull --cri-socket unix:///var/run/cri-dockerd.sock



kubernetes.sh file copy this file on master and slave machine and on both the server run this below command
chmod +x kubernetes.sh
./kubernetes.sh
above command will install all the prerequisites for kubernetes cluster creation.




Once you execute the above file on both master and slave machine. Run the below command on the master server.
sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=172.31.39.26(Change it to the private IP of ur Master Server) --cri-socket unix:///var/run/cri-dockerd.sock




Run the below command only on the worker node after the above command completes to join the worker node in the cluster with this flag
--cri-socket unix:///var/run/cri-dockerd.sock 
Example:
sudo kubeadm join 172.31.39.26:6443 --token pdbqdh.3g5fypnrfjks2hlz         --discovery-token-ca-cert-hash sha256:7121b34ffaf14a381ea91b00f7f24cad1476b2e40adcb7c22e6b496dc6608329 --cri-socket unix:///var/run/cri-dockerd.sock







CALICO 3RD PARTY NETWORK INSTALL

https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/

kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.2/manifests/tigera-operator.yaml

curl https://raw.githubusercontent.com/projectcalico/calico/v3.27.2/manifests/custom-resources.yaml -O

kubectl create -f custom-resources.yaml




    
    2  vi kubernetes.sh
    3  sudo chmod +x kubernetes.sh
    4  ./kubernetes.sh
    5  clear
    6  sudo kubeadm init --pod-network-cidr=192.168.0.0/16 --apiserver-advertise-address=172.31.9.106 --cri-socket unix:///var/run/cri-dockerd.sock
    
    
    GET RID OF SUDO
    8  cd /etc/kubernetes
    9  ls -al
   10  cd ~
   11  clear
   12  mkdir -p $HOME/.kube
   13  clear
   14  ls -al
   
   17  cd .kube
   18  ls -al
   19  cd ..
   20  pwd
   21  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config     ......COPY THE admin.conf to current user path
   22  sudo chown $(id -u):$(id -g) $HOME/.kube/config
   
   
   24  kubectl get nodes ,,,,,,,,,NOT READY , BECAUSE NETWORK IS NOT INSTALLED
   
   25  kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.0/manifests/tigera-operator.yaml
   27  curl https://raw.githubusercontent.com/projectcalico/calico/v3.27.0/manifests/custom-resources.yaml -O
   28  kubectl create -f custom-resources.yaml
  
  
   30  watch kubectl get nodes .... TO REFRESH AT INTERVAL
  
   32  kubectl get nodes ,,,,,,,,,NOW READY 
   
   33  kubectl get nodes -o wide
   34  
   36  kubectl cluster-info               MORE INFO
   
   37  kubectl get componentstatuses
   
   39  kubectl run mydemopod --image=nginx ........ CREATE POD
   40  kubectl get pods
   41  kubectl get pods -o wide
   
   44  kubectl get ns.........DIFF NAMESPACES ARE LISTED
   45  kubectl get pods
   46  
   47  kubectl get pods -n kube-system ....................TO SEE THE PODS IN THE kube-system ns
   48  kubectl get ns
   49  
   50  kubectl get pods -n calico-apiserver
   51  kubectl get pods -n kube-public
   
   
   54  kubectl get pods
   55
   56  kubectl logs mydemopod
   57  clear
   58  kubectl get pods
   59  kubectl describe pod mydemopod
   60  clear
   61  kubectl get pods
   62  kubectl exec -it mydemopod -- bash
   63  clear
   64  kubectl get pods
   65  kubectl delete pod mydemopod
   66  kubectl get pods
   67  kubectl run mydemopod --image=nginx
   68  clear
   69  kubectl get ns
   70  
   
   
   CREATE NS
   71  kubectl create ns devops
   72  kubectl get ns
   
   CREATE A POD INSIDE devops ns
   
   73  kubectl run mydemopod2 --image=nginx -n devops
   74  
   77  kubectl get pods -n devops
   78  clear
   79  kubectl get ns
   80  kubectl delete ns devops
   81  kubectl get ns
   82  clear
   83  kubectl api-resources
   






