
## 第 29 章 检查云和虚拟化服务

目标 3.5：概述容器、云和编排概念

![](img/c0a399aca0d18f8822d714ad0a173123_856_0.png)

在设计和管理各种云和虚拟化系统配置时，你需要了解虚拟网络和物理网络如何互操作、可用的各种磁盘存储选项、如何自动启动系统，以及如何在你的虚拟机上快速安装 Linux 发行版。此外，你还需要熟悉一些基本的虚拟机创建和管理工具。在本章中，我们将继续第 28 章开启的旅程，深入探讨云和虚拟化的主题。

### 专注于虚拟机工具

各种虚拟机实用程序允许你创建、销毁、启动、关闭和配置你的来宾虚拟机。有许多开源替代品可供选择。有些只能在命令行下工作，有时在 shell 脚本中使用，而有些则提供图形界面。在以下章节中，我们将介绍这些工具中的几个。

### 了解 libvirt

一个流行的虚拟化管理软件集是 `libvirt` 库。该系列包含以下元素：

- 一个应用程序编程接口（API）库，它被整合到多个开源 VMM（管理程序）中，例如 KVM
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

`libvirt` 项目的一个主要目标是提供管理虚拟机的单一方式。它支持许多管理程序，如 KVM、QEMU、Xen 和 VMware ESXi。你可以在 `Libvirt.org` 网站上了解更多关于 `libvirt` 项目的信息。

### 查看 `virsh`

一个使用 `libvirt` 库的实用工具是 `virsh` shell。它是一个基本的 shell，你可以用它来管理系统中的虚拟机。

> **注意**
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

**清单 29.3：交互式使用 virsh 实用程序**

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

在命令行创建虚拟机时，比 virsh 更简单的实用程序是 virt-install。它是一个 Python 程序，根据发行版的不同，通常可以从 virtinst 或 virt-install 软件包中获取。

### 使用 Virtual Machine Manager 进行管理

请注意，Virtual Machine Manager（也称为 VMM）不要与管理程序（VMM）混淆。Virtual Machine Manager 是一个用于创建和管理虚拟机的轻量级桌面应用程序。它是一个在许多使用图形用户界面（GUI）的发行版上可用的 Python 程序，可以从 virt-manager 软件包中获取。

Virtual Machine Manager 可以通过图形环境中的终端模拟器上的 virt-manager 命令启动。图 29.1 展示了 Rocky Linux 8 发行版上的 VMM 用户界面。

**图 29.1 Virtual Machine Manager**

![](img/c0a399aca0d18f8822d714ad0a173123_860_0.png)

你需要使用超级用户权限来运行 Virtual Machine Manager，如果 `virt-manager` 命令不是从具有这些权限的账户发出的，它将打开一个弹出窗口，要求输入 root 账户密码或类似内容，具体取决于发行版。

Virtual Machine Manager 通过其“View”菜单提供的一个很好功能是性能统计图表。此外，GUI 界面允许修改来宾虚拟机的配置，例如它们的虚拟网络（虚拟网络配置将在本章后面介绍）。

![](img/c0a399aca0d18f8822d714ad0a173123_861_0.png)

Virtual Machine Manager 默认提供一个虚拟网络计算（VNC）客户端查看器（`virt-viewer`）。因此，可以将图形（桌面环境）控制台连接到任何正在运行的虚拟机。但是，也可以配置 SPICE 来执行相同的功能。VNC 和 SPICE 在第 8 章“比较 GUI”中已介绍。

你可以在 `Virt-manager.org` 网站上查看 Virtual Machine Manager 的截图，阅读其文档并浏览其代码。

### 理解引导

引导（bootstrap）是鞋后跟上的一个小布料或皮革环。现在你用它们来帮助把鞋子穿到脚上，方法是用手指勾住环并拉紧。从那个小工具衍生出的短语“Pick yourself up by your bootstraps”，意思是不依靠任何外部帮助而从挫折中恢复。

随着时间推移，计算机行业开始模仿该短语，使用术语 *bootstrapping* 和 *booting*。它们经常互换使用，但通常启动系统是指给系统通电并让其通过引导加载程序代码启动。系统的 bootstrap 是指使用配置文件或先前系统安装的映像来安装新系统。

#### 使用 Shell 脚本启动

无论你是创建云中的来宾虚拟机还是在自己本地主机上，都有各种方法可以让它们启动。通过 GUI 启动几个虚拟机并不太难，但如果你公司使用了数百台虚拟机，你需要考虑自动化这个过程。

使用 shell 脚本启动虚拟机通常是一种自行构建的方法，尽管互联网上有许多示例。它在启动公司控制的宿主机器上的来宾虚拟机时效果最好。

![](img/c0a399aca0d18f8822d714ad0a173123_861_1.png)

如果你不想从头开始，请查看 GitHub 上可用的脚本。一个流行的项目，有多个分支，是 `http://github.com/gjtorres/kvm-install`。

你可以为你的各种虚拟机创建配置文件，并在需要时将其读入 shell 脚本中以进行启动。来宾虚拟机可以在宿主系统启动时、预定时间或按需启动。这是一种灵活的方法，允许大量的自定义。

