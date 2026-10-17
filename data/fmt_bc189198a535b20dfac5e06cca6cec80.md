
# 第 2 步：运行 Docker 容器

要删除之前的容器并基于 Nginx 镜像创建一个新容器，应应用以下命令集：

- `sudo docker ps -a | grep nginx`
- `sudo docker rm -f nginx`
- `sudo docker run -d --name nginx -p 8080:80 nginx`
- `sudo docker ps -a | grep nginx`

## 解释

- `-d`: 以分离模式（后台）运行容器。
- `--name nginx`: 为容器分配自定义名称。
- `-p 8080:80`: 将宿主机上的 `8080` 端口映射到容器内的 `80` 端口。
- `nginx`: 指定使用的镜像。

检查容器是否正在运行：`sudo docker ps`

在浏览器中访问 `http://localhost:8080` 查看 Nginx 欢迎页面。

# 第 3 步：列出和检查容器

- 列出所有运行中的容器：`sudo docker ps`
- 查看运行中和停止的容器：`sudo docker ps -a`
- 获取特定容器的详细信息：`sudo docker inspect mynginx`

# 第 4 步：管理容器

## 重启容器

重启已停止的容器：`sudo docker restart mynginx`

验证运行中的 Docker：`sudo docker ps -a | grep mynginx`

## 停止容器

停止运行中的容器，使用：`sudo docker stop mynginx`

## 移除容器

要移除容器，先停止它（如果正在运行），然后删除它：`sudo docker rm mynginx`

删除所有停止的容器：`sudo docker container prune`

# 第 5 步：运行交互式容器

对于交互式容器，例如基于 Ubuntu 的 shell 会话：

```bash
sudo docker run -it ubuntu
```

此过程取决于互联网连接情况，可能需要几分钟。

## 解释

- `-it`: 以带有终端的交互模式运行。
- `ubuntu`: 指定 Ubuntu 镜像。

使用 `exit` 退出交互会话。现在执行 `exit` 命令：在此时，从 CLI 层次结构中退出当前位置的界面至关重要。

# 第 6 步：管理容器日志

最后，要求在此特定的 CLI 和位置安装 `sudo` 命令：

```bash
apt update && apt install -y sudo
```

下组命令再次用于下载 nginx 镜像并为此服务添加功能：

- `sudo docker pull nginx`
- `sudo docker run -d --name mynginx -p 8080:80 nginx`

Docker 允许监控容器日志，使用：`sudo docker logs mynginx`

实时跟踪日志：`sudo docker logs -f mynginx`

> 注意：要退出 Docker 中的实时日志查看，我们只需按 `Ctrl + C`。这会停止日志跟踪过程，但不会停止容器本身。

本节涵盖了创建、运行、管理容器的必用 Docker 命令和概念。精通这些基础操作对于在容器化环境中部署和管理应用程序至关重要。这些基本命令使用户能够有效地与容器工作，确保应用程序与其依赖项一起打包，以便在不同系统之间实现一致部署。

下一节将关注更高级的主题，包括容器网络和存储。它将解释容器如何相互通信，以及如何有效地管理持久化数据，这些都是构建可扩展和可靠应用程序的关键方面。

理解这些概念是使用 Docker 创建更复杂的生产就绪系统的关键。

## 添加预期命令输出

为了提高清晰度并帮助读者验证命令执行成功，请为关键命令包含预期输出，例如 **docker compose up**、**docker info** 和 **aws ecs describe-clusters**。本节提供了将这些输出集成到第 12 章的步骤。

1. **识别关键命令：** 审查第 12 章，识别预期输出可以增强理解的命令。重点关注：

    - **docker compose up:** 显示多容器应用程序的启动。
    - **docker info:** 显示系统级 Docker 配置。
    - **aws ecs describe-clusters:** 提供 ECS 集群详情。
    - **docker ps:** 列出运行中的容器。
    - **docker logs mynginx:** 显示容器日志。

2. **在测试环境中执行命令：** 在安装了 Docker 的 Rocky Linux 9 上设置。运行每个命令并捕获输出。例如：

```bash
$ sudo compose up -d
[+] Running 2/2
- redis Pulled
- web Pulled
[+] Running 2/2
- redis Running
- web Running
```

列表 1：`docker compose up` 的预期输出

显示在配置好的 Rocky Linux 9 环境中运行 `compose` 命令后的预期输出。此命令初始化并启动 `docker-compose.yml` 定义的所有服务。输出提供了正在创建容器、网络和卷（如果尚不存在）的日志，随后是每个运行服务的状态。此列表帮助用户验证其多容器应用程序是否正确启动以及所有服务是否无错误。

3. **将输出集成到章节：** 在每个命令解释后添加名为“预期输出”的子节。使用代码块显示输出，确保在我们的编写软件中使用 `lstlisting` 环境进行清晰的格式化。

4. **解释输出：** 为输出的含义提供简要描述。例如，对于 `docker compose up`，说明输出确认了 Redis 和 Nginx 容器以分离模式拉取并运行。

5. **验证输出：** 在安装了最新 Docker 版本的 Rocky Linux 9 上测试命令（例如，2025 年 6 月的 Docker 27.3.1），以确保输出反映当前行为。更新章节以指定测试的 Docker 版本。

# 容器网络和存储

容器网络和存储是容器化环境的基础方面，实现了容器之间的有效通信和持久化数据管理。与传统的虚拟化（虚拟机具有专用网络接口和持久化存储）不同，容器依赖轻量级网络解决方案和外部存储系统来实现可移植性和扩展性。

本节探讨了容器网络和存储的核心概念，涵盖了网络模式、存储选项以及优化容器化部署性能与安全性的最佳实践。

# 容器网络

容器网络允许容器之间以及与外部服务之间进行通信。Docker 提供了多种网络选项以适应不同的用场景，包括：

## 桥接网络 (Bridge Network)

桥接网络是 Docker 容器的默认网络模式。它通过内部虚拟网络允许同一宿主机上的容器进行通信，同时除非显式暴露，否则它们将与外部网络隔离。

关键特性：

- 位于同一桥接网络上的容器可以使用容器名称进行通信。
- 默认情况下，不同桥接网络上的容器无法通信。
- 将容器服务暴露到宿主机上需要进行端口映射。

示例：

```
# 创建自定义桥接网络
docker network create my_bridge_network
# 运行连接到网络的容器
docker run -d --name web_container --network my_bridge_network nginx
```

## 主机网络 (Host Network)

主机网络模式允许容器共享宿主机的网络栈。这消除了端口映射的需求，但移除了容器与宿主机之间的网络隔离。

关键特性：

- 直接访问宿主机的网络接口。
- 由于流量不经过 Docker 的虚拟网络，因此降低了延迟。
- 容器无法与宿主机网络隔离。

要验证现有的容器，我们运行下一个命令：`sudo docker ps -a`

## 叠加网络 (Overlay Network)

叠加网络用于多主机 Docker Swarm 部署，允许运行在不同宿主机上的容器之间进行通信。

关键特性：

- 需要 Swarm 集群才能运行。
- 提供内置的服务发现功能。
- 确保节点之间的加密通信。

示例：

```
# 初始化 Docker Swarm 集群
docker swarm init
# 创建叠加网络
docker network create -d overlay my_overlay_network
```

## Macvlan 网络 (Macvlan Network)

Macvlan 通过分配唯一的 MAC 地址，允许容器表现为网络上的物理设备。

关键特性：

- 容器可以直接与外部网络通信。
- 适用于需要二层网络访问权限的遗留应用。
- 每个容器都从外部网络获得自己的 IP 地址。

示例：

```docker
docker network create -d macvlan --subnet=192.168.1.0/24
my_macvlan_network
```
