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