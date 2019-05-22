# 什么是Helm

Helm, Kubernetes的包管理工具 使用过docker swarm集群的 一定知道docker-compose 我觉Helm和docker-compose做的功能很类似


# setup 安装 Helm
下载

    https://github.com/helm/helm/releases

我选择的是linux-amd64

    wget https://get.helm.sh/helm-v3.0.0-alpha.1-linux-amd64.tar.gz

解压 
    
    tar -zxvf helm-v3.0.0-alpha.1-linux-amd64.tar.gz

把命令包放到/usr/local/bin/目录下
    
    mv linux-amd64/helm /usr/local/bin/

kubernetes 集群 
确定要应用于安装的安全配置
安装和配置集群端服务Helm和Tiller

推荐使用最新的Kubernets的稳定版本 在大多数情况

拥有本地配置的副本kubectl

注意：1.6之前的Kubernetes版本对基于角色的访问控制（RBAC）的支持有限或不支持。

Helm将读取您的Kubernetes 配置文件 通常是$HOME/.kube/config 来确定安装Tiller的位置 这是kubetl使用的文件

要找出Tiller将安装到那个集群 您可以运行kubectl config current-context 或 kubectl cluster-info
kubectl config current-context

参考
https://helm.sh/docs/using_helm/#quickstart-guide

yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

cat > ca-csr.json << EOF
{
  "CN": "kubernetes",
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
    {
      "C": "CN",
      "ST": "BeiJing",
      "L": "BeiJing",
      "O": "k8s",
      "OU": "System"
    }
  ]
}
EOF

cat > kubernetes-csr.json << EOF
{
   "CN": "kubernetes",
    "hosts": [
      "127.0.0.1",
      "10.30.221.97",
      "10.30.221.98",
      "kubernetes",
      "kubernetes.default.svc",
      "kubernetes.default.svc.cluster",
      "kubernetes.default.svc.cluster.local"
    ],
    "key": {
        "algo": "rsa",
        "size": 2048
    },
    "names": [
        {
            "C": "CN",
            "ST": "BeiJing",
            "L": "BeiJing",
            "O": "k8s",
            "OU": "System"
        }
    ]
}
EOF

cat > admin-csr.json << EOF
{
  "CN": "admin",
  "hosts": [],
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
    {
      "C": "CN",
      "ST": "BeiJing",
      "L": "BeiJing",
      "O": "system:masters",
      "OU": "System"
    }
  ]
}
EOF

cat > kube-proxy-csr.json << EOF
{
  "CN": "system:kube-proxy",
  "hosts": [],
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
    {
      "C": "CN",
      "ST": "BeiJing",
      "L": "BeiJing",
      "O": "k8s",
      "OU": "System"
    }
  ]
}
EOF

cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
        http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF


apt-get update && apt-get install -y apt-transport-https curl
curl -s http://packages.faasx.com/google/apt/doc/apt-key.gpg | sudo apt-key add -

cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main
EOF

apt-get update
apt-get install -y kubelet kubeadm kubectl
    
apt-mark hold kubelet kubeadm kubectl