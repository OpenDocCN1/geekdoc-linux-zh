

# 更多操作

### Kubernetes 主节点 (master)
- API server
- 用户
- 调度器 (Scheduler)
- 开发者操作
- etcd

### Kubernetes 节点 (node)
- Kubelet
- containvisor
- Kube-Proxy
- Kubelet
- containvisor
- Kube-Proxy

### Pod
- Pod
- Pod
- Pod
- Pod
- Pod
- 网络插件 (Flannel, Weave 等)

这是一个展示主运行关键组件和节点的概述。请注意，在实践中，由于数据存储和内存的需求，主组件可能会分布在多个节点上。通过容器编排，这一切（以及更多）都得到了解决。我们只需指定所需的内容，我们的编排工具就会满足这些需求。我们指定想要的内容，以及希望实现的方式。

# 成为 Kubernetes

Kubernetes (ku-be-ner) 是目前领先的编排工具，源于 Google。Kubernetes 的起源是 Google 的内部项目，用于运行 Google 大多数应用程序，包括其搜索引擎、Google Maps 等。当 Google 在 2015 年解密并发布了关于它的论文时，主项目揭示了 Borg 是 Kubernetes 背后的编排系统。

Borg 是一个管理 Google 数据中心集群的系统，它确保 Google 的应用程序（包括生产和开发）能够应对硬件故障、资源耗尽或其他可能导致中断的问题。它通过仔细监控组成 Borg 的数千个节点以及运行在上面的容器，根据问题或负载波动按需启动或停止容器。

Kubernetes 出生于 Google 的 GAFEE（Google 所有人基础设施），被设计为 Borg 的更友好版本，可以在 Google 之外发挥作用。它在 2015 年通过云原生计算基金会 (CNCF) 的成立捐给了 Linux 基金会。

Kubernetes 提供了一个用于“声明”容器应用程序和服务的系统，并确保您的应用程序按照这些声明运行。如果应用程序需要存储或网络等外部资源，Kubernetes 可以自动提供它们。您可以使用几个命令扩展或缩小应用程序，并轻松地扩展整个集群。您的 Kubernetes 确保您不需要知道它们运行在哪里；Kubernetes 为应用程序提供命名服务，以便它们可以连接到“端点”并在组件之间实现无缝连接。

最终结果是一个可以运行您应用程序的平台，从本地机架上的单个集群到云端的虚拟机，都使用相同的容器和配置。Kubernetes 是与供应商无关的：运行它

# ALIEN BENIGENS

# “Kubernetes 的起源是 Borg，一个用于运行 Google 大多数工具的 Google 内部项目”

Kubernetes 是一个强大的工具，而且几乎非常复杂。在我们进入概述之前，我们需要介绍 Kubernetes 内部术语。上述应用程序被分组在 Pod 中。Pod 是一组部署在同一主机上并共享资源的紧密关联容器。Pod 中的容器可以执行不同的功能，例如一个应用程序容器和一个带有应用程序特定服务的日志容器。

Kubernetes 组件包括 API Server、调度器 (Scheduler)、控制器管理器 (Controller Manager) 和配置数据库 etcd。API Server 是 Kubernetes 的心脏，端点管理控制器可能由 Kubernetes 组件（如调度器）通过命令行或 Web 界面等生成。它验证请求并更新 etcd 中的数据。

调度器决定 Pod 将运行在哪些节点上，并考虑了资源需求、硬件或软件限制、工作负载和截止日期等约束。

# 查看这些资源

如果您不熟悉 Docker（也称为 LXC），请从这里开始：https://docs.docker.com/started/。这里有一个开发和部署应用程序的交互式教程：https://kubernetes.io/docs/tutorials/basics/，用于查看如何构建 Kubernetes 集群。您可以在 https://trykill.com/ 玩免费集群，或者为了更多长期信息，可以在此处查看 Google Kubernetes 的优秀概述：https://storage.googleapis.com/cloud-tools-public-publication-data/4343.pdf

控制器管理器监控集群状态，并将通过 API Server 按需启动或停止 Pod，将集群桥接到所需状态。它还管理内部连接和安全令牌。

每个节点使用 Docker 和 Kube-Proxy 与 API server 以及容器通信，这些工具处理集群内部的代理和负载均衡。

etcd 分布式数据库系统的名称源于 Linux 系统中的警报（alert），用于存储配置信息；后缀 ‘cd’ 表示数据（data）。API server 保留集群中的所有状态。调度器和控制器管理器只能有一个实例。这意味着 Kubernetes 可以高可用运行而没有单点故障。

![](img/5f8379eaeda72d04307c37d75b0ba5d_80_0.png)

使用仪表板 (dashboard) 可以快速查看 Kubernetes。

# 整合一切

我们在实践中如何使用这些组件？这里遵循一个使用 Kubernetes 设置 WordPress 的示例。如果您想独立完成，您可能会使用一种名为 Helm 的配方。Helm 适用于许多常用应用程序，但在这里我们将查看让 WordPress 运行的步骤。

第一个任务是定义 MySQL：`kubectl create secret mysql --literal-password=` 将与 API Server 通信，它将验证命令。我们的服务定义在 YAML 中，我们需要为 MySQL 提供一些持久存储。

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
name: mysql-claim
labels:
  app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    storage: 20Gi
```

该规范自言易明。名称和标签用于从 Kubernetes 的其他部分引用此存储，这就是我们定义它们的原因。

一旦定义了数据库，我们就定义一个 MySQL 实例，指向预定义的存储。接下来是定义数据库本身；我们获得了每个服务的名称和标签。

现在我们需要另一个容器来运行 WordPress。

```yaml
kind: Deployment
name: wordpress
labels:
  app: wordpress
spec:
  type: Recreate
```

策略 ‘Recreate’（重建）意味着如果任何代码发生更改，运行的实例将被删除并重建。其他选项允许在创建新实例的同时删除现有实例，这在部署更新时非常有用。最后，我们为 WordPress 创建一个服务，使用 PHP 和 Apache。YAML 部分如下：

```yaml
kind: Service
name: wordpress
labels:
  app: wordpress
spec:
  ports:
    - port: 80
  selector:
    app: wordpress
  type: LoadBalancer
```

注意最后一行，将类型定义为 LoadBalancer。这指示 Kubernetes 在 Kubernetes 外部提供该服务。如果没有这一行，该服务将是仅限内部”的服务。

Kubernetes 将使用这些 YAML 文件作为所需内容的声明，并按需要设置 Pod、连接等，以使集群进入“所需”状态。

这只是 Kubernetes 的高层概述，我们忽略了系统的许多细节和功能。我们将涵盖自动伸缩（同时针对 Pod 和组成集群的节点）、定时任务（根据计划启动容器）、（HTTP 负载均衡、路由和 SSL 卸载）、RBAC（基于角色的访问控制）、网络（防火墙）等。Kubernetes 对于任何新的 IT 基础设施来说都是极其灵活且强大的，它必须是一个

![](img/5f8379eaeda72d04307c37d75b0ba5d_80_1.png)

