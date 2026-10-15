
有状态的应用程序可以使用 `PersistentVolumeClaims`（`PVC`，持久卷声明）来请求存储。`PVC` 类似于 `Pod`。正如 `Pod` 消耗节点资源并可以请求特定级别的资源（`CPU` 和内存）一样，`PVC` 消耗持久卷资源，并且可以请求特定的大小和访问模式（例如，它们可以一次以读写方式挂载，或者多次以只读状态挂载）。`PVC` 允许用户消费抽象的存储资源，而提供这些资源的职责则属于平台。

#### 06 Services（服务）

服务将临时 `Pod` 连接到需要长期运行的内部或外部进程，例如 `API` 端点。假设你正在运行三个执行 Web 服务器容器的 `Pod`，并且你需要一种方式将从公共互联网传入的请求路由到你的容器。你可以通过设置一个使用负载均衡器将请求从公共 IP 地址路由到其中一个容器之一来实现这一点。给 `Pod` 打上一个标签，例如 `web_server`，然后在服务定义中说明：“使用任何标记为 `web_server` 的容器提供 `80` 端口的服务”。

#### 07 The kubectl tool（kubectl 工具）

要在 `Kubernetes` 上部署和管理应用程序，你可以使用 `Kubernetes` 命令行工具 `kubectl`。它允许你检查集群资源，创建、删除和更新组件，以及执行更多操作。使用以下命令安装 `kubectl`：

```bash
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```

你应该使用以下语法从终端窗口运行 `kubectl` 命令：

```bash
$ kubectl [command] [TYPE] [NAME] [flags]
```

...其中 `command` 指定你想要执行的操作，`TYPE` 指定资源类型，`NAME` 指定资源名称，而 `flags` 是命令的额外输入参数。

#### 08 Pick the right platform（选择合适的平台）

`Kubernetes` 安装没有任何先决条件；你可以在各种平台上安装它，从笔记本电脑到虚拟机，再到云提供商或裸机服务器。这里需要注意的是，你的集群容量取决于底层平台。对于希望熟悉 `Kubernetes` 的用户来说，最好的入门方式是使用 `Minikube`，这是一种基于本地 `Docker` 的解决方案。这会在你的笔记本电脑上创建一个单节点 `Kubernetes` 环境。对于像 `GCE` 和 `AWS` 这样的云提供商，设置 `Kubernetes` 很容易。虽然 `GCE` 默认提供 `Kubernetes` 支持，但对于 `AWS`，你可以使用 `kops` 工具。

#### 09 Deploy applications on Kubernetes（在 Kubernetes 上部署应用程序）

现在你已经了解了 `Kubernetes` 的各种构建块及其工作原理，我们将看看如何实际部署一个应用程序。为此，你需要创建一个由 `Kubernetes` 定义格式的配置。然后，你可以使用 `kubectl create` 命令并将配置文件传递给 `Kubernetes`。该命令的格式如下：

```bash
$ kubectl create -f config.yaml
```

另一个选项是使用 `Kubernetes` 包管理器 `Helm`。包管理器维护一个名为 `Helm charts` 的 `Kubernetes` 配置公共仓库。要通过 `Helm` 部署应用程序，你可以使用带有 `chart` 名称的 `helm install` 命令。例如，要安装 `Minio` chart，你可以使用：

```bash
$ helm install stable/minio
```

> 像 `Kubernetes` 这样的容器编排平台管理运行容器所需的所有裸机或虚拟机

## NATIVELY MANAGE A CLUSTER WITH DOCKER SWARM（使用 Docker Swarm 原生管理集群）

当你能够同时运行大量容器时，为什么要只使用一个容器呢？

虽然像 `Kubernetes` 和 `DC/OS` (`dcos.io`) 这样的项目正在构建能够处理不同容器格式的容器编排平台，但 `Docker Inc` 将容器编排与其核心产品 `Docker Engine` 集成在一起。从 `Docker Engine v1.12.0` 开始，`Swarm` 已内置，无需安装任何额外软件即可使用。不过，你需要网络连接的主机机器来运行容器集群。

这种 `Swarm` 与 `Docker Engine` 的集成意味着你可以原生管理一个 `Docker Engine` 集群。这意味着你可以使用 `Docker CLI` 创建 `swarm`，向 `swarm` 部署应用程序服务并管理 `swarm` 的行为。使用最新的 `Docker Engine v1.13.0`，你甚至可以使用 `Docker Compose` 文件来管理你的 `Docker swarm`。对于初学者来说，`Docker Compose` 是一个用于在单个节点上定义和运行多容器 `Docker` 应用程序的工具。`Compose` 在名为 `docker-compose.yml` 的文件上工作。截至 `Docker Engine v1.13.0`，`Docker Compose` 文件也可以用于配置多节点 `swarm`。`Swarm` 提供了你所需的所有生产就绪功能，包括负载均衡、服务发现、滚动更新、扩展等。我们稍后将学习所有这些功能。现在，只需记住，当你在不使用 `swarm` 模式的情况下运行 `Docker` 时，你执行的是容器命令。当你在 `swarm` 模式下运行 `Docker` 时，你编排的是服务。

![](img/6866071e033820549b214c239744aaa0_27_0.png)

| 名称 | 活动 | 期望 | 状态 | URL | SWARM | DOCKER ENGINES |
|:---|:---|:---|:---|:---|:---|:---|
| `lucy@sdc-dockerswarm10/101905 docker-machine` | | | | | | |
| `swarm-war-manager-1` | `*` | 单个 | 运行中 | `tcp://198.199.226.244:2376` | `v1:13.0` | |
| `swarm-war-manager-2` | `*` | 单个 | 运行中 | `tcp://198.199.226.223:2376` | `v1:13.0` | |
| `swarm-war-worker-3` | | 单个 | 运行中 | `tcp://198.199.226.228:2376` | `v1:13.0` | |
| `swarm-war-worker-4` | | | 运行中 | `tcp://198.199.226.185:2376` | `v1:13.0` | |

### 01 Swarm 管理节点

参与 `swarm` 的 `Docker Engine` 实例称为节点。`Swarm` 可以有两种类型的节点：管理者和工作者。管理节点是 `swarm` 中的控制机构，处理所有管理任务，例如向工作者分发任务，并执行维持 `swarm` 期望状态所需的编排和集群管理功能。当 `swarm` 中有多个管理节点时，它们会选举一个唯一的领导者来执行编排任务。即使你想向 `swarm` 部署应用程序，你也是将服务定义提交给管理节点。

| 名称 | 地址 | 容器 | 期望/活动 | 所需内存 | 限制 |
|:---|:---|:---|:---|:---|:---|
| `manager` | | `1/运行中` `1/运行中` `1/运行中` | | | |
| | | `198.199.226.244:338372` | | `1536M` | |
| | | | | `15%` `15%` `15%` `15%` | |
| `manager` | | | | | |
| `worker` | | `3/运行中` `3/运行中` `3/运行中` | | | |
| | | `198.199.226.244:338372` | | | |

### 02 Swarm 工作节点

工作节点也是 `Docker Engine` 的实例，其唯一目的是执行容器。工作节点不参与做出调度决策，也不提供 `swarm` 模式 `HTTP API`。你可以创建一个包含一个管理节点的 `swarm`，但你不能在没有至少一个管理节点的情况下拥有工作节点。默认情况下，所有管理者也是工作者。在单管理节点集群中，你可以运行诸如 `docker service create` 之类的命令，调度器会将所有任务放置在本地引擎上。

### 03 Swarm 服务
