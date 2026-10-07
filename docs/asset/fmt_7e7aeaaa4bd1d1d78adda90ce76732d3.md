
要从当前目录下的 Dockerfile 创建容器，你可以运行 `docker build -t web directory`，其中 `directory` 是你系统上包含 Dockerfile 中 COPY 行参数所引用的文件的目录。如果这些文件和 Dockerfile 都在当前目录中，你可以使用 `docker build -t` 命令构建容器。容器构建完成后，你可以使用 `docker images` 命令查看你的容器镜像，并使用 `docker run` 命令在你的系统上运行它。要排查运行中的 Web 应用或微服务的问题，你可以使用 `docker logs -f container` 查看容器生成的日志，其中 `container` 是正在运行的容器的名称或 ID。

如果 Web 应用未启动，你可以使用 `docker remove image` 命令从系统中删除容器镜像。或者，如果 Web 应用或微服务运行成功，你可以使用 `docker push` 命令将容器镜像上传到 Docker Hub，其中 `username` 是你的 Docker Hub 用户名。

创建由多个微服务组成的 Web 应用的软件人员选择使用 `docker build` 命令创建每个微服务容器，并使用 `docker-compose` 命令在他们的工作站上一起运行它们进行测试。要使用 docker-compose 运行多个容器，你必须首先创建一个 `docker-compose.yml` 文件，其中包含应该运行的容器，以及每个容器所需的资源和网络设置。接下来，你可以在 `docker-compose.yml` 文件所在的目录下运行 `docker-compose` 命令来运行容器。

> 注意事项 47
有关可在 Dockerfile 或 `docker-compose.yml` 文件中使用的语法和选项，请参见 `docs.docker.com`。

## 在云中运行容器

一旦现有或新 Web 应用的代码更改作为 CI 过程的一部分（例如 Docker Hub）被部署并拉取，相关的容器镜像可以通过调度软件添加到云环境中的容器注册表中。在云环境中，Kubernetes 集群为 CD 工作流中的容器提供了编排和自动化，还可以被配置为与现有的构建自动化软件协同工作。该集群可用于测试、部署和管理容器，并根据需要扩展容器运行在许多不同的服务器上。

> 注意事项 48
Kubernetes 经常缩写为 K8s，它是字母 "K" 后面跟着 "8" 个字符和字母 "s"。

> 注意事项 49
可以安装在私有云、工作站或 IoT 环境中的 Kubernetes 版本称为 K3s。K3s 是去除了任何公共云提供商特定新增内容的 Kubernetes。

Kubernetes 集群包含系列虚拟机节点。一个或多个主节点（`master nodes`）提供管理集群的服务。集群中的所有节点都由主节点控制，并有一个运行容器的容器运行时。你在每个节点上运行的 Web 应用被称为 `pods`，由一个或多个相关容器以及可选的持久卷组成。图 13-8 展示了一个运行四个使用唯一 IP 地址标识的 pod 的示例 Kubernetes 节点。

### 图 13-8 示例 Kubernetes 节点

![](img/0065b92b6d2dfbf8ba2a41373880797d_575_0.png)

# 第13章 配置网络服务和云技术

> 注意事项 50
Kubernetes 经常缩写为 K8s，它是字母 "K" 后面跟着 "8" 个字符和字母 "s"。

> 注意事项 51
可以安装在私有云、工作站或 IoT 环境中的 Kubernetes 版本称为 K3s。K3s 是去除了任何公共云提供商特定新增内容的 Kubernetes。

虽然有许多管理工具可用，但管理 Kubernetes 最常用的工具是 `kubectl` 命令。因为 Kubernetes 几乎所有的配置都以 YAML 格式存储，你可以添加 YAML 获取 Kubernetes 设置。你也可以使用 `kubectl apply -f yaml.yaml` 配置组件。

## 在云中运行虚拟机

某些应用需要大量的处理器资源或存储，或者出于安全考虑需要操作系统。对于这些 Web 应用，在云提供商的虚拟机内部署它们更具成本效益。大多数云提供商在创建虚拟机时提供多个预配置的虚拟机模板供你使用，但你可以用自己创建的模板进行修改或替换。大多数云虚拟机托管开放虚拟格式（OVF）文件中，该文件使用 `.ovf` 扩展。

> 注意事项 52
你可以将虚拟机磁盘和虚拟机设置合并到一个文件中，以便于轻松导入云提供商。一种常见的虚拟机设备是开放虚拟归档（OVA），它将虚拟机磁盘和 `.ovf` 合并为一个使用 `.ova` 扩展的存档文件。

> 注意事项 53
与其拷贝虚拟机模板，你可以选择从云提供商的安装源向虚拟机磁盘手动安装操作系统。

要自定义运行在云提供商上的虚拟机模板，你可以使用配置管理（CM）软件。CM 软件允许你添加应用（Web 应用的新版本）、修改现有配置或为特定系统或系统组执行管理任务。由 CM 软件管理的系统统称为清单（`inventory`），每个系统都是清单成员。你有可供安装的 CM 软件软件包来管理你的清单；每种软件都提供了配置清单的不同方法。大多数 CM 软件软件包要求在每个清单成员上安装软件代理。某些 CM 软件软件包是无代理的；它们使用 SSH 连接到清单成员执行配置管理。某些 CM 软件要求你在脚本中定义必须在清单上执行的步骤（称为命令式配置），而 CM 软件仅要求你在配置文件指定清单成员必须具备的属性（例如应用和设置）（称为声明式配置）。

以下是一个针对三个清单成员（`server1`、`server2` 和 `server3`）的声明式配置简单示例，CM 软件可以使用其通过 `dnf` 安装 Apache（`httpd`）、添加首页（`index.html`）、启动 Apache、使用 `touch` 创建新文件（`/tmp/httplog`），并添加一个接收 Bash shell 登录的新用户：

```
name: Sample Declarative Configuration

hosts: server1,server2,server3

tasks:
  name: Install Apache
  dnf:
    name: httpd
    state: present
```
