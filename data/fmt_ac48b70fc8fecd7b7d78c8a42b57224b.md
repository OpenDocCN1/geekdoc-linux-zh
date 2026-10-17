
Ubuntu v16.04 封装了预构建的 Docker debian 软件包，因此默认包含了 `contain` 和 `runC`。在宿主机系统上部署引擎的方式上略有变化。第一步是使用示例 8-1 显示的命令更新本地 apt 索引。

### 示例 8-1 更新 Ubuntu 软件包

```
blockchain@itschain:$ sudo apt-get
Hit:1 http://us.ports.ubuntu/ubuntu-ports-xenial InRelease
Hit:2 http://us.ports.ubuntu/ubuntu-ports-xenial-updates InRelease
Hit:3 http://us.ports.ubuntu/ubuntu-ports-xenial-backports InRelease
Hit:4 http://us.ports.ubuntu/ubuntu-ports-xenial-security InRelease
Reading lists... Done
blockchain@itschain:$
```

使用以下方案之一向宿主机系统部署 Docker 软件包：

- 从官方 Docker 引擎仓库部署软件包
- 从预包的 Ubuntu 发行版部署 Docker 引擎

示例 8-2 展示了使用第二种方案部署 Docker。Ubuntu 16.04 LTS 为 LinuxONE 预构建了名为 `docker.io` 和 `docker.registry` 的软件包。这种方法的优势是它们在发行版中经过了集成和测试。然而，Docker 引擎可能是旧版本，或者不是最新版本。

### 示例 8-2 安装 Docker 软件包

```
blockchain@itschain:$ sudo apt-get -y install docker.io docker-registry
Reading packages... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
bridge-utils cgroups-mount contained dns-root-data dnsmasq-base git-man-liberror-perl
netfilter-containerpack3 runc-ubuntu xz-utils
Suggested packages:
mountall all-tools btrfs-tools bootstrap linux rnfse-fuse |
zfutis-git-daemon-run |
git-daemon-systemd git-docker doc-git-extra git-git gitkit
```

The NEW packages will be installed:

bridge-utils cgroups-mount contained dns-root-data dnsmasq-base docker-registry.io

git git-man liberror-perl netfilter-containerpack3 runc-ubuntu

0 已升级，15 新安装，0 要移除，0 未升级。
需要下载 20.4 MB 的归档。134
执行此操作后，将使用 134 MB 的额外磁盘空间。

```
Processing triggers for systemd (229-4ubuntu0) ...

Processing triggers for rereadada (0.100.0-19) ...

Processing triggers for libc-bin (2.23-ubuntu3) ...

Processing triggers for dbus (1.10.6-1ubuntu3) ...

blockchain@itostchain:$
```

Docker 守护进程绑定到 UNIX 套接字而不是 TCP 端口，因此 Docker 守护进程始终以 root 身份运行。为了避免在执行 `docker` 命令时需要使用 `sudo`，请如示例 8-3 所示将用户添加到 `docker` 组。

### 示例 8-3 将用户添加到 docker 组

```
blockchain@itostchain:$ sudo usermod -ag docker blockchain
```

注销并重新登录该用户，以使用户权限生效。然后，你可以如示例 8-4 所示验证 `docker` 命令。

### 示例 8-4 验证 docker 版本

```
blockchain@itostchain:$ docker --version

Docker version 1.11.2, build b9f10c9

blockchain@itostchain:$
```

验证完成后，访问 `dockerhub` 中的预构建 `docker` 镜像部分，并如示例 8-5 所示运行一个测试 `hello-world` 容器。

### 示例 8-5 运行 docker 容器

```
blockchain@itostchain:$ docker pull s390x/hello-world

Using default tag: latest

latest: Pulling from s390x/hello-world

9efa39566ce: Pull complete

digest: sha256:ec5a634fc76db7d16296a133ec332fa3a85351cb30b50cc59f59f8b5051f83c58

Status: Downloaded image for s390x/hello-world
```

| REPOSITORY | TAG | CREATED | SIZE |
|---|---|---|---|
| s390x/hello-world | latest | 0490c0ea2cf | 3 months ago | 1.984 kB |

```
blockchain@itostchain:$ docker run 0490c0ea2cf
```

Hello from Docker on docker!
此消息显示你的安装似乎运行正常。

你已成功部署了 `docker`。

140 从 x86 到 LinuxONE 的实战迁移

## 8.3 在 IBM LinuxONE 上部署 MongoDB

MongoDB 是一个开源数据库，被认为是最流行且增长最快的 NoSQL 数据库。这很大程度上是因为它在传统 SQL 数据库遇到困难的领域表现良好。它非常适合处理大型非结构化数据集，并且对存储的数据具有极快的读取速度。尽管它不是所有存储结构化应用程序的替代品，但它为海量非结构化数据和移动流量提供了现代解决方案。

凭借 LinuxONE 的性能和虚拟化能力，使其成为扩展和使用基于 MongoDB 的 NoSQL 工作负载的理想平台。本节将介绍在 LinuxONE 上部署 MongoDB（Docker 容器）的步骤。

### 8.3.1 工作环境

本示例使用 Ubuntu 16.04 LTS 作为 MongoDB 部署的宿主机。由于我们决定将 MongoDB 安装为 Docker 容器，第一步是在宿主机系统上设置 Docker。有关部署 Docker 的深度文档，请参阅《The Virtualization Cookbook for Systems Volume 4: Ubuntu Server 16.04, SG24-8354》。

> **重要：Ubuntu 16.04 官方仓库提供的 Docker 安装包可能不是最新版本。要获取最新版本，请从 Docker 官方仓库安装 Docker。**

配置 Docker 后，在主机操作系统上启用并运行其服务。
示例 8-6 显示了验证 Docker 配置。

### 图 8-6：验证 Docker

```
itsoadmin@lnxmongo:$ docker version

Version: 1.12.1

API version: 1.24

Go version: go1.6.3

Git commit: 23cf638

Built: Mon, 19 Sep 2016 20:34:59 +1200

OS/Arch: linux/s390xServer:

Version: 1.12.1

API version: 1.24

Go version: go1.6.3

Git commit: 23cf638

Built: Mon, 19 Sep 2016 20:34:59 +1200

itsoadmin@lnxmongo:$
```

```
itsoadmin@lnxmongo:$ docker images

| REPOSITORY | TAG | IMAGE ID | CREATED | SIZE |

|---|---|---|---|---|

itsoadmin@lnxmongo:$
```
