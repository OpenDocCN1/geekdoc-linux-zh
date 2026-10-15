
| `login` | 登录 Docker hub 仓库 |
| `logs` | 从正在运行的容器获取日志 |
| `ps` | 列出正在运行的容器 |
| `pull` | 从 Docker 仓库获取容器 |
| `push` | 将容器镜像提交到 Docker 仓库 |
| `rm` | 删除已停止的容器 |
| `rmi` | 从本地存储中删除容器镜像 |
| `run` | 启动容器镜像 |
| `stop` | 停止正在运行的容器 |
| `start` | 启动已停止的容器 |

## 练习 28.1

### 使用容器

1. 从你的发行版软件仓库安装 Docker 软件（参见第 13 章“管理软件”）。对于 Ubuntu，输入命令 `sudo apt install docker`。对于基于 Red Hat 的发行版，如 Rocky Linux，命令是 `sudo dnf install docker`。

2. 安装 Docker 软件后，你通过 `docker` 命令与其通信。通过在命令行输入 `sudo docker ps` 来检查 Docker 是否正在运行：

   ```
   $ sudo docker ps
   Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
   CONTAINER ID  IMAGE  COMMAND  CREATED  STATUS  PORTS  NAMES
   ```

   输出显示 Docker 正在运行，并列出当前正在运行的任何容器（目前为空）。

3. 通过输入命令 `sudo docker pull docker.io/library/httpd:latest` 获取用于通用 Apache Web 服务器的 Docker 定制容器镜像。这会导致 Docker 查询 `http://hub.docker.com` 上的 Docker 仓库并获取运行在通用 Linux OS 平台上的最新版本的定制 Apache Web 服务器。如果你需要使用特定版本的 Apache，可以在容器镜像名称后指定，例如 `httpd:2.4`。

4. 通过输入 `sudo docker run -d -t -p 8088:80 --name myApache httpd` 将 `httpd` 容器镜像部署到你的 Docker 环境中。此命令在后台模式下启动容器（`-d` 选项），将终端连接到容器（`-t` 选项），将容器上的 TCP 80 端口暴露给主机上的 8088 端口（`-p` 选项），并为容器赋予一个简单的名称以用于 `docker` 命令。重要的是要记住，容器是自包含的，因此要连接到容器上的端口，你必须指示 Docker 将该端口暴露给主机系统。运行此命令时，Docker 将显示分配给容器的 ID。通过输入 `sudo docker ps` 验证容器是否正在运行。

   ```
   $ sudo docker run -d -t -p 8088:80 --name myApache httpd
   Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
   43eee94b028d7b3c9a168cf29284428b155624f8bf3cfc5cb5c64c56548cc
   $ sudo docker ps
   Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
   CONTAINER ID  IMAGE                       COMMAND       CREATED              STATUS             PORTS                  NAMES
   43eee94b028d  docker.io/library/httpd:latest  httpd-foreground  4 seconds ago  Up 5 seconds ago  0.0.0.0:8088->80/tcp  myApache
   ```

### 练习 28.1（续）

输出结果表明，`httpd` 容器确实在运行，并且它已将容器的 TCP 80 端口映射到宿主系统的 TCP 8088 端口。

5. 在宿主机的 Linux 桌面上打开浏览器并输入 `http://localhost:8088`，以连接到正在容器中运行的 Apache Web 服务器。您将看到 Apache Web 服务器生成的通用“It works!”消息。

6. 通过输入 `sudo docker exec -i -t myApache bash` 在正在运行的容器中打开一个交互式 Bash shell。这将作为交互式终端连接到名为 `myApache` 的容器（`-i` 和 `-t` 选项），并运行 `bash` 命令，生成一个 shell 提示符。您应该会看到类似以下内容：

```bash
$ sudo docker exec -it myApache bash
Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
root@43ee094b028d:/usr/local/apache2#
```

7. Bash shell 命令提示符表示您已以 `root` 用户账户登录到容器操作系统，并且当前位于 `/usr/local/apache2` 目录中。从这里，您可以查看和修改 Apache Web 服务器配置文件，或在 `/usr/local/apache2/htdocs` 目录中创建新的 Web 页面。要返回到宿主系统命令行，请输入 `exit`。

```bash
root@43ee094b028d:/usr/local/apache2# exit
exit
[rich@localhost ~]$
```

8. 通过输入 `sudo docker stop myApache` 停止正在运行的容器。您可以通过输入 `sudo docker ps` 来验证容器已停止。

9. 通过输入 `sudo docker rm myApache` 从您的 Docker 系统中删除该容器。

10. 如果您不想再在工作站上保留 `httpd` 容器镜像，请输入 `sudo docker rmi httpd`。

## 摘要

云计算提供了一种轻松扩展公司计算资源的方式，而无需购买和管理自己的硬件。云计算有三个层级，每个层级提供不同的服务。基础设施即服务 (IaaS) 提供硬件资源，如服务器、存储和网络。平台即服务 (PaaS) 提供开发环境，由操作系统以及开发、测试和交付应用软件所需的任何库组成。软件即服务 (SaaS) 通过互联网从云服务器上运行应用程序。

云计算环境使用虚拟化来实施多台服务器，而无需大量物理硬件。通过虚拟化，一台大型服务器可以托管多个较小的客户系统。管理程序软件管理分配给每个客户系统的资源，并管理这些资源的使用方式。

有两种类型的使用管理程序环境。I 型管理程序直接与系统硬件交互。客户系统直接由管理程序软件接收系统资源。II 型管理程序运行在宿主操作系统之上。宿主操作系统与系统硬件交互，并为 II 型管理程序提供资源，后者进而将资源分配给客户系统。

容器是一种不同类型的虚拟化。容器为单个应用程序提供一致的运行环境。当您部署应用程序到容器中时，无论它在哪个服务器上运行，都保证应用程序容器以相同的方式运行。通过使用容器部署应用程序，您保证应用程序在开发、测试和生产环境中将以相同的方式运行。容器不像虚拟机那样包含大量的开销，使其更容易分发。

## 考试要点

- **描述提供云计算环境的三种主要方法。** 公有云托管在由第三方拥有和运营的服务器上。公司不拥有或运营任何服务器硬件；它只是利用这些服务器上的空间。其他公司可以在同一个公有云中租用空间。私有云托管在位于企业网络内部的服务器上。所有应用程序文件以及数据文件都驻留在企业网络内部。混合云利用私有云服务器，但也将它们与公有云服务器进行接口连接。使用混合云，数据可以位于外部的公有云中，也可以位于内部的私有云上。

- **解释三种云服务类型。** 基础设施即服务 (IaaS) 为客户提供硬件级别的服务。这包括服务器、存储空间以及连接它们的网络资源。平台即服务 (PaaS) 提供用于开发软件的按需环境。在 PaaS 云服务中，服务器硬件、操作系统和运行时库均由云服务提供。软件即服务 (SaaS) 在云环境中运行应用程序，允许客户通过互联网访问这些应用程序。

- **解释两种类型的管理程序。** I 型管理程序直接运行在系统硬件上。它们作为硬件和客户操作系统之间的中介。I 型管理程序为每个客户操作系统分配资源，确保每个系统都能获得足够的资源。II 型管理程序运行在宿主操作系统之上。宿主操作系统与服务器硬件交互；管理程序软件必须通过宿主操作系统来访问资源。客户操作系统仍然仅与管理程序软件交互。

- **描述容器与虚拟机的区别。** 大多数容器包不包含完整的操作系统，但虚拟机包含。容器包仅包含运行特定应用程序所需的库文件和应用程序运行时文件。这使得容器轻量且易于部署。

## 复习题

1. 哪种云服务方法仅利用由第三方拥有和运营的服务器？

    - A. 私有
    - B. 公有
    - C. 混合
    - D. II 型
    - E. I 型

2. Tom 目前在公司内部服务器上运行一个云平台，但他需要额外的处理能力来运行一个新应用程序。他可以检查哪种云服务方法，以便利用现有云平台而无需购买更多的内部服务器？

    - A. 私有
    - B. 公有
    - C. 混合
    - D. I 型
    - E. II 型

3. Sally 有兴趣在云中开发她的应用程序，而不必担心管理操作系统。她应该购买哪种类型的云服务？

    - A. PaaS
    - B. 私有云
    - C. IaaS
    - D. SaaS
    - E. 混合云

4. 哪种类型的云服务允许您在云提供的基础设施上启动自己的操作系统？

    - A. PaaS
    - B. 私有云
    - C. IaaS
    - D. SaaS
    - E. 混合云

5. 哪种类型的管理程序直接与宿主系统硬件进行接口？

    - A. 私有
    - B. 公有
    - C. II 型
    - D. I 型
    - E. 混合

6. Henry 已经在他的服务器上安装了 Red Hat Linux，但现在需要安装虚拟机。他应该使用哪种类型的管理程序包？

    - A. 私有
    - B. 公有
    - C. II 型
    - D. I 型
    - E. 混合

7. 哪种类型的管理程序模板将所有配置文件打包到单个文件中以便分发？

    - A. XML
    - B. JSON
    - C. OVA
    - D. OVF
    - E. YAML

8. Fred 想要打包他的应用程序，以确保无论他的客户使用哪种 Linux 发行版，它都能以相同的方式运行。他该如何做到这一点？

    - A. 将应用程序打包为容器。
    - B. 将应用程序打包为管理程序。
    - C. 将应用程序部署到私有云。
    - D. 将应用程序作为虚拟机部署。
    - E. 将应用程序捆绑为 `tar` 文件并部署。

9. 您应该使用哪种方法轻松地将应用程序从开发环境迁移到生产环境，而无需复制操作系统？

    - A. 公有云
    - B. 私有云
    - C. I 型管理程序
    - D. II 型管理程序
    - E. 容器

10. 哪种 Linux 容器包在宿主操作系统上以进程形式运行引擎，并提供一个命令行界面来控制容器？

    - A. Snap
    - B. Docker
    - C. KVM
    - D. XEN
    - E. VirtualBox

## 第 29 章 检查云和虚拟化服务

目标 3.5：概述容器、云和编排概念

![](img/c0a399aca0d18f8822d714ad0a173123_856_0.png)

在设计和管理各种云和虚拟化系统配置时，你需要了解虚拟网络和物理网络如何互操作、可用的各种磁盘存储选项、如何自动启动系统，以及如何在你的虚拟机上快速安装 Linux 发行版。此外，你还需要熟悉一些基本的虚拟机创建和管理工具。在本章中，我们将继续第 28 章开启的旅程，深入探讨云和虚拟化的主题。

### 专注于虚拟机工具

各种虚拟机实用程序允许你创建、销毁、启动、关闭和配置你的来宾虚拟机。有许多开源替代品可供选择。有些只能在命令行下工作，有时在 shell 脚本中使用，而有些则提供图形界面。在以下章节中，我们将介绍这些工具中的几个。

### 了解 `libvirt`

一个流行的虚拟化管理软件集是 `libvirt` 库。该系列包含以下元素：

- 一个应用程序编程接口（API）库，它被整合到多个开源 VMM（管理程序）中，例如 `KVM`
- 一个守护进程 `libvirtd`，它运行在虚拟机宿主系统上，并执行所需的来宾虚拟机管理任务，例如启动和停止虚拟机
- 命令行实用程序，例如 `virt-install` 和 `virsh`，它们运行在虚拟机宿主系统上，用于控制和管理来宾虚拟机

通常，大多数以 `vir` 或 `virt` 开头的命令行实用程序都使用 `libvirt` 库，你可以使用 `ldd` 命令来再次确认这一点。下面是一个在已安装管理程序软件包的 Rocky Linux 发行版上的示例，如清单 29.1 所示。

**清单 29.1：使用 `ldd` 命令检查 `libvirt`**

```bash
$ which virsh
/usr/bin/virsh
$
$ ldd /usr/bin/virsh | grep libvirt
libvirt-lxc.so.0 => /lib64/libvirt-lxc.so.0 (0x00007f4a3a10c000)
libvirt-qemu.so.0 => /lib64/libvirt-qemu.so.0 (0x00007f4a39f08000)
libvirt.so.0 => /lib64/libvirt.so.0 (0x00007f4a39934000)
$
```

`libvirt` 项目的一个主要目标是提供管理虚拟机的单一方式。它支持许多管理程序，如 `KVM`、`QEMU`、`Xen` 和 `VMware ESXi`。你可以在 `Libvirt.org` 网站上了解更多关于 `libvirt` 项目的信息。

### 查看 `virsh`

一个使用 `libvirt` 库的实用工具是 `virsh` shell。它是一个基本的 shell，你可以用它来管理系统中的虚拟机。

> **注意**
>
> 如果你想尝试 `virsh` shell，可以通过 `libvirt-client` 或 `libvirt-clients` 软件包获取它。对于较旧的发行版，它可能位于 `libvirt-bin` 软件包中。软件包安装在第 13 章“软件治理”中已有介绍。请注意，创建虚拟机需要额外的软件包。

如果你已安装 VMM（管理程序）产品，可以使用 `virsh` shell 来创建、删除、启动、停止和管理你的虚拟机。清单 29.2 展示了进入和退出 `virsh` shell 的示例。请记住，涉及虚拟机的 shell 命令通常需要超级用户权限。

**清单 29.2：探索 `virsh` shell**

```bash
$ virsh
Welcome to virsh, the virtualization interactive terminal.
Type: 'help' for help with commands
'quit' to quit
virsh # exit
$
```

你不必进入 `virsh` shell 就可以管理你的虚拟机。各种 `virsh` 命令可以直接从 Bash shell 中输入，这使得那些希望在 shell 脚本中使用命令以自动化虚拟机管理的人员非常受益。清单 29.3 展示了交互式使用 `virsh` 实用程序的示例。

**清单 29.3：交互式使用 `virsh` 实用程序**

```bash
$ virsh help setcpus
NAME
    setcpus - change number of virtual CPUs
SYNOPSIS
    setcpus <domain> <count> [--maximum] [--config]
    [--live] [--current] [--guest] [--hotpluggable]
DESCRIPTION
    Change the number of virtual CPUs in the guest domain.
OPTIONS
    [--domain] <string>    domain name, id or uuid
    [--count] <number>     number of virtual CPUs
    --maximum              set maximum limit on next boot
    --config               affect next boot
    --live                 affect running domain
    --current              affect current domain
    --guest                modify cpu state in the guest
    --hotpluggable         make added cpus hot(un)pluggable
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_859_0.png)
