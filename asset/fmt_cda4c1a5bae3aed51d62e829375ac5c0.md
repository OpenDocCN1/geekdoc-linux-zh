
```
curl -sSL https://get.docker.io/ubuntu/
```

一旦你确信它不会安装最新的 NSA 后门或窃取比特币的外国恶意软件，你就可以让它运行：

```
curl -sSL https://get.docker.io/ubuntu/ | sudo sh
```

这将安装一些软件包并启动一个 `docker` `daemon` 进程，你可以通过 `ps` 命令确认其正在运行。其他发行版的说明可以在官方网站上找到（http://bit.ly/DockerInstalls）。现在让我们用传统的‘Hello, World!’直接上手，以确认一切按预期工作！

```
sudo docker run ubuntu /bin/echo "Hello, World!"
```

你会看到一条消息说本地找不到 Ubuntu 镜像，并且会下载一个镜像（通过 Docker Hub）以及一些更新。值得庆幸的是，一旦镜像下载完成，它会保留在缓存中，后续运行会快得多。一旦一切准备就绪，神奇的文字就会出现。但这里发生了什么？`docker run` 命令正如你所期望的那样工作：它运行一个容器。我们要求使用 Ubuntu 镜像来创建容器，当 Docker 找不到本地副本时，它会从其 hub 拉取。最后，我们要求在其中运行简单的 `echo` 命令。一旦 Docker 完成任务，容器就会关闭。我们可以通过使用 `-i` 和 `-t` 标志以更交互的方式使用此下载的镜像，这使我们能够使用容器的 STDIN 并获得终端连接。

```
sudo docker run -i -t ubuntu /bin/bash
```

这应该几乎立即在容器本身内提供一个 `root` 提示。希望它出现的速度是 Docker 受欢迎的原因之一。容器非常快速且轻量。许多容器可以在一个系统上共存，比如果它们更像传统的重量级虚拟机，则无法处理的容器要多得多。这部分是由于 Docker 使用联合文件系统，这些文件系统通过创建层来操作。这使它们极其快速。正如你所期望的，Linux 带有不止一个变体。Docker 默认使用 `devicemapper`，但也支持 `AUFS`、`btrfs` 和 `vfs`。

从该提示符运行几个命令，例如 `df -h`、`ls` 和最后 `top`。虽然前两个的输出看起来相当普通，但 `top` 将显示一个相当奇怪的情况：只有两个正在运行的进程：`bash` 和 `top` 命令本身。通过按 `q` 退出这种奇怪的矩阵式情况（退出

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_114_0.png)

Docker 网站 – 这里没有苍白的鲸鱼 – 并包含一个实时在线教程，大约 10 分钟内讲解基础知识。

## Hypervisors vs Containers – 有什么区别？

如今，系统管理员在被要求设计新基础设施时，有大量可供考虑的选项。任何人都可以原谅在虚拟化迷宫中迷路。所以超visor 和基于容器的系统到底有什么区别？超visor 源于 1960 年代的 IBM 系统，通过让主机系统在多个客户系统（或虚拟机）之间共享硬件资源来工作。超visor 管理客户操作系统的执行，并向它们呈现底层资源的虚拟化表示。有几种不同的类型：

- Type 1 hypervisors 这些是在任何客户系统之前安装的，并直接与底层硬件一起工作（VMware 就是这种方法的例子）。
- Type 2 hypervisors 在传统操作系统之上运行，客户位于其上方的另一个层级（这就是 Virtualbox 的工作原理）。

容器 however，通过让操作系统的内核在‘用户空间’（即内核之外）中运行隔离的进程来工作。这可以只是一个单一应用程序，因此不需要完整操作系统的开销（然后需要维护、修补等）。容器还有一个好处是它们非常轻量。事实上，许多容器可以在同一硬件上运行，但不能运行‘其他’操作系统（例如 Windows），因此被认为不如超visor 本质上安全。

通常情况下，选择最适合特定情况或环境的虚拟化技术。应考虑成本、现有系统、管理工具和技能集等问题。然而这两种方法并不相互排斥，实际上可以互补 – 许多 Docker 采用者承认在基于超visor 的客户机中运行它。虚拟化是一个活跃的开发领域，开源处于前沿。

### Quick tip

`LXC`（Linux Containers）既可以指内核的底层功能（`cgroups` 等），也可以指维护用户空间工具的项目 – 值得一看，已达到 1.0 版本。

更多网络 借助 Zabbix 跟踪一切，见 p118。

## 网络

首先，如果你还没退出的话，输入 `exit` 即可退出；Docker 随后会关闭我们的容器。你可以通过运行 `sudo docker ps` 来确认这一过程，此时只会显示一些表头，没有任何运行中的容器。当然，Docker 也可以处理守护进程，它们不会在我们操作完成后立即退出，所以让我们启动一个试试：`sudo docker run -d ubuntu /bin/bash -c "echo 'yawn'; sleep 60"`

这次我们使用 `-d` 标志启动容器并将其置于后台运行，Docker 会返回一个容器 ID。我们的简单命令行在容器中运行，并进入休眠状态。现在我们可以看到 `sudo docker ps` 提供了更多信息，包括 Docker 为容器分配的一个相当有趣的名字（在我们的测试中是“pensive_franklin”）。我们可以使用这个名字来查看容器正在做什么：`sudo docker logs pensive_franklin`，它应该返回一个略显沉闷的哈欠，来自我们那个短暂运行中的进程。当 `sleep` 命令的 60 秒结束后，Docker 再次挥下斧头，容器就此消失。如果我们为 `sleep` 命令设置更大的值，又等得不耐烦，可以通过以下方式使用 `docker stop` 命令：`sudo docker stop pensive_franklin`

我们可以再尝试几次 `docker run` 命令，试验不同的命令行。当我们玩够了这些把戏后，运行 `sudo docker ps -a` 可以查看所有容器，包括未运行的容器。这里还有很多其他标志可用，我们建议查看 `man docker-ps`。

### 一个更有用的示例

这一切固然不错，但有没有更有用的场景呢？一个非常适合容器的轻量级应用典范就是 Nginx [参见第 76 页]——高性能的 Web/缓存/负载均衡/代理服务器。我们能否轻松地搭建一个全新的 Nginx 实例，并让它随时准备提供网页服务呢？让我们来看看！

快速浏览一下 Docker Hub (https://registry.hub.docker.com)，可以看到 Nginx 在首页上拥有官方仓库。我们可以使用 `pull` 参数将其拉取到本地机器：`sudo docker pull nginx`

过一会儿（有相当大小的层需要下载），我们的镜像就准备好了。我们可以通过在命令提示符下运行 `sudo docker images` 来查看本地已有的镜像。现在，我们可以通过运行以下命令快速验证 Nginx 是否正常工作：`sudo docker run -d -p 8080:80 nginx` `sudo docker ps`

假设 Nginx 显示为运行状态，我们可以将桌面浏览器连接到 http://127.0.0.1:8080 查看默认的 Nginx 页面。一切顺利。但我们如何向其中添加内容呢？首先，让我们通过 `sudo docker stop <那个有趣的名字>` 命令停止正在运行的容器，然后创建一个非常基本的示例文件。打开你喜欢的文本编辑器，创建以下内容，并保存为 `docker-example.html`。最好在一个新的子目录中操作——名称随意——以免其他文件干扰 Docker。然后将该文件保存在新目录下的一个子目录中，并将那个子目录命名为 `content`。

```html
<html>
<head>
<title>Here is our dockerized web site!</title>
</head>
<body>
<h1>We are running in a container</h1>
</body>
</html>
```

Docker Hub 包含了来自常见发行版的许多预定义 Linux 容器。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_115_0.png)

### 你的 Docker 镜像是否损坏？

开源和 Linux 最大的优点之一就是众说纷纭的思想和观点，尤其是在正确运行系统的方法上。其中一例在 Docker 世界中引起了小小的波澜：Phusion——知名产品/项目 Phusion Passenger（广泛用于 Ruby on Rails 和其他 Web 开发环境）的团队——发布了它的 Docker 镜像（可在 Docker Hub 上的 `phusion/baseimage` 获取）。他们认为，Docker 常见的运行单一应用程序进程的做法（正如本教程中 `top` 输出所示）意味着许多重要的系统服务不会在容器中运行，尤其是 `init` 进程会缺失。
