

# 教程

## 原材料

在这里，我们专注于在集群上部署 Web 服务，但树莓派的设置包含了可扩展规模的硬件。树莓派拥有 28 个 GPIO 引脚、一个 USB 端口和一个摄像头接口。你拥有了制作某些独特之处的原材料。你表达了一个表达式，比如 4。你尝试尝试在它处理请求时点亮一个 LED 灯吗？

## 08 在 Docker 上构建 Docker！

现在我们有了可以运行的版本，需要对其进行编译：

- cd /docker-arm/images/docker-arm
- ./build.sh

在接下来的 30-60 分钟内，代码将为 ARM 构建并打补丁，设置你的树莓派，并复制到树莓派的本地文件夹。脚本将一直运行直到你收到如下消息：

`Created binary: bundles/1.9.1/binary/docker-1.9.1-arm-linux-armv7*`

如果输出成功，你就可以继续安装更改：

- cd /docker-arm/images/docker-arm
- sudo install.sh
- sudo systemctl start docker

## 09 构建 Docker Swarm

公共仓库中有一个 Swarm 镜像，但我们无法使用它因为它它是为 x86_64 架构（普通 PC）构建的。所以让我们构建自己的吧：

- cd /docker-arm/images/docker-arm
- ./build.sh
- docker run alexelsis2-swarm --version

## 10 额外节点

此时，你可以复制 SD 卡，也可以在每个树莓派上运行指令。使用这种方法，我们需要更新所有树莓派上的 /etc/hostname 和 IP 地址。如果复制卡片，请确保使用 /docker

![](img/f4a034c4fbc20906a013558fa4e058a2_73_0.png)

## 11 我们将第一个节点专门用于管理集群

端口 4000 用于 swarm，并在 8500 通过 Consul 处理服务发现。两者将运行在本地 Docker 实例上。

注册表中还有其他镜像 - 你可以根据需要构建它们，也可以使用 `build_all.sh` 脚本（推荐）。这可能需要一些时间。

- cd /docker-arm/images/console-arm
- ./build.sh

- ./script/start_consul.sh
- ./manage_swarm.sh

如果你构建了 swarm-container，你会发现这次快得多，因为 Docker 缓存了步骤，所以只有节点之间的更改需要重新构建。

![](img/f4a034c4fbc20906a013558fa4e058a2_73_1.png)

# 构建、传输、运行

面向开发者和系统管理员的分布式应用程序开放平台

开始使用 Docker

## 通过 AWS 部署 Docker

在 AWS 上运行 Docker 提供了一种高可靠、低成本的方法，用于质量构建、传输和运行各种规模的分布式应用：使用 AWS 市场中的 AMI 部署 Docker。

立即开始使用 Docker 和 AWS »

## 通用控制平面的 Beta 访问

Docker 可以运行任何应用，通用控制平面为你的 Docker 应用提供非本地化的管理解决方案，无论它们运行在何处。

立即注册 Beta 访问

Docker 正在快速成为内容技术的行业标准

加入集群

连接到其中一个节点，例如 192.168.0.201，并启动 `auto_join-swarm.sh` 脚本。这将查询 eth0 的 IP 地址并广播连接到 swarm 管理器。

启动等数量的节点：集群，并将它们链接到 redis 容器。

```bash
# /docker-arm/script/auto_join_swarm.sh
```

你将在 `docker ps` 下看到运行的 swarm。如果想查看输出，检查 `docker logs`。在每个节点上重复此步骤。

```bash
# docker run -p 6379:6379 -d \
--name redis \
--link redis:1 \
alexis. redis
```

在 balancer 节点上最终运行：

![](img/f4a034c4fbc20906a013558fa4e058a2_73_0.png)

```bash
# DOCKER_HOST=tcp:// docker run -d --name=balancer -p 80:80 nginx
```

## 查询 swarm

登录主节点并通过 swarm-arm 镜像查询 console 的地址：

![](img/f4a034c4fbc20906a013558fa4e058a2_73_1.png)

```bash
# docker run alexellisiz/swarm-arm console://192.168.0:2500/
```

 Apache Bench

使用 10 个并发线程和共 1000 次请求启动 Apache Bench。在设置额外的树莓派后，我们开始操作。为了将 Web 服务从一个容器扩展到多个，请使用 `docker` 命令，并将 `DOCKER_HOST` 变量设置为你的 swarm 管理器地址：

```bash
# ab -n 1000 -c 10 http://192.168.0:2500/
```

并发级别：10
测试耗时：2.5 秒
每秒请求数：38（平均）

在单个树莓派上重复实验是每秒 80 次请求，共 12 秒。你也可以尝试将 `-c` 值增加到 100。

![](img/f4a034c4fbc20906a013558fa4e058a2_73_2.png)

```bash
# export DOCKER_HOST=tcp://192.168.0:2000
```

现在查看我们有多少资源：

```bash
# docker info
```
节点：4
CPU：20
总内存：7 GB

# 示例：分布式 Web 应用程序

我们现在设置一个分布式数据库环境。我们将运行多个实例并使用 nginx 负载均衡来处理流量。然后可以使用 Apache Bench 进行测试。

## 将流量直连你的 swarm

如果你在其中一个上拉取 docker，可以使用 `DOCKER_HOST` 变量指向任何节点而无需登录树莓派。swarm 创建并将 Web 服务从一个容器扩展到多个。这些容器需要按顺序启动，从 Redis 开始，最后是 nginx。

```bash
# DOCKER_HOST=tcp://192.168.0:2000
# docker run -p 6379:6379 -d --name=redis-1 alexellisiz/redis-arm
# wget get.docker.com/builds/arm/v7 -O docker-compose
# docker-compose --version
```

Docker Compose 是一个允许你定义多个容器的工具，让你无需手动即可将 Web 服务从一个扩展到多个。

```yaml
node:
  image: redis
  ports:
    - "3000"
nginx:
  image: nginx
  ports:
    - "80"
```

# 教程

## 创建 Minecraft 游戏

使用你的树莓派和 Python 知识在 Minecraft 中编写一个简单的迷你游戏。Pi 镜像已预装了 Minecraft 和 Python。如果你使用的是旧版本，建议下载并更新到新的 Raspberry 镜像。

## 更新和安装

更新你的树莓派，打开终端并输入：

```bash
sudo apt-get update
sudo apt-get upgrade
```

# 导入模块

加载你喜欢的编辑器并启动新窗口。你需要导入以下模块：**random** 用于创建和生成位置，**time** 用于向程序添加暂停和延迟。接下来，添加几行代码：`from mc import minecraft` 和 `mc = minecraft.Minecraft()`。这些创建了 Minecraft 和 Python 之间的链接。这使你能够写入“创建了 Minecraft”。

```python
import random
import time
from mc import minecraft
mc = minecraft.Minecraft()
```

# 种花

下面的程序将向展示它是如何工作的。每个区块都有自己的 ID 数字，共有数百个。x, y, z = mc.getPos() 获取玩家在世界中的位置并以元组形式返回。现在你知道自己在世界的什么位置，可以使用 `mc.setBlock(x, y, flower)` 放置区块。

```python
flower = 38
while True:
    x, y, z = mc.getPos()
    mc.setBlock(x, y, flower)
    time.sleep(1)
```

# 运行代码

减小 Minecraft 窗口的大小更容易看到代码和运行中的程序；在它们之间切换可能会很麻烦。Tab 键可以隐藏 MC 窗口的键盘和鼠标。运行 Python 程序并等待加载——随着你的走动，花朵出现了！更改第一行的 ID 来更改区块类型，而不是花，尝试种植金、水或火光。

![](img/f4a034c4fbc20906a013558fa4e058a2_73_0.png)

# 向 Minecraft 世界发布消息

也可以向世界发布消息，这在游戏后期用于告知玩家分数和当前分数。在你的进度中，在代码行 `flower = 38` 添加以下内容，将其变为 `mc.postChat("I grew some flowers with code")`。现在看到消息弹出。你可以更改消息，移动到下一步开始游戏。

# 创建地板

游戏在玩家当前所在的地板上进行，因此在运行程序之前建议飞到空中寻找平坦的地形。要创建地板，你需要编写一个循环并在世界中使用 `x, y, z = mc.getPos()` 运行程序。使用 `mc.setBlock` 代码放置构成地板的区块。

