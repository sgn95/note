# Kubernetes 简介

谷歌开源的容器集群管理系统
主要功能包括：

基于容器的应用部署、维护和滚动升级
负载均衡和服务发现
跨机器和跨地区的集群调度
自动伸缩
无状态服务和有状态服务
广泛的 Volume 支持
插件机制保证扩展性

wget https://github.com/GoogleCloudPlatform/kubernetes/releases/download/v1.4.0/kubernetes.tar.gz
核心组件
```
etcd：保存了整个集群的状态；
apiserver：提供了资源操作的唯一入口，并提供认证、授权、访问控制、API 注册和发现等机制；
controller manager：负责维护集群的状态，比如故障检测、自动扩展、滚动更新等；
scheduler：负责资源的调度，按照预定的调度策略将 Pod 调度到相应的机器上；
kubelet：负责维护容器的生命周期，同时也负责 Volume（CVI）和网络（CNI）的管理；
Container runtime：负责镜像管理以及 Pod 和容器的真正运行（CRI）；
kube-proxy：负责为 Service 提供 cluster 内部的服务发现和负载均衡
```
https://www.jianshu.com/p/27a8187af0e9
wget https://github.com/GoogleCloudPlatform/kubernetes/releases/download/v1.6.0/kubernetes.tar.gz
借鉴
https://blog.devopszen.com/kubernetes
