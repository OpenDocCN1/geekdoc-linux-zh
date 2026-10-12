
Kubernetes 提供了一个系统，你可以在此系统中“声明”你的容器化应用程序和服务，它确保你的应用程序按照这些声明运行。如果你的程序需要外部资源，如存储或负载均衡器，`Kubernetes` 可以自动配置这些资源。它可以随负载变化自动扩展你的应用程序，甚至可以在需要时扩展你的整个集群。你的程序组件甚至不需要知道它们在哪里运行：`Kubernetes` 为应用程序提供内部命名服务，使它们可以相互连接并自动连接到正确的资源。

最终结果是一个平台，可用于在任何基础设施上运行你的应用程序，从单台机器到本地机架系统，再到运行在任何主要云提供商上的基于云的虚拟机集群，全部使用相同的容器和配置。`Kubernetes` 与提供商无关：在任何你想运行的地方运行它。

### 成为 Kubernetee

`Kubernetes`（ku-ber-net-ez）是当今领先的容器编排工具，它来自 `Google`。如果有人知道如何运行大规模 IT 基础设施，那就是 `Google`。`Kubernetes` 的起源是 `Borg`，这是 `Google` 的一个内部项目，至今仍用于运行 `Google` 的大多数应用程序，包括其搜索引擎、`Gmail`、`Google Maps` 等。`Borg` 在 2015 年 `Google` 发表关于它的论文之前一直是个秘密，但这篇论文清楚地表明，`Borg` 是 `Kubernetes` 的主要灵感来源。

`Borg` 是一个管理 `Google` 数据中心中计算资源的系统，尽管发生硬件故障、资源耗尽或其他可能导致停机的问题，它仍确保 `Google` 的应用程序（包括生产环境和其他环境）持续运行。它通过仔细监控组成 `Borg`“单元”的数千个节点及其上运行的容器，并根据问题或负载波动启动或停止容器来实现这一点。

> **查看这些资源**

> 如果你不熟悉 `Docker`（另见 *LXF237 中的教程*），请从这里开始：[https://docs.docker.com/get-started.](https://docs.docker.com/get-started.) 这里有一个关于部署和扩展应用程序的交互式教程：[https://kubernetes.io/docs/tutorials/kubernetes-basics.](https://kubernetes.io/docs/tutorials/kubernetes-basics.) 请参阅 [https://kubernetes.io/docs/setup/scratch](https://kubernetes.io/docs/setup/scratch) 了解如何构建集群。你可以在 [https://tryk8s.com.](https://tryk8s.com.) 上体验免费的 `Kubernetes` 集群。最后，你可以在这里仔细阅读一篇长篇技术论文，其中出色地概述了 `Google` 对 `Borg` 的使用及其对 `Kubernetes` 设计的影响：[https://storage.googleapis.com/pub-tools-public-publication-data/pdf/434343.pdf.](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/434343.pdf.)

### 外星起源

> “`Kubernetes` 的起源是 `Borg`，一个用于运行 `Google` 大多数工具的 `Google` 内部项目”

`Kubernetes` 是一个强大的工具，必然也是复杂的。在我们进入概述之前，我们需要介绍 `Kubernetes` 中使用的一些术语。

-   如前所述，容器运行单个应用程序，并组成 `Pod`。`Pod` 是一组紧密关联的容器，部署在同一主机上并共享一些资源。`Pod` 内的容器作为一个团队工作：它们执行相关功能，例如应用程序容器和针对该应用程序具有特定设置的日志记录容器。

-   `Kubernetes` 的四个关键组件是 API 服务器、调度器、控制器管理器以及一个名为 `etcd` 的分布式配置数据库。API 服务器是 `Kubernetes` 的核心，作为所有管理请求的主要端点。这些请求可能来自多种来源，包括其他 `Kubernetes` 组件（如调度器）、通过命令行或基于 web 的仪表板的管理员，以及容器化应用程序本身。它验证请求并更新存储在 `etcd` 中的数据。

-   调度器确定各个 `Pod` 将在哪些节点上运行，同时考虑资源需求、任何硬件或软件约束、工作负载、截止日期等约束。

控制器管理器（Controller Manager）负责监控集群状态，并通过 API 服务器（API Server）在必要时尝试启动或停止 `Pod`，以使集群达到期望状态。它还管理一些内部连接和安全特性。

每个节点都运行一个 `Kubelet` 进程，该进程与 API 服务器进行通信并管理容器（通常使用 `Docker`），以及 `Kube-Proxy`，后者负责处理集群内的网络代理和负载均衡。

`etcd` 分布式数据库系统的名称源自 Linux 系统中的 `/etc` 文件夹，该文件夹用于存储系统配置信息，再加上后缀“d”，后者通常用来表示守护进程。`etcd` 的目标是以分布式、一致且容错的方式存储键值数据。

API 服务器将其所有状态数据保存在 `etcd` 中，并且可以并发运行多个实例。调度器（scheduler）和控制器管理器只能有一个活动实例，但使用租约（lease）系统来确定哪个运行实例是主节点。这意味着 `Kubernetes` 可以作为一个高可用系统运行，没有单点故障。

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_80_0.png)

> 使用仪表板视图获取 `Kubernetes` 运行情况的概览摘要。

## 将所有部分结合起来

那么我们在实践中如何使用这些组件呢？下面是一个使用 `Kubernetes` 搭建 `WordPress` 网站的示例。如果你真想这样做，你可能会使用一种称为 Helm Chart 的预定义配方。许多常见应用程序都有可用的 Helm Chart，但在这里，我们将查看在 `Kubernetes` 上启动并运行 `WordPress` 网站所需的一些步骤。

```
kubectl create secret generic mysql-pass --from-literal-password=YOUR_PASSWORD
```

`kubectl` 将与 API 服务器进行通信，API 服务器将验证该命令，然后存储密码到 `etcd`。

我们的服务在 YAML 文件中定义，现在我们需要为 MySQL 数据库提供一些持久存储。

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi
```

该规格说明应该大多不言自明。`name` 和 `labels` 字段用于从 `Kubernetes` 的其他部分引用此存储，在本例中是我们的 `WordPress` 容器。

一旦定义了存储，我们就可以定义一个指向预定义存储的 MySQL 实例。随后是定义数据库本身。我们为那个数据库指定一个名称和标签，以便在 `Kubernetes` 中轻松引用。

现在我们需要另一个容器来运行 `WordPress`。容器部署规格的一部分是：

```yaml
kind: Deployment
metadata:
  name: wordpress
```

```yaml
name: wordpress
labels:
  app: wordpress
spec:
  strategy:
    type: Recreate
```

策略类型“`Recreate`”意味着，如果组成应用程序的任何代码发生变化，那么运行实例将被删除并重新创建。其他选项包括能够循环引入新实例并移除现有实例，一个接一个地移除，从而在部署更新期间使服务继续运行。最后，我们为 `WordPress` 本身声明一个服务，包括 PHP 代码和 Apache。声明此服务的 YAML 文件的一部分是：

```yaml
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  ports:
    - port: 80
  selector:
    app: wordpress
    tier: frontend
  type: LoadBalancer
```

注意最后一行，将服务类型定义为 `LoadBalancer`。这指示 `Kubernetes` 使该服务在 `Kubernetes` 外部可用。如果没有该行，这仅仅是一个内部的“仅限 `Kubernetes`”服务。

就这么简单。`Kubernetes` 现在将这些 YAML 文件用作所需内容的声明，并设置所需的 `Pod`、连接、存储等，以使集群达到“期望”状态。
