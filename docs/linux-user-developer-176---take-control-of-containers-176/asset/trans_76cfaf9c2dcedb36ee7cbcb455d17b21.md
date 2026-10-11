
> “当你在不使用 Swarm 模式的 Docker 中运行时，你执行的是容器命令。当你在 Swarm 模式下运行时，你编排的是服务”

这意味着你可以使用 Docker Compose 格式创建一个文件，并用于在 Swarm 模式下部署服务。这不仅简化了部署过程，还使得轻松传递 Swarm 服务定义成为可能。

![](img/6866071e033820549b214c239744aaa0_28_0.png)

```
hosted-docker-dashboard swamd running pool "localhost-swarm-new" master-manager:1 ...
```

```
To add a worker to this swarm, run the following commands:
$ docker swarm join ...
```

## 05 Compose 文件格式

Compose 文件以版本部分开头。对于兼容 Swarm 的 Compose 文件，版本应为 3。接下来，你需要在 services 部分下定义要在 Swarm 中创建的服务。每个服务以服务名称开头，随后是 image 部分。在此你需要指定用于该服务的镜像。接下来，你需要添加 volumes、ports、network、environment 和 deploy 部分。最后，command 部分指示用于启动服务的命令。

## 06 负载均衡

Swarm 管理器使用入口负载均衡来暴露你希望提供给 Swarm 外部访问的服务。Swarm 管理器可以自动为服务分配 PublishedPort，或者你可以为服务配置 PublishedPort。你可以指定任何未使用的端口。在 Compose 文件中，ports 部分指定端口映射。如果你没有指定端口，Swarm 管理器将分配 30000-32767 范围内的一个端口给该服务。

## 07 创建 Swarm

要创建一个 Swarm，你需要在所有主机上安装 Docker Engine v1.12 或更高版本，并且所有机器上都要运行 Docker Engine 守护进程。此外，如果有网络连接这些主机，则端口 2377（用于集群管理）、7946（用于节点间通信）和 4789（用于创建覆盖网络）应该可用。一旦主机就绪，SSH 登录到你想用作管理器的机器，并初始化 Swarm：

```bash
$ docker swarm init --advertise-addr <MANAGER-IP>
```

在这里，你需要设置管理器机器的 IP 地址。

```
hosted-docker-dashboard:~$ docker-swarm-init --advertise-addr worker01-01
```

## 08 向 Swarm 添加节点

一旦你创建了带有管理器节点的 Swarm，你就可以准备添加工作节点了。打开终端并 SSH 登录到你想运行工作节点的机器。登录机器后，运行上一步 `docker swarm init` 输出中生成的命令，以创建加入现有 Swarm 的工作节点。或者，你可以使用命令：

```bash
$ docker swarm join-tokens worker
```

```
hosted-docker-dashboard:~$ docker swarm init
```

## 09 检查服务

你可以使用 Docker CLI 查看 Swarm 中运行的服务的所有详细信息。如果你还没有这样做，请打开终端并 SSH 登录到运行管理器节点的机器。然后，运行命令：

```bash
$ docker service inspect --pretty <SERVICE-ID>
```
...以易读的格式显示服务的详细信息。你可以使用其他 docker service 命令来探索服务详情。例如：

```bash
$ docker service ls
```
...显示所有正在运行的服务。

```bash
$ docker service ps <SERVICE-ID>
```
...显示为服务运行的所有任务。

# 特性

# 控制容器

# 使用 MESOSPHERE 运行企业级容器

这个分布式系统简化了在大型架构上构建和运行应用程序的过程

DC/OS 是一个基于 Apache Mesos 分布式系统内核的分布式操作系统。它使得将多台机器作为一个单一计算机进行管理成为可能。它自动化资源管理，调度进程放置，促进进程间通信，并简化和分布式服务的安装和管理。其 Web 界面和命令行界面促进了集群及其服务的远程管理和监控。

Apache Mesos 是 Mesosphere DC/OS 的核心开源分布式系统内核。Mesos 始于加州大学伯克利分校（BSD UNIX 的诞生地）的一个研究项目。受 Google 专有的 Borg 系统的启发，该项目的目标是创建一个开源内核，简化在非常大的规模上构建和运行分布式应用程序，并将整个数据中心视为一个巨大的超级计算机，同时保持可扩展的架构。

![](img/6866071e033820549b214c239744aaa0_29_0.png)

传统的单体调度器维护底层应用程序和基础设施的完整状态，同时执行工作负载放置逻辑。这种架构使得扩展变得非常具有挑战性，引入新特性和功能更加困难。通过双层级架构，Mesos 处理底层基础设施调度操作，而顶层的另一层（框架）处理所有特定于应用程序的操作和逻辑。

![](img/6866071e033820549b214c239744aaa0_29_1.png)

主节点（masters）编排运行在 Mesos 代理上的任务。它接收来自 Mesos 代理的资源报告，并将这些资源分配给已注册的 DC/OS 服务，例如 Marathon 或 Spark。Mesos 代理节点代表框架运行离散的 Mesos 任务。私有代理节点通过不可路由网络运行已部署的应用和服务。公共代理节点在公共可访问网络中运行 DC/OS 应用和服务。

![](img/6866071e033820549b214c239744aaa0_29_2.png)

预置容器镜像（AppC 也即将推出）。这意味着你可以在 DC/OS 中同时使用 Mesos 容器化程序和容器镜像类型。你还可以直接通过 DC/OS 使用 Docker 容器运行时，但通用容器运行时支持运行 Docker 镜像而不依赖于 Docker Engine，从而实现了与 Mesos 的更好集成。

## 01 架构

DC/OS 内核空间由 Mesos 主节点和 Mesos 代理组成。用户空间包括系统组件，如 Mesos-DNS、分布式 DNS 代理，以及服务，如 Marathon 和 Spark。用户空间还包括由服务管理的过程，例如 Marathon 应用程序。Mesos

## 02 Mesos 容器化程序

容器化程序允许你在容器中运行任务。DC/OS 支持两种容器化程序类型 – DC/OS 通用容器运行时和 Docker 容器化程序。通用容器运行时扩展了 Mesos 容器化程序以支持

![](img/6866071e033820549b214c239744aaa0_30_0.png)

## 03 DC/OS 安装

你可以通过使用自定义设置文件或云模板在任何你想要的环境中安装 DC/OS。针对所有主要云基础设施提供商都有详细的说明步骤。你还可以使用 Vagrant 在本地机器上创建虚拟机集群，用于 DC/OS 的演示、开发和测试。

## 04 Mesos 执行器和调度器

Mesos 调度器定义新的 Mesos 任务并为其分配资源（将其放置在特定节点上）。调度器接收描述 CPU、RAM 等的资源报价，并将它们分配给可由 Mesos 代理通过执行器启动的离散任务。

执行器进程由代理节点上的 Mesos 代理启动和管理。Mesos 任务由其调度器定义为由特定执行器（或默认执行器）运行。每个执行器运行在属于自己的容器中。

![](img/6866071e033820549b214c239744aaa0_30_1.png)

## 05 Marathon

Marathon 是 DC/OS 的生产级容器编排平台。它是 DC/OS 的核心组件，也是在 DC/OS 集群启动后第一个被引导的框架。这是因为 Marathon 还运行其他 Mesos 框架。

Marathon 支持 Mesos 容器（使用组）和 Docker。你还可以通过将持久存储卷绑定到应用程序来运行有状态应用。这意味着像 MySQL、Postgres 这样的数据库和像 Minio 这样的对象存储可以轻松部署在 DC/OS 上，并且其存储由底层平台计算。

## 06 Chronos

Chronos 是一个用于运行基于计划和依赖关系的作业的 Mesos 调度器。

![](img/6866071e033820549b214c239744aaa0_30_2.png)

你可以将 Chronos 视为 cron 的替代方案。它是一个分布式且容错的调度器，运行在 Apache Mesos 之上，可用于作业编排。使用 Chronos 调度的作业配置有基于 ISO8601 的具有重复间隔的计划。通常，作业被计划无限期运行，例如每天或每小时一次。依赖作业可能有多个父级，一旦所有父级自依赖作业上次调用以来都成功调用过至少一次，它们就会被触发。

## 07 应用程序

像 WordPress、Jenkins 或其他此类实际应用程序可以作为 Marathon 应用程序部署在 DC/OS 上。应用程序通常是一个长期运行的服务，在许多主机上运行许多实例。每个应用程序实例称为一个任务。应用程序定义描述了启动和维持任务所需的一切。我们将在接下来的步骤中了解如何编写应用程序定义。

## 08 应用程序配置

在 DC/OS 中，应用程序可以定义为 JSON 文件。让我们以一个打印短语“Hello Marathon”的简单应用程序为例。创建一个 JSON 文件并添加以下详细信息：

```json
{
  "id": "basic-0",
  "cmd": "while [ true ] ; do echo 'Hello Marathon' ; sleep 5 ; done",
  "cpus": 0.1,
  "mem": 10.0,
  "instances": 1
}
```

上面的例子是执行的命令。它的值由底层的 Mesos 执行器通过 /bin/sh -c $(cmd) 包装。然后你可以将服务添加到 DC/OS：

```bash
$ dcos marathon app add <your-service-name>.json
```

完成后，Marathon 将执行权移交给 Mesos。Mesos 为每个任务创建一个沙箱目录。沙箱目录是代理节点上的一个目录，作为执行环境并包含相关的日志文件。

## 09 在应用程序中使用资源

为了运行需要诸如文件等资源非平凡应用程序，Marathon 有 URI（统一资源标识符）的概念。URI 使用 Mesos 获取器在下载（以及可能的）资源提取方面做繁重的工作。

```json
{
  "id": "basic-1",
  "cmd": "chmod u+x cool-script.sh && ./cool-script.sh",
  "cpus": 0.1,
  "mem": 10.0,
  "instances": 1,
  "uris": [ "http://example.com/app/cool-script.sh" ]
}
```

上面的例子执行命令，下载 cool-script.sh 资源（通过 Mesos）并使其在服务的 Mesos 沙箱中可用。运行使用 Docker 镜像的应用程序很简单，为什么不试试呢？例如，这是如何在 DC/OS 中创建一个简单的 Docker 应用：

```json
{
  "id": "basic-3",
  "cmd": "python3 -m http.server 8080",
  "cpus": 0.5,
  "mem": 32.0,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "python:3",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 8080, "hostPort": 0 }
      ]
    }
  }
}
```

