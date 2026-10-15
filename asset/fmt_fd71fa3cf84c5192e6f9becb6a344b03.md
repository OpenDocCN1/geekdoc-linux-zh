
- 4. 以检查模式（check mode）在 `my_playbook.yaml` 上运行 `ansible-playbook`，以查看完成 playbook 是否存在问题（提示：存在）。
- 5. 修改 `my_playbook.yaml` 以提升权限，以便任务以 `root` 用户身份运行。
- 6. 再次运行 `ansible-playbook`，直到 `httpd` 包成功安装在你的系统上。
- 7. 再次修改 `my_playbook.yaml` 以启动 `httpd` 服务，并设置其在每次系统启动时自动启动。
- 8. 运行 `ansible` 命令检查 `localhost` 上的 `httpd` 服务是否运行。
- 9. 创建一个包含文本“Web server is up”的 `index.html` 文件，并使用 `ansible` 命令将该文件复制到 `localhost` 的 `/var/www/html` 目录。
- 10. 使用 `curl` 命令查看你刚刚复制到 Web 服务器的文件内容。

## 使用 Kubernetes 部署容器应用程序

## 本章内容

- 理解 Kubernetes
- 尝试 Kubernetes
- 运行 Kubernetes 基础教程
- 使用 EKS 构建企业级 Kubernetes

Linux 容器将它们包含的应用程序与其运行的操作系统分离开来。准确地说，容器将包含一组离散的软件，这些软件可以高效地传输和运行。故事并没有此结束。一旦你拥有了一些容器，下一步就是让它们与 Kubernetes 等平台结合，允许你执行以下操作：

- 将一组容器组合形成更大的应用程序。例如，今天部署一个 Web 服务器、数据库和监控工具。
- 根据需求扩展容器规模。事实上，你希望能够单独扩展大型应用程序的每个组件，而无需扩展所有内容。
- 设置应用程序的状态而不是运行它。这意味着，你不是直接运行一个容器，而是能够说诸如“运行三个容器 X 的副本，如果其中一个崩溃了，务必启动另一个来替换它”之的话。
- 从主机故障或过载中恢复。如果运行容器的主机发生故障，你希望容器能够快速恢复并在另一台主机上启动。
- 无需担心基础设施。你希望应用程序连接到它所需的服务，而无需知道与服务相关的主机名、IP 地址或端口号。
- 在不停机的情况下升级你的容器化应用程序。

Kubernetes 提供了所有这些功能更多。虽然还有其他平台（如 Mesos 和 Docker Swarm）在竞争容器编排平台，但 Kubernetes 已成为编排、部署和管理容器化应用程序无可争议的领导者。Kubernetes 也成为运行大规模运行的人工智能和机器学习应用程序的首选。

# 第六部分：接触云计算

本章向你介绍 Kubernetes 以及亚马逊提供的企业级 Kubernetes 平台——Elastic Kubernetes Service (EKS)。学习 Kubernetes 的最好方法是启动一个 Kubernetes 集群，并运行命令来探索 Kubernetes 并部署容器化应用程序。在开始之前，你应该稍微了解一下什么是 Kubernetes 集群，以及将应用程序部署到集群时需要的组件。

### 理解 Kubernetes

Kubernetes 集群由节点组成，形成控制平面（用于管理集群）和数据面（用于运行负载）。对于个人使用，你可以在同一系统上运行控制和平数据面服务。例如，正如本章后面介绍的 Minikube，你可以从笔记本电脑上的虚拟机运行 Kubernetes 集群（https://minikube.sigs.k8s.io/docs/start/）。

在生产环境中，控制平面持续运行，而数据面可以根据工作负载的需求进行启动和关闭。如果你要建立生产级的 Kubernetes 基础设施，需要考虑的不同组件如下：

**控制平面：** 控制平面管理 Kubernetes 集群中运行的组件。它管理组件之间的通信，调度应用程序在数据面节点上运行，扩展应用程序，并确保正确数量的容器（分布在 pod 中）正在运行。控制平面可以运行在一个节点上，但你通常需要准备三个或更多可用节点，以确保控制平面服务始终可用。

**数据面：** 数据面是部署的容器实际运行的地方。你需要的节点数量取决于你的工作负载。对于本地集群，你可能希望高峰需求期间可能需要的最大数量节点，并在需要时引入节点，在不需要时撤销。对于云环境，云提供商通常有系统来处理你的数据面需求，因此你只需要根据需要为那些节点付费。如果你需要需求巨大的特殊类型（例如 GPU），你可能需要预留它们。

**存储：** 持久性网络化存储允许容器访问相同的存储，无论它们运行在哪些节点上。

**其他服务：** 为了将 Kubernetes 环境集成到现有的数据中心，你可能希望将其与身份识别和管理集成。在 Kubernetes 中，你用于部署的最小单元被称为 pod。pod 可以包含一个或多个容器，以及描述容器的元数据。

### 第31 章：使用容器部署应用程序

在 Kubernetes 中，你用于部署的最小单元被称为 `pod`。`pod` 可以包含一个或多个容器，以及描述容器的元数据。

### Kubernetes 控制平面

控制平面监督集群的所有活动。控制平面的核心是 API 服务器（`kube-apiserver`），它接收请求。集群中所有节点之间的通信都通过 API 服务器。当 API 服务器收到一个对象时（例如运行某些数量 pod 的请求），Kubernetes 调度器（`kube-scheduler`）会找到节点并调度到这些节点上。Kubernetes 控制器（`controller-manager`）持续运行执行诸如命名空间是否存在、服务账户是否可用、正确的副本数量是否运行以及定义的节点是否激活等操作。如果任何内容不同步，就会发出请求将这些对象恢复到请求状态，通过引入更多 pod 或重建缺失的节点。

### Kubernetes 数据面

Kubernetes 数据面每个节点的核心是 `kubelet`。`kubelet` 通过 API 服务器监控其节点。API 服务器 指令 `kubelet` 执行诸如运行 API 服务器 请求的容器，并确保其继续以健康状态运行。

每个节点上运行的另一个服务是容器引擎（通常称为运行时）。最初，Docker 服务是最流行的容器引擎，用于通过 `PodSpec` 启动、管理和删除容器。然而，在 Kubernetes v1.23 中，Kubernetes 中的 Docker 已被弃用，Docker 被 `containerd` 替换为 Kubernetes 的默认容器运行时。

# 第六部分：与云计算交互

响应此类请求，并确保这些请求在 Kubernetes *数据平面节点*上执行。

Kubernetes 使用服务（Services）的概念将应用程序的位置与其实际的 IP 地址和端口号隔离开。通过为提供该服务的 Pod 集合分配服务名称，集群不需要知道每个 Pod 的确切位置。相反，由 Kubernetes 来将对该服务的请求路由到可用的 Pod。

默认情况下，集群无法直接与活动 Pod 关联的 IP 地址进行通信。这需要你来定义如何将与 Pod 集合关联的服务暴露到集群外部。通过使用 `Service` 对象，你可以以不同的方式暴露服务。

默认情况下，通过 `ClusterIP` 类型暴露的服务使其仅对集群内部的其它组件可用。要向集群外暴露服务，可以使用 `NodePort`，它允许通过运行该 Pod 的每个节点上的外部 IP 地址上通过相同的 Kubernetes 分配的端口来访问提供服务的 Pod。

第三种方法是使用 `LoadBalancer` 分配一个外部的固定 IP 地址，作为提供服务的 Pod 的负载均衡器。通过 `LoadBalancer`，云厂商的外部负载均衡器会将流量重定向到后端 Pod。最后，你可以使用 `ExternalName` 暴露服务，将服务与特定的 DNS CNAME 记录关联。

无论你如何暴露 Kubernetes 服务，只要有对该服务的请求，Kubernetes 就会将通信路由到提供该服务的 Pod 集合。通过这种方式，Pod 的启动和关闭不会影响使用该服务的客户端。

# Kubernetes 接口

Kubernetes 既有命令行界面也有 Web 控制台用于访问 Kubernetes 集群。本章中的示例侧重于命令行工具。命令包括 `minikube`（用于管理 Kubernetes 虚拟机并启动/停止集群）以及 `kubectl`（用于管理 Kubernetes 集群的通用工具）。

# 尝试 Kubernetes

搭建生产级的 Kubernetes 集群需要一些预见性，本章将重点介绍几种简易的方法，让你快速运行并访问个人 Kubernetes 集群。特别是，有几种不同的方法可以让你访问 Kubernetes 集群：

- Kubernetes 教程：Kubernetes 官方网站提供了交互式的 Web UI 教程，你可以在那里启动自己的集群并尝试 Kubernetes。从 [Kubernetes Tutorials](https://kubernetes.io/docs/tutorials)，你可以选择基础、配置、无状态应用或其他教程主题。

- **Minikube**：通过 Minikube，你可以在自己的电脑上运行 Kubernetes。可以运行虚拟机的 Linux、macOS 或 Windows 系统可以在几分钟内在笔记本电脑或桌面系统上运行一个 Kubernetes 集群。[Minikube](https://kubernetes.io/docs/tutorials/hello-minikube) 包含了设置 Minikube 的说明。

- **K3s**：K3s (https://k3s.io/) 是一个为在 IoT 和远程位置运行而 Kubernetes 发行版。它适用于需要无人运行的配置。

- **MicroK8s**：对于想要纯 Kubernetes 体验的开发者，MicroK8s 提供了简单的安装和构建，并与最新的 Kubernetes 版本保持同步。

- **Docker Desktop**：另一个选项（此处未详述）是 Docker Desktop，它让你在工作站上拥有一个预配置的 Kubernetes 集群，并运行控制平面和节点。[Docker Desktop](https://docs.docker.com/desktop/features/kubernetes)。

为了开始，我将向你展示一些 Kubernetes 教程，并解释它们操作背后的概念。你可以跟随教程操作，或者在你的 Minikube 环境上运行这些命令。接下来我将描述如何通过这些方法之一获取 Kubernetes。

> 注意：如果你已经运行了 Amazon EKS 环境，你也可以在 EKS 中遵循大部分这些步骤。在大多数情况下，使用 `kubectl` 命令可以获得与 `minikube` 相同的结果。

# 获取 Kubernetes 

以下描述将告诉你如何通过安装或启动 Minikube，通过 Kubernetes 基础教程与 Kubernetes 集群交互。

# 启动 Kubernetes 基础教程

要启动 Kubernetes 项目基础交互式教程，请从浏览器浏览器访问以下 URL：

```
https://kubernetes.io/docs/tutorials/kubernetes-basics
```

图 31.1 显示了 Kubernetes 基础教程的开始。由于教程启动了一个实时集群，你也可以使用该界面尝试其他命令。

# 第六部分：与云计算交互

图 31.1

逐步进行 Kubernetes 教程。

![](img/a623301149fbdf7af5e6dcdd26f766e2_752_0.png)

# 启动 Minikube

在你的个人电脑上运行 Minikube 需要一些条件。这包括：

- 以具有 `sudo` 权限的用户登录。
- 使用配置为虚拟机管理程序（hypervisor）的计算机，以便运行 Minikube 虚拟机。你可以按照第 28 章“设置虚拟机管理器”部分的说明进行设置。
- 拥有 Minikube 需要的资源（两个或多个 CPU、2GB 或更多可用内存、20GB 或更多可用磁盘空间，以及连接连接）。
- 容器或虚拟机。

对于 Linux、macOS 和 Windows 系统，请访问此处查找最新说明：

https://minikube.sigs.k8s.io/docs/

这些是安装 minikube 的基本步骤：

- 1. **选择**操作系统、架构、发布类型和安装程序类型。例如，在具有稳定发布版本的 Linux x86_64 系统上，你可以运行以下命令来下载 minikube：

```
$ curl -Lo https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd4

$ sudo install minikube-linux-amd4 /usr/local/bin/minikube && rm minikube-linux-amd4
```

# 第31 章：使用 Kubernetes 部署应用程序

2. **启动集群**：以具有 `sudo` 权限的用户运行 `minikube start`。如果一切顺利，minikube 将找到你的虚拟机管理程序并创建 minikube 控制平面。此时你可以在集群上尝试一些 `kubectl` 命令并运行容器化应用程序。

3. **安装 kubectl 命令**：获取与你的 Kubernetes 版本匹配的 kubectl 版本。安装最新版本的 kubectl 和 minikube 即可。输入以下命令：

```
$ sudo curl -LO https://storage.googleapis.com/kubernetes-release/

$ release=$(curl -Ls https://storage.googleapis.com/kubernetes-release/stable.txt)

$ sudo mv $release/linux/amd64/kubectl /usr/local/bin/

$ sudo chmod 755 /usr/local/bin/kubectl
```

严格来说，你不需要单独获取 kube 二进制文件，因为 minikube 已经包含了。例如，你可以运行 `minikube node`。但在其他环境中，你会使用 `kubectl` 作为独立命令。

# 运行 Kubernetes 基础教程

Kubernetes 基础教程将带你通过一组良好的命令熟悉 Kubernetes：

https://kubernetes.io/docs/tutorials/kubernetes-basics

以下内容将直接带你通过 Kubernetes 教程页面的前五个模块进行操作，请启动 Minikube（`minikube start`）。如果你已经在笔记本电脑的虚拟机上使用 Minikube，仍然可以遵循此过程。步骤是相同的，因为两者都使用 Minikube。

## 获取集群信息

运行这些命令获取集群的基本信息：

- 1. **Minikube 版本**：查看你正在使用的 minikube 版本，输入以下命令：

```
$ minikube version

minikube version: v1.35.0

commit: dd5d320e41b5451cdcf30c1891bc4e1d189586ed-dirty
```

- 2. **集群信息**：查看 Kubernetes 主节点和 DNS 服务的 URL，输入以下命令：

```
$ kubectl cluster-info

Kubernetes control plane is running at https://localhost:36555

CoreDNS is running at https://localhost:36555/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```

## 第六部分：与云计算交互

为了进一步调试和诊断集群问题，请使用 `kubectl cluster-info dump`。

- 3. 列出节点信息：要查看运行的节点数量（Minikube 只有一个主节点）及其状态，请输入以下命令：

```
$ kubectl get nodes

NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   23m   v1.32.0
```

- 4. 列出集群和客户端版本：要列出 kubectl 客户端和 Kubernetes 集群的版本（确保它们之间的差异在一个版本以内），请输入以下命令：

```
$ kubectl version

Client Version: v1.31.0
Kustomize Version: v5.4.2
Server Version: v1.32.0
```

## 部署 Kubernetes 

在 Kubernetes 集群上运行管理容器化应用（以 pod 形式）的请求被称为部署（deployment）。当创建一个部署时，将由 Kubernetes 确保请求的 pod 始终运行。它通过以下方式实现这一点：

- 通过 API 节点接受部署创建请求
- 请求调度器在可用节点上运行每个 pod 中请求的容器
- 监控 pod 以确保它们按照请求继续运行
- 如果 pod 失败（例如容器停止运行），则启动一个新的 pod 实例（在相同或不同的节点上）

本教程展示了如何从容器镜像创建一个简单的部署示例。例如，你为它指定一个名称并标识要使用的容器镜像。部署的其他设置将使用默认值填充。

- 1. 创建部署：要启动一个名为 kubernetes-bootcamp 并拉取 kubernetes-bootcamp 镜像的部署，请输入以下命令：

```
$ kubectl create deployment kubernetes-bootcamp \
  --image=gcr.io/google-samples/kubernetes-bootcamp:v1

deployment.apps/kubernetes-bootcamp created
```

- 2. 列出部署：查看部署是否存在（并且有一个请求实例和一个运行中的实例），请输入以下命令：
