
```
n@lakh:nithish-VirtualBox:~ $ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from hello-world
51125ac580d: Pull complete
5f70cb1826b2: Already exists
hello-world:latest: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.
Digest: sha256:af506d50c957eeccd1f99f08778679686f3284c76a3886158182bed336df4ccb3721eae52
Status: Downloaded newer image for hello-world:latest
Hello from Docker.
This message shows that your installation appears to be working correctly.
To generate this message, Docker took the following steps:
1. The Docker client contacted the Docker daemon.
2. The Docker daemon pulled the 'hello-world' image from the Docker Hub.
3. The Docker daemon created a new container from that image which runs the executable that produces the output you are currently reading.
4. The Docker daemon streamed that output to the Docker client, which sent it to your terminal.
To try something more ambitious, you can run an Ubuntu container with:
  $ docker run -it ubuntu bash
Share images, automate workflows, and more with a free Docker Hub account:  https://hub.docker.com
For more examples and ideas, visit: https://docs.docker.com/useguide/
n@lakh:nithish-VirtualBox:~ $
```

右侧可以使用命令 `docker run <image-name>` 创建一个 Docker 容器

![](img/e7f197876caa0b235fb5da2d16a578ea_44_0.png)

Docker 镜像是预定义格式的可读模板，Docker 守护进程可以运行它——因此，任何你想作为 Docker 容器运行的应用程序，首先需要制作成 Docker 镜像。镜像通常包含基础操作系统、运行应用程序所需的库和二进制文件，以及应用程序本身。Docker 提供了构建新镜像或更新旧镜像的简单方法。你还可以通过 Docker 注册表下载其他人构建的镜像。

Docker 注册表是一种存储和内容交付系统，用于保存 Docker 镜像。你可以使用 `push` 和 `pull` 命令与注册表交互。根据你的需求，注册表可以是私有的或公共的。Docker 还提供官方的 Docker 注册表，作为一个 SaaS（软件即服务）平台，称为 Docker Hub。Docker Hub 可以被视为一个巨大的 Docker 镜像仓库，其中的镜像可免费 downloading 和运行。你也可以创建自己的镜像并将其推送到 Docker Hub。

## 03 Docker 容器

容器可能是 Docker 生态系统中最重要组件，可以将其视为 Docker 镜像的运行实例。镜像（即将作为容器运行）告知 Docker 容器包含什么、启动容器时运行什么进程以及各种其他配置数据。如前一步所述，镜像是只读的，但当镜像被执行（即转换为容器）时，Docker 会在镜像之上创建一个读写层，以便应用程序能正常运行。稍后，当容器停止时，顶部的读写层会丢失，镜像恢复原状。

> “容器隔离了你需要运行的应用程序的运行时环境，但所有容器都使用同一个内核”

Docker 提供了诸如 `run`、`start`、`stop`、`ps`、`rm` 等命令，以便与容器交互。你可以输入 `docker <command-name> --help` 来获取与 `<command-name>` 相关的帮助信息。

现在，你已经对 Docker 的重要组件及其协作方式有了清晰的了解，让我们安装 Docker 并观察这些组件的实际运行。请注意，我使用 Ubuntu 14.04 作为安装和演示的基础系统。

## 04 安装

Docker 的安装相当直接。首先，登录系统并使用 `which` 命令检查是否安装了 `wget`。如果未安装，运行命令 `sudo apt-get update` 和 `sudo apt-get install wget`。成功安装 `wget` 后，让我们安装 Docker。运行命令 `wget -qO- https://get.docker.com/ | sh`。系统会提示输入 root 密码，然后下载并安装 Docker 及其依赖项。要验证 Docker 是否成功安装，你可以运行命令 `sudo docker run hello-world`。这将下载一个测试镜像并在你的系统上的容器中运行它。如果你仔细查看上一页面的输出，你会看到 Docker 生成该消息所遵循的步骤。这有助于了解 Docker 中组件之间是如何交互的。

## Docker Swarm

Docker Swarm 允许你为 Docker 创建原生集群——你可以创建一个 Docker 主机池。并且由于 Docker Swarm 支持标准的 Docker API，任何已经与 Docker 守护进程通信的工具都可以使用 Swarm 透明地扩展到多个主机。

虽然 Docker Swarm 目前仍处于早期阶段，预计其处理方式将会发生变化。

![](img/e7f197876caa0b235fb5da2d16a578ea_45_0.png)

![](img/e7f197876caa0b235fb5da2d16a578ea_45_1.png)

## 05 创建 Docker 组

Docker 安装成功，并且我们已经使用 `docker run` 命令进行了验证，然而，你可能注意到我们在运行任何 Docker 命令前都需要添加 `sudo`，因此每次在新终端中运行 Docker 命令时，都需要输入 root 密码。这是因为 Docker 守护进程绑定到 Unix 套接字而非 TCP 端口，且 root 用户拥有该 Unix 套接字。为了避免使用 `sudo`，你可以创建一个名为 docker 的组并将用户加入其中；这里的“用户”指那些需要运行 Docker 命令的用户。现在，当 Docker 守护进程启动时，它将 Unix 套接字的读/写权限设置为 docker 组中的所有用户。

要创建组并添加用户，请以需要运行 Docker 命令的用户身份登录 Ubuntu。然后运行命令 `sudo usermod -aG docker username`——别忘了将 `username` 替换为实际用户名。然后注销系统并重新登录。通过输入 `docker run hello-world` 来验证 Docker 命令是否现在无需 `sudo` 即可工作。如果成功，我们添加的组机制即可正常工作。现在，每次想要运行 Docker 命令时都不需要输入密码了。

## 06 基础镜像

正如所讨论的，Docker 容器是使用镜像创建的。镜像可以是基础镜像，除了操作系统基础外没有其他内容；也可以是由复杂的预构建应用程序堆栈组成，随时准备启动。这一切都是得益于 Docker 对镜像的层叠方法。这为构建应用程序容器提供了极其强大的抽象，其中一个步骤作为下一个步骤的基础，即新的工具、应用程序、内容、补丁等，在基础（基础镜像）之上形成额外的层。

基础镜像是没有下层任何其他层的那个；这是 Docker 镜像最基本的形式，仅包含操作系统。Docker Hub 拥有所有主要 Linux 发行版的基础镜像，但你也可以自由创建自己的基础镜像。为此，你可以在 Docker Hub 中使用 `scratch` 仓库，只需在 `Dockerfile` 中使用 `FROM scratch`（下一部分将详细介绍 `Dockerfile`）。另一种方法是使用 `tar` 命令。输入：
