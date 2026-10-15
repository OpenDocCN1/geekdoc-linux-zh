
```
RUN apt-key adv --keyserver http://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo "deb http://repo.mongodb.org/apt/ubuntu\ 14.04 release -x04/mongodb-org/3.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.0.list
```

然后安装 MongoDB：

```
RUN apt-get update && apt-get install -y mongodb-org
```

MongoDB 还需要一个数据目录。使用以下命令创建它：

```
RUN mkdir -p /data/db
```

最后，将容器的相关端口暴露给主机，并设置入口点为 MongoDB 守护进程：

```
EXPOSE 27017
ENTRYPOINT ["/usr/bin/mongod"]
```

保存此文件。我们现在可以继续从这个 `Dockerfile` 构建镜像。要构建镜像，请在终端中输入以下内容：

```
$ docker build --tag mymongodb .
```

这告诉 `Docker` 从当前目录中的 `Dockerfile`（注意结尾的 `.`）构建一个镜像，并将其标记为 `mymongodb`。现在你的 MongoDB 镜像已经准备就绪可以运行了。让我们从该镜像生成一个容器。

```
$ docker run -p 27017:27017 --name mongo_db_instance_01 -d mymongodb
```

这创建了一个名为 `mongo_db_instance_01` 的容器并执行它。你可以使用以下命令检查当前正在运行的容器：

```
$ docker ps
```

最后，你可以通过运行以下命令连接到 MongoDB 容器：

```
$ mongo --port 27017
```

- 需要自动化测试流程吗？使用 `Daisi` 等工具，它们从仓库获取代码，然后以 `Docker` 容器的形式将其部署到预定义的硬件节点上。

`Docker` 在实施新的 `DevOps` 成功路径方面提供了极大的灵活性。现在让我们来看看一些使 `Docker` 成为灵活工具的关键功能。

### 联合文件系统

`Docker` 鲜为人知的功能之一是联合文件系统。虽然对最终用户来说并不显见，但联合文件系统在后台工作，以实现在旧容器之上构建新容器，从而避免重复劳动。让我们可视化这个过程。每个 `Docker` 镜像都始于一个基础镜像。当你在 `Dockerfile` 中添加指令时，每条指令都会在结果镜像中创建一个新的层。当你最终运行该镜像时，联合文件系统将所有层合并为一个单一镜像，然后作为容器运行。这种分层方法意味着你也可以使用现有镜像作为新镜像的基础。

### Docker Registry

我们所有人都不知道 `GitHub`。`Docker Registry` 可以被认为是 `Docker` 镜像的类似物。虽然不属于你的 `Docker` 安装的一部分，但 `Docker Registry` 与 `Docker` 紧密集成，允许你轻松推送/拉取 `Docker` 镜像。

从 `DevOps` 的角度来看，这提供了大量的连通性。即使团队位于不同的地理位置，他们也更容易共享和分发 `Docker` 镜像。如果你对 `Docker` 本身提供的云托管 `Docker Registry` 感兴趣，请前往 `hub.docker.com`。

### Docker Swarm

为了能够在集群上部署和管理多个 `Docker` 镜像，`Docker` 提供了一种名为 `Docker Swarm` 的工具。开始使用 `Swarm` 的前提条件是：本地系统安装了 `VirtualBox`，所有节点都可以访问 `Docker` 以拉取镜像，并且每个节点都关联了一个发现服务，如 `etcd`、`Consul`、`ZooKeeper` 等。

### 浏览器内终端

`Wetty` (`Web`+`http`) 是一个由 `JavaScript` 驱动的浏览器内终端模拟器。你可以使用 `DockerInBrowser` 的 `Wetty` 在浏览器中运行 `Linux` shell；`Docker` 镜像已经在 `DockerHub` 上可用，所以你只需要输入：

```
$ docker run -p 3000:3000 -d nathanaele/wetty
```

注意，`Wetty` 目前仅在 `Chrome` 浏览器中工作。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_20_0.png)

![](img/0fc17bd4c29dc437e3ac28a53f7559db_20_1.png)

左：如果你需要管理许多 `Docker` 镜像，请充分利用 `Docker Swarm` 工具

## 使用 PUPPET 自动配置节点

`Puppet` 允许你管理 `IT` 基础设施的状态。在这里，我们将看看 `Puppet` 的安装过程，然后是主/代理设置。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_21_0.png)

上：你可以在 `puppetlabs.com` 上了解有关 `Puppet` 状态的更多信息

自动化是实施 `DevOps` 的关键因素之一。你越少在重复任务中投入人力，就能从你的劳动力中获得越多。`IT` 基础设施配置是涉及重复任务的一个领域——配置物理和虚拟机、编排、报告和其他类似任务。以下是配置管理工具提供的一些优势：

- 代码提交日志向你展示了基础设施上变更的完整历史

- 在系统间可复现

- 易于扩展

- 一致且连贯的服务器设置

- 针对开发、测试和生产节点的协调环境

因此，一个能让你处理所有这些及更多内容，而不必让你在编码中脏手头的工具，可以极大地帮助你在 `DevOps` 道路上走得更远。`Puppet` 就是这样的工具。简而言之，`Puppet` 让你管理你的 `IT` 基础设施的状态。在主/代理设置中，主节点是中央 `Puppet` 服务器，所有你的配置数据都将从此进行管理和分发，而你其余的服务器都将是 `Puppet` 代理节点，可以由 `Puppet` 主节点配置。在独立 `Puppet` 中，每个节点定期使用 `puppet apply` 命令使用完整的 `Puppet` 模块和清单来编译和应用程序自己的配置。换句话说，每个节点需要与主/代理 `Puppet` 中的 `Puppet` 主节点所需的相同文件和数据。在本教程中，我们将专注于主/代理 `Puppet` 设置。

### 01 安装前步骤

一旦你决定了设置类型，即主/代理或独立，下一步是识别主节点（如果你计划使用主/代理设置）。注意，`Windows` 机器不能充当主节点。此外，主节点应该是一台专用机器，至少拥有两个处理器核心和 `1GB` 的 `RAM`。它还必须可以通过可靠的主机名访问。你可以通过确保主节点位于 `puppet` 的默认主机名下来减少代理节点上的设置时间。`Puppet` 主节点应允许入站流量使用端口 `8140`，代理节点应能够连接到主节点。`Puppet` 主节点充当证书颁发机构，因此它必须准确设置系统时间，否则它可能会错误地从遥远的过去或未来颁发代理证书，其他节点会将这些视为过期。一旦所有这些都被处理完毕，你就可以继续 `Puppet` 安装的下一步。

### 02 在主节点上安装

是时候在主节点上安装 `Puppet` 了。首先启用 `Puppet Labs` 软件包存储库；一旦启用了此存储库，我们就可以安装 `Puppet`。输入：

```bash
$ wget https://apt.puppetlabs.com/puppet-labs-release-trusty.deb
$ sudo dpkg -i puppet-labs-release-trusty.deb
$ sudo apt-get update
```

接下来，在 `Puppet` 主节点上，输入以下内容之一：

```bash
$ sudo apt-get install puppetmaster-passenger
```

... 这是 `PuppetLabs` 本身推荐的，因为它安装了 `Puppet` 及其先决条件，并自动配置了一个具备生产容量的 `Web` 服务器；或者，输入：

```bash
$ sudo apt-get install puppetmaster
```

... 这将仅安装 `Puppet`、其先决条件以及用于运行测试级 `Puppet` 主节点服务器的 `init` 脚本 `/etc/init.d/puppetmaster`。

### 声明式语言

`Puppet` 使用声明式语言帮助你描述系统的状态。这意味着你不需要考虑通过安装 `Apache`、`MySQL` 和 `PHP` 来构建 `LAMP` 堆栈：然后调整 `php.ini`；然后启用 `mod_php`；等等。你只需描述你想要的状态 – 例如，“一个具有 `Apache`、`MySQL` 和 `WordPress` 的 `Web` 服务器” – 然后让 `Puppet` 使其发生。

### 03 在代理上安装及安装后配置

现在，你需要在所有代理节点上运行以下命令：

```bash
$ sudo apt-get install puppet
```
