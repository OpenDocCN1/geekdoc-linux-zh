
```bash
$ kubectl describe pods $POD_NAME
Name: kubernetes-bootcamp-9bc58d867-7g6dr
Namespace: default
Priority: 0
Service Account: default
Sease:
Node: minikube
Start Time: Sat, 12 Apr 2025 03:39:50 -0400
Labels: app=kubernetes-bootcamp pod-template-hash=9bc58d86 version=v1
```

```bash
$ kubectl get pods -l version=v1
NAME READY STATUS RESTARTS
kubernetes-bootcamp-9bc58d867-7g6dr 1/1 Running 0
```

## 删除服务

如果你正在使用该服务，可以删除它。这将移除对 NodePort 的访问，但不会删除 deployment。

1. 检查服务：确保 `kubernetes-bootcamp` 服务存在：

```bash
$ kubectl get services
| NAME | TYPE | CLUSTER-IP | EXTERNAL-IP | PORT(S) | AGE |
| kubernetes | ClusterIP | 10.96.0.1 | <none> | 443/TCP | 97m |
| kubernetes-bootcamp | NodePort | 10.106.58.189 | <none> | 8080:30128/TCP | 30m |
```

2. 删除服务：使用标签删除服务：

```bash
$ kubectl delete service -l app=kubernetes-bootcamp
service/bootcamp deleted
```

3. 检查服务和部署：确保服务已删除但部署仍然存在：

```bash
$ kubectl get services
| NAME | TYPE | CLUSTER-IP | EXTERNAL-IP | PORT(S) | AGE |
| kubernetes | ClusterIP | 10.96.0.1 | <none> | 443/TCP | 64m |
```

```bash
$ kubectl get deployment
| NAME READY UP-TO-DATE AVAILABLE |
| kubernetes-bootcamp 1/1 1 |
```

## 扩容应用程序

Kubernetes 最强大的功能之一是可以根据需要扩容应用程序。此过程从 `kubernetes-bootcamp` 部署开始，通过 ReplicaSet 功能增加额外的 pod，并将应用程序暴露到外部。

1. 获取部署：列出 `kubernetes-bootcamp` 部署的信息，并注意它被设置为一个副本集 (rs)：

```bash
$ kubectl get deployments
| NAME READY UP-TO-DATE AVAILABLE AGE |
| kubernetes-bootcamp 1/1 1 1 107s |
```

```bash
$ kubectl get rs
| NAME DESIRED CURRENT READY AGE |
| kubernetes-bootcamp-5b48cfcd 1 1 1 3m4s |
```

2. 扩容副本：通过以下命令将部署扩容到四个副本：

```bash
$ kubectl scale deployments/kubernetes-bootcamp --replicas=4
deployment.apps/kubernetes-bootcamp scaled
```

3. 检查新副本：列出部署以确保现在四个副本已就绪可用：

```bash
$ kubectl get deployments
| NAME READY UP-TO-DATE AVAILABLE AGE |
| kubernetes-bootcamp-9bc 4/4 4 4 8m4s |
```

4. 检查 pod：现在应该有四个 `kubernetes-bootcamp` pod 在运行，每个 pod 都有集群内部 IP 地址。为了确认，请检查以下内容：

```bash
$ kubectl get pods -o wide
| NODE NOMINATED STATUS RESTARTS AGE IP |
| kubernetes-bootcamp-9bc | 1/1 Running | 0 | 8m4s | 10.24.0.6 |
| minikube | <none> | | | | |
| kubernetes-bootcamp-9bc | 1/1 Running | 0 | 12s | 10.24.0.4 |
| minikube | <none> | | | | |
| kubernetes-bootcamp-9bc | 1/1 Running | 0 | 12s | 10.24.0.5 |
| minikube | <none> | | | | |
| kubernetes-bootcamp-9bc | 1/1 Running | 0 | 12s | 10.24.0.7 |
| minikube | <none> | | | | |
```

5. 查看部署详情：要查看部署中副本的详情，执行以下命令：

```bash
$ kubectl describe deployments/kubernetes-bootcamp
```

```yaml
Name: kubernetes-bootcamp
Namespace: default
NewReplicaSet: kubernetes-bootcamp-9bc58d867 (4/4 replicas created)
Events:
| Type | Reason | Age | From | Message |
|---|---|---|---|---|
| Normal | ScalingReplicaSet | 59m | deployment-controller | Scaled up replica set kubernetes-bootcamp-9bc58d867 from 0 to 1 |
Normal | ScalingReplicaSet | 2m5s | deployment-controller | Scaled
```

## 检查负载均衡器

要检查流量是否分布在四个 pod 上，你可以获取 NodePort，然后使用 curl 命令确保多次连接结果指向不同的 pod。

1. 列出服务的详细信息：要查看 `kubernetes-bootcamp` 服务的详情，执行以下命令：

```bash
$ kubectl expose \
  deployment/kubernetes-bootcamp \
  --type="NodePort" --port 8080
$ kubectl describe services kubernetes
```

2. 获取 NodePort：输入以下命令将 `$NODE_PORT` 设置为分配给服务的端口号：

```bash
$ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp \
  -o go-template='{{{{index .spec.ports 0}}.nodePort}}')

echo NODE_PORT=$NODE_PORT
NODE_PORT=31915
```

3. 运行 curl：多次使用 curl 查询服务。如果你运行几次，你会发现它正在访问不同的 pod。这就是负载均衡器正在运行的证明：

```bash
$ curl $(minikube ip):$NODE_PORT
|Hello Kubernetes bootcamp!|Running on: kubernetes-bootcamp-9bc58
867-en257|v=1
```

## 缩容应用程序

要缩减部署中定义的副本集数量，只需将副本数量更改为较小的值即可。

## 第 31 章：使用 Kubernetes 部署容器化应用程序

1. 缩减副本数：输入以下命令将部署的副本数更改为 2：

```bash
$ kubectl scale deployments/kubernetes-bootcamp --replicas=2 deployment.extensions/kubernetes-bootcamp scaled
```

2. 检查部署：确保部署已设置为 2，且只有两个 pod 正在运行，输入以下命令：

```bash
$ kubectl get deployments
```

| NAME | READY | UP-TO-DATE | AVAILABLE | AGE |
|---|---|---|---|--|
| kubernetes-bootcamp | 2/2 | | 2 | 52m |

```bash
$ kubectl get pods -o wide
```

| NAME | NOMINATED | READY | STATUS | RESTARTS | AGE | IP |
|---|---|---|---|---|---|--|
| kubernetes-bootcamp-9bc... | | 2/2 | Running | 0 | 8m4s | 10.244.0.6 |
| minikube | | <none> | | | | 10.244.0.4 |
| kubernetes-bootcamp-9bc... | | 1/1 | Running | | 12s | |

此时，你应该已经熟悉如何通过各种方式查询 Kubernetes 集群，并从部署、pod 和副本开始操作。要继续学习高级 Kubernetes 教程，请参考 Kubernetes 教程主页 (https://kubernetes.io/docs/tutorials/)。

## 使用 EKS 获取企业级 Kubernetes

虽然我们可以像在书中那样在单机上运行 Kubernetes 来测试其功能，但它的真正价值在于你需要在生产环境中运行并扩展 Kubernetes 时。当你正在构建企业级集群来运行最关键的业务负载时，你应该考虑以下因素：

- **可扩展性**：如果你的应用程序过载，Kubernetes 可以增加 pod。如果你的节点达到了容量极限，Kubernetes 可以增加节点。同样，随着需求增加，可以关闭这些节点。

- **自愈能力**：Kubernetes 可以对容器、pod、节点、服务和其他对象进行健康检查，并在它们失败或性能下降时进行替换。

- **高可用性**：通过使用扩展性和自愈等功能，Kubernetes 可以确保应用程序对客户始终可用。由于 Kubernetes 正在响应故障和增加的需求，应用程序不会表现为不可用。Kubernetes 集群还可以分布在多个位置，这样即使一组集群甚至整个数据中心故障，也可以切换到其他位置的系统。

- **效率**：由于 Kubernetes 允许你根据当前需求运行尽可能多的负载和节点，你可以实现计算资源的最大化利用。为此，Kubernetes 可以通过合并负载到单个更高效、尺寸合适的计算机上，或者将负载迁移到成本更低的系统。

![](img/a623301149fbdf7af5e6dcdd26f766e2_847_0.png)

# 第六部分：接触云计算

- **开源 Kubernetes 生态系统**：由于 Kubernetes 是一个开源项目，不由单一公司拥有或维护，许多公司和组织已经采用并扩展了它。这意味着你可以从内置功能以及第三方软件中进行选择，使用它们来满足你的需求。

- **可移植性**：Kubernetes 能够在不同的环境中运行（如本地、边缘计算和数据中心），并获得不同供应商（如 AWS、Microsoft、Google 和 Red Hat）的支持。这允许你开发公司的应用程序，然后将其部署到最符合你需求的任何地方。

大多数云提供商提供托管 Kubernetes 服务，可以从多个方面提供帮助。它们可以在你开发产品的同时节省创建自有数据中心的成本，并允许你根据需求增长 Kubernetes 使用。流行的云服务提供商包括 Amazon Web Services (AWS) Elastic Kubernetes Service (EKS)、Microsoft Azure 的 Kubernetes Service (AKS) 以及 Google Cloud 的 Kubernetes Engine (GKE)。

这些 Kubernetes 集群还可以通过简化进入 Kubernetes 的流程来提供帮助。例如，它们可以为你提供简单的方法来管理控制平面，选择一组他们打包好的实用附加软件，甚至设置自动伸缩来扩展你用于运行负载的节点。

随着你对使用 Kubernetes 越来越熟悉，你将能够灵活调整集群并增强与集群配合软件。监控和可观测性等功能可以使你的 Kubernetes 使用更高效、更具成本效益。

## 总结

Kubernetes 已经成为在大型数据中心部署容器化应用程序的首选平台。一个 Kubernetes 集群由控制平面（引导集群活动）和节点（实际运行容器化负载的机器）组成。

作为使用 Kubernetes 进行应用程序容器化的用户，你可以创建部署来定义正在运行的应用程序的状态。例如，你可以部署一个配置为运行多个代表该应用程序的 pod 副本的应用程序。你可以将应用程序标识为服务，并设置应用程序在挂载存储可用且从其所在节点的定义端口可用时可用。

当你需要在稳定且支持的环境中运行关键任务应用程序时，可以使用基于 Kubernetes 的产品。大多数主流云提供商提供托管 Kubernetes 服务，可以提供简单、廉价的进入生产级 Kubernetes 集群的方法，并让你根据需要轻松扩展 Kubernetes 负载。

## 练习

本节的练习描述了与尝试 Kubernetes 相关的任务，可以通过在线或在计算机上设置 Minikube 来完成。如果你遇到困难，附录 B 中提供了任务的解决方案。请记住：

1. 安装 Minikube 和 kubectl 客户端。
2. 查看你的 Minikube 版本以及 kubectl 版本。
3. 创建一个管理 pod 的部署 (gcr.io/hellonode)。
4. 使用 kubectl 命令详细描述部署。
5. 查看与部署相关的副本集 (replica set)。
6. 将部署扩展到三个副本。
7. 使用 LoadBalancer 将 Kubernetes 集群暴露部署。
8. 获取暴露服务的 IP 地址。
9. 使用 curl 命令通过上一步的 IP 地址和端口查询服务。
10. 使用 kubectl 命令删除服务和部署，然后使用 minikube 命令停止虚拟机。

# 媒体

# 附录

获取 Linux 发行版

创建可启动的 USB、CD 或 DVD

除非你购买了预装 Linux 的计算机，或者有人为你安装了它，否则你需要找到获取 Linux 发行版的方法，并在计算机上安装或运行它。幸运的是，Linux 发行版广泛存在且形式多样。

在本附录中，你将学习执行以下操作：

- 获取几个 Linux 发行版。
- 创建用于安装发行版的可启动磁盘。
- 从 USB 驱动器启动 Linux。

为了有效地使用本内容，你应该有一个 Linux 发行版供你操作。在阅读时能够体验 Linux 是重要的。因此，请尝试示例并完成练习。

Linux 发行版通常可以在制作组织的网站获取。以下章节描述了提供下载 ISO 镜像的 Linux 发行版相关网站。

> ISO 是一种磁盘镜像，采用 ISO 格式，通常用于 USB、CD 和 DVD 镜像。由于这是一个常用格式，Windows、Mac 和 Linux 都可以读取。ISO 可创建可启动 USB 闪存盘、CD 或 DVD 介质，取决于镜像的大小。文件系统中的 ISO 可以以回环模式挂载，以便查看或复制其内容。

当 ISO 包含 Linux 文件或安装镜像时，这些镜像是可启动的。这意味着你不是从计算机硬盘启动操作系统（如 Windows 或 Linux），而是告诉计算机从安装的 CD 或 DVD 启动。这允许你运行一个安装在硬盘上的完全不同的操作系统，而不会损坏该硬盘上的数据。

## 附录 A：媒体

### 获取 Fedora

> **注意**
>
> 我建议下载 Workstation Live 镜像（工作站实时版）并配合本书使用，因为书中的大部分内容适用于该发行版。在您觉得足够准备好永久安装之前，可以先运行它而无需急于覆盖您电脑的硬盘。

为了测试书中的示例，我主要使用了 Fedora 42 64 位 Fedora Workstation 镜像，你可以从 Fedora.org (https://fedoraproject.org/en/workstation/download) 获取它们。如果你的电脑是 64 位的，则必须使用 64 位的 ISO。此外还有 64 位 ARM 和 PowerPC 版本可供选择。

带有 GNOME 桌面面的后续 Fedora 版本也应该可以使用。这里是用于 Fedora 42 Workstation 的确切 ISO 链接：

https://download.fedoraproject.org/pub/fedora/linux/releases/42/Workstation/x86_64.iso/Fedora-Workstation-42-1.1.x86_64.iso

请记住，最新的 Fedora Workstation ISO 镜像无法放入 CD，因此你必须将其刻录到 DVD 或 USB 驱动器。请参见本附录后部分适用于 Windows、macOS 和 Linux 的 CD/DVD 刻录工具描述。

图 A.1 显示了 Fedora Workstation 下载页面的示例。

图 A.1

从 Fedora Workstation 下载页面获取 Fedora ISO 镜像。

![](img/a623301149fbdf7af5e6dcdd26f766e2_851_0.png)

> **注意**
