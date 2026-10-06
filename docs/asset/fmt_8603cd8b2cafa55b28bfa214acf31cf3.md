
`cfb44e2d4c2d1ef6d6ba3e501da4691b2eae3b96a01fe95fe9b` ex/webapp "`app.js`" 44a ago Up 43h 36002->80/tcp cust2

`c4b6e8f4b8e8f5f` ex/webapp "`app.js`" 51s ago Up 50s 36001->80/tcp cust1

`[root@server1]# #`

```
```

`docker` 命令的 `-d` 选项从你的终端显示容器的输出详情，并保持容器运行，直到你使用 `stop` 命令将其停止。例如，`docker stop cust2` 命令将停止 `cust2` 容器并将其资源释放给操作系统；当 `cust2` 登出用于管理其 IoT 网站时，这可能会自动触发。同样，当触发 `cust2` 稍后登录网站管理其 IoT 设备时，`docker start cust2` 命令将再次运行容器。

你还可以使用 `docker exec` 命令在运行的容器内访问 shell。例如，`docker exec -it cust2` 应该连接到 `cust2` 容器并运行交互式 shell 以供你进行配置更改。

> 注意事项 45
你可以在任何 `docker` 命令中使用 `--help` 选项来获取可用选项和信息。例如，`docker --help` 将显示 `docker` 命令的通用选项和用法，`docker run --help` 将显示 `docker run` 命令的用法。

# 微服务

软件开发人员还可以设计由多个较小程序（称为微服务）组成的 Web 应用程序，每个程序在 Web 中执行独特的功能并在它们自己的容器中运行。例如，开发者可以在另一个容器中创建一个 JavaScript 微服务，用于收集数据并使用机器学习（人工智能）分析来自 JavaScript 微服务的数据。这两个微服务收集和分析的数据可以通过另一个包含 PostgreSQL 服务的容器进行存储和检索，该容器可以访问网络上的持久化卷（例如 NFS 共享目录）或由云提供者直接提供的卷。图 13-7 描述了这种结构。

图 13-7 由三个微服务组成的 Web 应用程序

## 第13 章 配置网络服务与云技术

> 注意 46
运行在不同容器中的微服务可以相互直接通信，也可以通过名为服务网格（service mesh）的特殊代理服务进行通信，该服务提供了额外的安全和监控功能。

由微服务组成的 Web 应用更容易开发、修复和演。例如，软件开发人员只需要修改 Python 微服务并重新部署相关的容器。

## 创建容器

在开发过程中，软件开发人员会在工作站上创建并运行容器以测试他们的 Web 应用。要创建一个容器，你必须创建一个名为 `Dockerfile` 的文件，其中包含生成容器的指令。以下示例 `Dockerfile` 指定了新容器应该基于 Docker Hub 上最新的 Ubuntu 容器镜像，但安装了 `postgresql`、`ruby-3.1.0` 和 `libcap-dev` 软件包。此外，当前目录中的所有文件都会复制到容器中；通常，这些是组成 Web 应用或微服务的文件。当容器运行时，容器内的 `ruby` 命令将带有 `/app/main.rb` 运行 Web 应用或微服务，并且相关的端口号（5059）将对外部客户端可用。

```
@server1]# cat Dockerfile

FROM ubuntu:latest

RUN install -y postgresql ruby-3.1.0 libcap-dev

COPY . /app

CMD ["/app/main.rb"]

EXPOSE 5059

@server1]# 
```

要从当前目录下的 `Dockerfile` 创建容器，你可以运行 `container build -t web directory`，其中 `directory` 是你系统上的目录，包含 `Dockerfile` 中 `COPY` 行第一个参数所引用的文件。如果文件和 `Dockerfile` 都在当前目录中，你可以使用 `docker build -t web` 命令来构建容器。容器构建完成后，你可以使用 `docker images` 查看你的容器镜像，并使用 `docker run` 命令在你的系统上运行它。要排查容器运行时 Web 应用或微服务的问题，你可以使用 `docker logs -f container` 命令查看容器生成的事件日志，其中 `container` 是你正在运行的容器的名称或 ID。

如果 Web 应用未运行，你可以使用 `docker rmi` 命令从系统中删除容器镜像。或者，如果 Web 应用或微服务运行成功，你可以使用 `docker push` 命令将容器镜像上传到 Docker Hub。创建由多个微服务组成的应用的软件开发人员可以选择使用 `docker build` 命令创建每个微服务容器，然后使用 `docker-compose` 命令在工作站上共同运行它们进行测试。对于使用 `docker-compose` 的多个容器，你必须先创建一个 `docker-compose.yml` 文件，列出应该运行的容器，以及每个容器所需的资源和网络设置。接下来，你可以在 `docker-compose.yml` 文件所在的相同目录下运行 `docker-compose up` 命令来运行容器。

> 注意 47
有关可在 `Dockerfile` 或 `docker-compose.yml` 文件中使用的详细语法和选项，请参阅 `docs.docker.com`。

## 在云中运行容器

一旦现有或新 Web 应用的代码更改作为 CI 过程（例如 Docker Hub）的一部分被应用，就可以通过编排软件将相关的容器镜像添加到云环境中的容器注册库中。在云环境中，Kubernetes 集群为 CI 工作流中的容器提供了编排和构建自动化，还可以被配置为与现有的构建自动化软件协同工作。该集群用于测试、部署和管理容器，并根据需要扩展容器运行在许多不同的服务器上。

> 注意 48
Kubernetes 经常缩写为 `K8s`，即字母 "K" 后面跟着 "8" 个字符和字母 "s"

> 注意 49
一种可以安装在私有云、工作站或 IoT 环境中流行的 Kubernetes 版本称为 `K3s`。`K3s` 是去除了任何公共云提供商特定新增内容的 Kubernetes。

Kubernetes 集群包含一系列称为节点（nodes）的虚拟机。一个或多个主节点提供管理集群的服务。集群中的所有节点都由主节点控制，并有一个用于运行容器的容器运行时。你在每个节点上运行的 Web 应用被称为 `pod`，可能由一个或多个容器以及可选的持久卷组成。图 13-8 展示了一个运行四个使用唯一 IP 地址标识的 `pod` 的 Kubernetes 节点。

## 图 13-8 Kubernetes 节点

![](img/12ad6df66c6622b4ab7acf53dfd7f646_574_0.png)

## 第13 章 配置网络服务与云技术

> 注意 50
软件开发人员经常在工作站上创建一个单节点 Kubernetes 集群来测试 Web 应用。在这种情况下，有一个主节点，该节点也包含一个用于运行容器的容器运行时。

> 注意 51
`pod` 中的所有容器可能并不参与提供 Web 应用功能。例如，你可能在 `pod` 中有一个用于监控 `pod` 或提供服务网格功能的容器；这些第三方容器被称为 `sidecar` 容器（旁路容器）。另一个例子是 `ambassador` 容器，它们将来自 `pod` 中其他容器的请求发送到 `pod` 外部的服务，例如对象存储。

要将 Web 部署到 Kubernetes 集群，你必须配置一个部署，以确定如何在每个节点上启动、管理和扩展集群，以及一个允许从节点外部访问 `pod` 的服务。为了从集群外部访问服务，你需要设置负载均衡器或入器控制器（ingress controller）。公共云提供商提供自己的路由流量的负载均衡器服务。或者，你可以使用入器控制器来路由流量。图 13-9 显示了一个扩展到三个节点的 Kubernetes 集群。

## 图 13-9 Kubernetes 集群

![](img/12ad6df66c6622b4ab7acf53dfd7f646_575_0.png)

虽然有图形化管理工具可用，但管理 Kubernetes 最常用的工具是 `kubectl`。由于 Kubernetes 将几乎所有的配置都以 YAML 格式存储，你可以使用 `kubectl` 来获取设置。你还可以使用 `kubectl apply` 来配置组件。

## 在云中运行虚拟机

某些应用需要大量的专用处理器资源或存储空间，或者一个操作系统。对于这些应用，在云提供商的虚拟机内部部署更具成本效益。大多数云提供商提供几个预配置的虚拟机模板供你使用，但你可以用自己创建的模板替换它们。每个虚拟机模板由一个虚拟磁盘（包含预装的操作系统）以及定义虚拟机设置（如内存和硬件）的一个或多个文件组成。云的大多数虚拟机设置使用使用 `.ovf` 扩展 Open Virtualization Format (`OVF`)。

> 注意 52
你可以将虚拟硬盘和虚拟机设置合并到一个文件中，以便方便地导入云提供商。一种常见的虚拟机设备格式是 Open Virtualization Archive (`OVA`)，它将虚拟磁盘和 `.ovf` 文件合并为一个使用 `.ova` 扩展名的归档文件。

> 注意 53
与其复制虚拟机模板，你选择从云提供商的安装文件手动向虚拟磁盘安装操作系统。

要自定义运行在云提供商上的虚拟机模板副本，你可以使用配置管理（CM）软件。配置管理软件允许你添加应用（包括新版本的应用）、修改现有配置，或为特定系统或网络上的系统组执行管理任务。由配置管理软件管理的系统统称为清单（inventory），每个系统都是清单成员。有许多配置管理软件包可供安装以管理你的清单；每种软件提供了不同的清单配置方法。大多数配置管理软件包是无代理的：使用 `SSH` 连接到清单成员以执行配置管理。某些配置管理要求你在脚本中定义必须在清单上执行的单独步骤（称为命令式配置），而配置管理软件只需要在配置文件中指定清单成员必须具备的属性（例如应用和设置）（称为声明式配置）。

以下示例展示了使用 `dnf` 配置 Apache、启动 Apache、使用 `touch` 创建新文件 (`/tmp/httplog`) 以及添加一个登录后接收 Bash shell 的新用户：

```
name: Sample Declarative Configuration

hosts: server1,server2,server3

become: true

tasks:
  - name: Install Apache
    dnf:
      name: httpd
      state: present
```
