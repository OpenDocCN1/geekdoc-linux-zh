
`master@ubuntu-server:~$ kvm -m 1024 -cdrom ubuntu-16.04-desktop-amd64.iso -boot d disk.img`

指定的 `kvm` 选项：

- `-m` 指定分配给虚拟机的内存量。在本例中我们指定了 `1024`。
- `-cdrom` 指定虚拟 CD-ROM 设备。在本例中我们指向了之前下载的 ISO 镜像。
- `-boot` 指定启动设备。在本例中 `d` 代表 CD-ROM。其他选项有软盘 (`a`)、硬盘 (`c`) 和网络 (`n`)。
- `disk.img` 指定原始磁盘镜像。

> 提示 由于某些安装程序的图形启动界面存在问题，你可能需要在启动安装操作系统的 `kv` 命令中添加 `-no-kvm` 参数。

- 8. 新配置的虚拟机应该立即在 QEMU 窗口中启动。虚拟机将尝试从 `-cdrom` 指定的 ISO 镜像启动。打开一个类似的窗口。
- 9. 从这里开始，你可以像在普通机器上安装一样继续安装（第 2 章）。示例中使用的特定 Ubuntu 版本是 Live Desktop。其他方面，这意味着你可以尝试并使用操作系统，而无需实际向磁盘安装任何内容。
- 10. 一旦操作系统安装到虚拟机中，你可以通过 `yangyang@ubuntu-server:/vms$ kvm -m 1024 disk.img` 启动虚拟机。

# 容器

容器指的是一类准虚拟化技术，它们利用各种机制为应用程序（甚至整个操作系统）提供隔离的运行时。容器背后的理念是仅提供应用程序或软件栈运行所需的最小且最具可移植性的资源集。在本章之前讨论的虚拟化解决方案（如 `KVM`、`VMware` 等）旨在虚拟化计算基础设施的几乎每个方面，包括硬件、操作系统等。

正如前面提到的，容器化的基本前提在 UNIX 世界中已经存在了一段时间；如今的新颖之处在于围绕该概念的实现方式和辅助工具。旧和当前的实现方式示例包括 `sprout`、`LXE`、`libvirt LXC`、`systemd-spawn`、`Solaris Zones`、`FreeBSD Jails` 以及 `Docker`。

在这些实现中，`Docker` 是目前获得大量关注和动力的实现方式之一。因此，`Docker` 将是我们本节中容器实施的重点。

## 容器 vs 虚拟机

尽管容器和虚拟机在功能、定义和用例上似乎有重叠，但它们是完全不同的。下表总结了它们的一些相似与不同：

| 虚拟机 (VMs) | 容器 (Containers) |
| :--- | :--- |
| 包含整个操作系统。 | 不需要包含整个操作系统。 |
| 与宿主机无关。宿主机操作系统可以与虚拟机完全不同。例如，你可以在 Linux 宿主机内部运行 Windows、OS X 和 Linux 虚拟机。 | 宿主机操作系统和应用程序容器必须运行相似的操作系统（如对应）。例如，你可以在基于 Red Hat 的宿主机系统内运行基于 Debian 的容器。 |
| 节点资源占用和需求较高。 | 节点资源占用和需求极低。 |
| 开箱即用的安全性更高。 | 开箱即用的安全性可能较低，部分原因是由于第三方镜像可以轻松获取。 |
| 每个虚拟机通常需要自己的内核。需要虚拟化层 (`hypervisor`)。 | 依赖宿主机系统的内核。不需要虚拟化层。 |
| 创建和启动速度较慢。 | 创建和启动速度更快。 |

## Docker

`Docker` 是一组工具和接口，用于以容器的形式开发、管理、交付和运行应用程序。`Docker` 可以利用各种机制访问 Linux 内核的虚拟化内部/接口，主要的机制是 `libcontainer` 库。具体来说，它利用 Linux 内核暴露的命名空间（`namespace`）和控制组（`cgroups`）接口来提供其隔离和资源共享优势。

一些术语和概念在 `Docker` 世界中是独特且常用的。在这里，我们概述了：

- `Docker` 镜像形成了 `Docker` 生态系统的构建模块。它们是创建容器的只读蓝图。当 `Docker` 从镜像运行容器时，它会在镜像上层添加一个读写层。
- `Docker` 容器是从 `Docker` 镜像创建的用于运行应用程序的实际工作负载。
- `Registry`（仓库）是指任何存储 `Docker` 镜像的仓库或源。默认/主仓库是一个名为 `Docker Hub` 的公共仓库，它包含了由各种开源项目、社区和个人贡献的数千个镜像。可以通过网页界面 (`https://hub.docker.com`) 或各种客户端工具访问仓库。
- `Docker Host`（`Docker` 主机）是安装 `Docker` 应用程序的系统。
- `Docker daemon`（守护进程）守护进程负责管理运行在 `Docker Host` 上的容器。它接收来自 `Docker` 客户端的命令。
- `client`（客户端）由用户态工具和应用程序组成，向守护进程发出命令以执行容器相关的管理任务。
- `file`（文件）这是一个配置文件，描述了组装镜像所需的步骤。

## Docker 的安装与启动

在我们的示例 Fedora 服务器上，我们将通过以下步骤演示安装 `Docker`、启动守护进程服务并启用其未来的自动启动：

- 1. 以 root 身份登录时，使用 `dnf` 运行命令安装 `Docker`
```bash
[root@fedora-server ~]# dnf -y install docker
```

- 2. 软件安装成功后，使用 `systemctl` 检查 `docker` 服务的状态：
```bash
[root@fedora-server ~]# systemctl is-enabled docker
```

- 3. 如果输出显示服务被禁用自动启动，你可以通过运行命令启用它：
```bash
[root@fedora-server ~]# systemctl enable docker
```

- 4. 接下来，启动 `docker` 守护进程服务：
```bash
[root@fedora-server ~]# systemctl start docker
```

如果 `docker` 守护进程在采用 Btrfs 文件系统且 SELinux 处于强制模式的 Red Hat 类发行版上无法启动，你可以尝试通过删除 `/etc/sysconfig/docker` 文件中 `OPTIONS` 行的 `selinux-enabled` 来绕过此问题。保存更改后重新启动 `docker`。

## 使用 Docker 镜像

`Docker` 镜像是构成容器的“比特区块”。你将在官方 `Docker` 公共仓库中找到由各种项目、组织和个人创建的数千个镜像。仓库存储了用于各种用途的镜像，范围从娱乐/多媒体用途、开发以及各种网络服务器（HTTP、DNS、VoIP、数据库等），一直到封装在容器中的完整操作系统。

我们将演示如何使用官方 Apache HTTP 项目 (`http://httpd.apache.org/`) 创建的镜像来设置容器：

- 1. 查询本地 `Docker Host` 上的任何已存在镜像：
```bash
[root@fedora-server ~]# docker images
```
在新的 `Docker Host`/安装上，列表应该是空的。

- 2. 在公共仓库中搜索名称中包含 `httpd` 关键字的镜像：
```bash
[root@fedora-server ~]# docker search httpd
```
输出应显示各种可用镜像。`NAME`（名称）和 `OFFICIAL`（官方）列提供了关于镜像是由官方项目维护者还是个人上传的提示。`STARS`（收藏）列的值提示了镜像的热度。

- 3. 在我们的示例系统中，我们将从官方源选择并拉取 `httpd` 镜像（`NAME` = `docker.io/httpd`），它恰好也是评分最高的那个。输入 `latest`：Pulling from `docker.io`...

- 4. 在我们的示例系统中，查询本地 `Docker Host` 上的任何现有镜像：
```bash
[root@fedora-server ~]# docker images
```

| REPOSITORY | TAG | IMAGE ID | CREATED | VIRTUAL | SIZE |
| :--- | :--- | :--- | :--- | :--- | :--- |
| docker.io/httpd | latest | de979434d9d4 | weeks ago | | 16MB |

## 使用容器

`Docker` 镜像是构成容器的“比特区块”。你将在官方 `Docker` 公共仓库中找到由各种项目、组织和个人创建的数千个镜像。

`Docker` 是一组工具和接口，用于以容器的形式开发、管理、交付和运行应用程序。`Docker` 可以利用各种机制访问 Linux 内核的虚拟化内部/接口，主要的机制是 `libcontainer` 库。具体来说，它利用 Linux 内核暴露的命名空间（`namespace`）和控制组（`cgroups`）接口来提供其隔离和资源共享的优势。

一些术语和概念在 `Docker` 世界中是独特且常用的。在这里，我们概述了：

- `Docker` 镜像形成了 `Docker` 生态系统的构建模块。它们是创建容器的只读蓝图。当 `Docker` 从镜像运行容器时，它会在镜像上层添加一个读写层。
