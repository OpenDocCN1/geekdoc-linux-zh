
# 停止和启动容器

`docker run --restart=always --name wordpressdb -e MYSQL_ROOT_PASSWORD=<PASSWORD> -e MYSQL_DATABASE=wordpress -d mysql:5.7`

2. 接下来，安装并运行官方 WordPress 镜像，将其作为 Docker 容器实例运行，并连接到 MySQL 容器（提供与上一步相同的 `<PASSWORD>` 字符串）：

```
docker run --restart=always -e WORDPRESS_DB_PASSWORD=<password> -d --name wordpress --link wordpressdb:mysql -p 8080:8080 wordpress
```

3. 现在，MySQL 和 WordPress 容器应该已经在运行了。要检查当前运行的容器，输入：

```
docker ps
```

4. 要获取所有 Docker WordPress 容器设置，使用：

```
docker inspect wordpress
```

5. 要检查 WordPress 容器的日志文件，运行以下命令：

```
docker logs -f wordpress
```

6. 在与运行 Docker 守护进程的服务器处于同一网络的计算机上打开浏览器，并输入以下内容：

`http://<服务器IP>:8080/`

## 工作原理...

来自 Docker Hub 的官方 WordPress 镜像不包含自己的 MySQL 服务器。它依赖于外部，因此我们将通过从 Docker Hub 安装并运行一个 MySQL Docker 容器开始本教程。

Docker 镜像是包含了所有文件的集合，它可以运行应用程序并允许访问，它是只读的镜像。如果你想运行这样的镜像，通过克隆镜像来实现。这实际上是一个可运行的镜像。正如我们所见，Docker 镜像可以包含任何应用程序所需的所有文件以及其依赖项，这可以通过运行镜像来实现。Docker 确实是一个真正可扩展的系统，因为在创建你自己的镜像时你就不需要重新造轮子。只需前往 Docker Hub (`https://hub.docker.com/`) 搜索你想运行的软件，然后使用 `docker run` 命令，提供 Docker 镜像名称，你就搞定了。

所以我们从这次经历中学到了什么？

我们开始这段旅程是使用 `docker run` 命令从远程 Docker Hub 下载镜像并将其放入本地镜像存储（`mysql:5.7` 和 `wordpress`），然后运行它们（容器）。要获取机器上下载的所有镜像列表，输入 `docker images`。正如我们所见，两个运行命令都提供了命令行参数，我们需要它来设置一些容器内部可见的必需环境变量。这些包括我们要运行的 MySQL 数据库以及设置和访问它们的 MySQL 密码。在这里我们 Docker 容器之间通信的一个非常重要的功能！通常你可以将不同的 Docker 容器组件堆叠在一起并使系统变得非常容易。另一个参数是 `-p`，用于从我们的主机端口 8080 映射到 http 端口 80，并打开防火墙允许此端口的入站流量。`--restart=always` 有助于让镜像容器重启，因此主机重启时容器会自动重启。之后，我们引入了 `docker inspect` 命令行参数，它打印出名为 `wordpress` 的运行容器以及它们的 `CONTAINER_ID`。这个 ID 是一个唯一的 MD5 哈希值，我们在大多数 Docker 命令行输入中引用特定容器时都会使用它（在本教程中我们通过容器名称引用，这也是可能的）。之后，我们展示了如何使用 `inspect` 参数打印容器的配置。然后，如何以开放流的方式获取 WordPress 容器的日志文件，我们使用了 `log -f` 参数。

注意，如果你在任何时候从 Docker 下载任何容器时遇到连接问题，例如 `dial tcp: lookup index.docker.io: no such host`，请在重试之前重启 Docker 服务。

## 更多...

在本节中，我们将向你如何启动和停止容器，以及如何连接到你的容器。

在主配方中，我们使用了 Docker 的 `run` 命令，它实际上是另外两个 Docker 命令的封装：`create` 和 `start`。正如这些命令的名字所示，`create` 命令从现有镜像创建（克隆）容器，如果本地缓存中不存在镜像，它将从指定的 Docker 注册库（如预定义的 Docker hub）下载；而 `start` 命令则实际上启动它。要列出计算机上所有的容器（运行中或已停止的），请输入 `ps -a`。识别你特定的 `CONTAINER_ID`。然后我们可以通过执行正确的 `CONTAINER_ID` 来启动一个已停止或启动的容器，或者找到并停止一个运行中的容器，例如执行 `docker stop 0b353947d812` 或 `docker stop a2felle26e5145`（`CONTAINER_ID` 的哈希值会在你的计算机上消失）。

有时你需要删除一个容器；如果你想在从镜像重新创建时完全更改其命令行参数。要删除容器，请使用 `rm` 命令（但记住它必须先停止）：`docker stop b7f720fbfd23; docker rm b7f720fbfd23`

## 连接并与容器交互

Linux 容器是运行在服务器上独立环境的隔离进程，没有办法像使用 `ssh` 登录普通服务器那样进入它。如果你需要访问容器的 BASH shell，那么你可以运行 `docker exec` 命令，这对于调试问题或修改你的容器（例如，在容器内安装新软件包或更新程序）特别有用。注意，这只对运行中的容器有效，并且你需要在运行以下命令之前知道你容器的 ID（输入 `docker ps` 来查找）：`docker exec -it CONTAINER_ID /bin/bash`，例如 `docker exec -it d22dd594f0dd /bin/bash`。一旦成功挂载到容器上，你将看到一个略有变化的命令行提示符，以 `CONTAINER_ID` 作为主机名，例如 `root@d22dd594f0d:/var/www/html#`。如果你需要退出容器，输入 `exit`。

## 从 Dockerfile 创建自己的镜像并上传到 Docker Hub

除了镜像和容器，Docker 还有一个一个非常重要的术语叫做 `Dockerfile`。

`Dockerfile` 就像一个为特定应用程序创建环境的配方，这意味着它包含了蓝图以及关于如何构建特定镜像文件的每个描述。例如，如果我们想容器化一个基于 Web 服务器的应用程序，我们将为它定义所有依赖，例如提供系统依赖的基础 Linux 系统（如 Ubuntu、Debian、CentOS 等，这并不意味着我们虚拟化核心操作系统，而只是使用系统依赖），以及 `Dockerfile` 中所有的应用程序、动态库和服务（如 PHP、Apache、MySQL），以及所有的特殊配置选项或环境变量。构建自己的自定义镜像有两种方法。其一，你可以下载一个现有的基础镜像（正如我们在之前的 WordPress 配方中做的那样），并使用 BASH 连接到容器，安装额外的软件，修改你的配置文件，然后将容器作为新镜像提交到注册库。或者，在本配方中，我们将教你如何从用于 Express.js Web 应用程序服务器的新 `Dockerfile` 构建自己的镜像，并将其上传到你自己的 Docker Hub 账户。

### 准备工作

完成此配方，你需要一个具有 root 权限的 CentOS 7 操作系统安装、一个你选择的控制台文本编辑器，以及一个连接以便与 Docker Hub 通信。预计 Docker 已经安装并运行。此外，为了将你的新镜像上传到 Docker Hub，你需要在那里创建一个新的 Docker Hub 用户账户。只需访问 `https://hub.docker.com/` 并在那里免费注册。在我们的示例中，我们将使用虚构的 Docker Hub 用户 ID `johnndoe`。

### 如何操作...

1. 首先，登录 root 并使用你的 Docker Hub 用户 ID 创建一个新的目录结构（将 `johnndoe` 目录名相应地替换为你自己的 ID），并打开一个空的 Dockerfile，在其中放入你镜像的构建蓝图：

```bash
mkdir -p ~/johnndoe/centos7-express

cd $ && vi Dockerfile
```

2. 将以下内容放入该文件：

```bash
FROM centros:7

RUN yum install -y epel-release;yum install -y npm;

RUN npm install express --save
```

# 操作系统 - 虚拟化

```bash
COPY ./src

EXPOSE 8080

CMD ["node", "/src/index.js"]
```
