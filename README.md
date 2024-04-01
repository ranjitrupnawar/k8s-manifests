k8s sta
#k8s instalation
firstly config aws on cli through aws cli [apt install aws-cli -y]

 #==> kubectl
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.27.1/2023-04-19/bin/linux/amd64/kubectl
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.27.1/2023-04-19/bin/linux/amd64/kubectl.sha256
sha256sum -c kubectl.sha256
openssl sha1 -sha256 kubectl
chmod +x ./kubectl
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
kubectl version --short --client

 #==> Eksctl 
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version


#==> IAM Access:
curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.9/aws-iam-authenticator_0.5.9_linux_amd64
openssl sha1 -sha256 aws-iam-authenticator
chmod +x ./aws-iam-authenticator
mkdir -p $HOME/bin && cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$HOME/bin:$PATH
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
aws-iam-authenticator help

#Note: attach role

#------------------------------------------
eksctl create cluster --name my-cluster --region ap-northeast-1 --version 1.26 --node-type t2.micro --nodes 2

#------------------------------------------

#commands:
kubectl get nodes -y
kubectl get service -y
kubectl get pods | pods --watch -y
kubectl create deployment nginx --image nginx -y
kubectl get deployment nginx -o yaml 
kubectl get pod <name of pod> -o yaml
kubectl expose deployment nginx --port 80 --type=LoadBalancer
kubectl create deployment art-mongo --image mongo
kubectl logs nginx-748c667d99-hmv47
kubectl delete pod <name of pod>
kubectl delete deployment <name of deployment>
