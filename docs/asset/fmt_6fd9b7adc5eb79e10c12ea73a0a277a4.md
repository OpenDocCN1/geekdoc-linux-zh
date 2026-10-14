
```bash
mattias@laptop:~/.config/fw$ sudo ./lock-down.sh
[sudo] password for mattias: Locking down firewall
mattias@laptop:~/.config/fw$ # 今天在所有平台上检测并停止电脑病毒。此外，我们正在与不同的人整合，这意味着 Ubuntu 可能会下载病毒，如果我们把它们全部发送，我们可能也会感染他人。为了避免这种情况，使用杀病毒软件是一个良好的做法。
```

从安装开源工具 ClamAV 开始：
https://www.clamav.net/
`sudo apt-get install clamav`

安装 ClamAV 的同时也会安装 `clamscan` 工具。`clamscan` 可以扫描你的文件夹中的任何病毒。要扫描你下载文件夹中的文件，请在文件夹中运行 `clamscan`：
`mattias@laptop~$ clamscan Downloads/`
`/home/mattias/Downloads/818_1-reviewed-1.docx: OK`
`/home/mattias/Downloads/balenaEtcher-1.13-x64.AppImage: OK`
`/home/mattias/Downloads/NVIDIA-Linux-x86_64-525.85.05.run: OK`
`/home/mattias/Downloads/818_2_Reviewed_mh_1.docx: OK`
`/home/mattias/Downloads/Invoice.pdf: OK`
`/home/mattias/Downloads/818_1-reviewed_AS.docx: OK`
`/home/mattias/Downloads/818_2_Reviewed_AS.docx: OK`
`/home/mattias/Downloads/818_2_Reviewed_mh.docx: OK`

113

# 第 5 章

## 准备虚拟化环境

### 引言

虚拟化改变了我们使用计算机（包括桌面和服务器）的方式，使得在同一台主机上运行多个操作系统成为可能。这有助于更好地利用主机的资源，并区分运行中的不同操作系统。虚拟化是云提供商使用一台物理服务器的方式，然后你可以在其添加虚拟机。在本章中，我们将安装 KVM 并设置和运行虚拟机。然后我们将查看如何将虚拟机连接到网络并运行任务。还有虚拟化引擎，我们将查看来自 HashiCorp 的工具 Vagrant。

### 结构

在本章中，我们将涵盖以下主题：

- Ubuntu 中的虚拟化概述
- Ubuntu 中的 KVM 虚拟化
- 创建桥接 (Bridge)
- 安装我们的第一个虚拟机
- 你的虚拟机设置
- 快速照 (Snapshots)
- 访问虚拟机
- 在虚拟机中直接使用硬件设备
- 其他虚拟化技术
- 使用 Vagrant 进行构建和运行

### 目标

在本章结束时，我们将理解如何设置基础网络以供运行在主机上的虚拟机使用。我们还将查看 Linux 默认虚拟化引擎 KVM。我们还会查看一些虚拟化引擎、使用 Vagrant 在不同引擎之间共享和使用虚拟机、如何迁移镜像以及如何测试虚拟化。

### Ubuntu 中的虚拟化概述

在运行服务器或桌面系统时，有时你想要运行同一个操作系统的多个版本。如果你与许多客户工作，你可以为每个客户准备一个桌面，或者准备许多台服务器。然而，你可以更有效地共享计算机资源。为了实现这一点，虚拟化允许你安装操作系统，然后在其内部安装不同的操作系统，这些系统共享相同的 CPU 和内存，但是隔离的，并表现为独立的服务器或桌面级设备。

这主要用于你想测试服务器、轻松地拍摄快照并恢复状态到命令行的情况。当你想要将不同系统相互隔离时，安全性也是一个大问题。例如，你有许多客户，并希望客户之间相互隔离。如果一个虚拟桌面感染了病毒，你可以轻松地销毁该虚拟机并创建一个新的使用。

所有云提供商都使用虚拟化作为其服务器的基础。因此，当你在云端启动服务器时，你启动的服务器是一个虚拟服务器。有很多不同的虚拟化引擎，我们将查看其中一些。它们的工作原理都是相同的。你的 CPU 需要支持全虚拟化。你可以运行以下命令来验证并进入计算机的 BIOS 模式启用虚拟化。然而，如果你的计算机不支持虚拟化，性能将会缓慢。

测试计算机是否支持虚拟化的命令：

`mattias@laptop: sudo kvm-ok`

### Ubuntu 中的 KVM 虚拟化

KVM 是 Ubuntu 中标准虚拟化引擎的名称。按照如下方式安装 KVM：

`sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager`

将你的用户名添加到 `libvirt` 组。这将赋予你创建和控制虚拟机的正确权限，如下：

`sudo adduser username libvirt`

在我们创建第一个虚拟机之前，让我们验证我们的主机上是否具有硬件支持。运行以下命令来测试你的计算机支持种种虚拟系统：

`mattias@laptop:~ sudo apt install cpu-checker`
`mattias@laptop: sudo kvm-ok`
`mattias@laptop: INFO: /dev/kvm exists`
`mattias@laptop: KVM acceleration can be used`
`mattias@laptop:~`

`kvm-ok` 命令返回“KVM acceleration can be used”，说明我们拥有支持。如果命令输出无法使用加速，我们仍然安装虚拟机，但性能会较慢。

现在我们拥有了启动虚拟化的所有工具和程序，但首先，让我们创建一个桥接网络。这使得我们很容易从主机计算机连接到虚拟机。

在虚拟化中，我们可以使用不同类型的网络，如下：

- NAT 网络：在这里，主机计算机充当路由器，你的虚拟服务器位于一个独立的子网之后。如果你想将自己与大网络隔离开，但又希望主机计算机具有访问权限，这种方法非常有效。
- 桥接模式 (Bridge mode)：在这里，我们在主机计算机上创建一个桥接，然后与虚拟机共享该桥接。然后虚拟机将访问网络上的另一台计算机，并像主机一样从你的路由器获取 IP。
- MAC Tap：在这里，虚拟机将在你的网卡上添加一个 tap 设备并从你的网络获取 IP，这与主机处于同一个网络。然而，你将无法与主机或虚拟机进行通信。

在使用桥接模式时，我们只需要配置一些设置，并且仅在你计划从主机计算机和其他本地 IP 客户端连接到虚拟机时。

你也可以使用 MAC Tap 从本地网络获取 IP，并让其他网络客户端通过 MAC Tap 接口连接到虚拟机。然后你也可以添加一个桥接。

### 创建桥接

当你在云端启动服务器时，你启动的服务器是一个虚拟服务器。有很多不同的虚拟化引擎，我们将查看其中一些。它们的工作原理都是相同的。

你的 CPU 需要支持全虚拟化。你可以运行以下命令来验证并进入计算机的 BIOS 模式启用虚拟化。然而，如果你的计算机不支持虚拟化，性能将会缓慢。

测试计算机是否支持虚拟化的命令：

`mattias@laptop: sudo kvm-ok`

### 安装我们的第一个虚拟机

可以使用以下步骤安装你的第一个 Ubuntu 虚拟机：

1. 转到 Ubuntu 下载页面，下载 Ubuntu Desktop iso，并存储在你的下载文件夹中。
https://ubuntu.com/download/desktop
2. 启动 KVM 工具虚拟机管理器 (`virtual manager`)，点击**添加虚拟机 (add virtual machine)** 按钮。然后你将获得引导设置第一个虚拟机。填入你的值或保持默认值，直到看到网络设置。
3. 在网络设置中，选择桥接 (`bridge`)，并将我们之前创建的桥接名称作为网络设备。
4. 启动虚拟机并按照指南安装 Ubuntu。（我们在第 2 章中介绍过 Ubuntu 的安装：安装、升级和配置 Ubuntu 桌面）
5. 安装完成后，启动你的虚拟机并登录。下图显示了在虚拟机内部运行的登录界面：

![](img/729ff652633ff312828be609e679849e_120_0.png)

我们在 Ubuntu 桌面内部运行着一个 Ubuntu 虚拟机（VM）。通过它，我们可以将虚拟机当做一个普通应用程序使用，并像平时一样打开和关闭它。

### 虚拟机设置

当你在 KVM 管理器中打开虚拟机时，你可以在顶部菜单看到一个带有小字母“i”的蓝色圆圈。点击它可以打开虚拟机的设置页面。在这里，你可以添加新的网卡、磁盘等。某些设置需要你停止并重启虚拟机，但某些设置可以在虚拟机运行时进行更改。

图 5.2 显示了可以更改的设置的设置页面。在这里，你可以添加磁盘或更多网络设备：

![](img/729ff652633ff312828be609e679849e_121_0.png)

图 5.2：显示虚拟机的设置页面

### 快照 (Snapshots)

快照是虚拟机中的某个时间点。如果你需要检查某些内容，可以回到该时间点，并根据快照创建一个新的虚拟机。现在，当我们有一个干净的 Ubuntu 安装时，这个快照就是一个干净的 Ubuntu 安装，如果你想开始一个新的 Ubuntu 桌面，它是一个极佳的起点。

创建一个快照并将其命名为 Stabil。

接下来的图片了带有快照 Stabil 的虚拟机快照页面：

![](img/729ff652633ff312828be609e679849e_122_0.png)

图 5.3：虚拟机的快照管理器页面

### 自定义快照

通过快照，我们还可以创建自己的自定义 Ubuntu 系统，然后从那里启动一个干净的 Ubuntu 桌面。让我们安装一些我们在 Ubuntu 日常工作中使用的工具。然后，我们将创建一个新的快照。现在我们可以克隆这个已经包含了一些基础工具的新 Ubuntu 桌面。这是一种获取预备就桌面的简单方法，如果你需要一个新的、干净的 Ubuntu，或者如果你正在测试新工具并希望在出现问题时恢复，可以使用这种方法。

### 访问虚拟机

有几种方法可以访问虚拟机。使用普通的 SSH 访问来获取机器的命令行（CLI）访问。使用你看到启动的 KVM 提供的桌面，你也可以添加桌面共享工具，使用 VNC 等工具共享桌面。

接下来的图片显示了一个安装了 `openssh-server` 的 Ubuntu 虚拟机，以及从宿主机到虚拟机的 ssh 访问：

![](img/729ff652633ff312828be609e679849e_123_0.png)

**图 5.4：**从宿主机访问虚拟机

### 在虚拟机中直接使用硬件设备

通过 KVM，我们可以将设备直接传递到虚拟机中。例如，当你有一个 GPU 并想在虚拟机内部访问它时，就会这样做。我们许多人使用 Ubuntu 作为日常操作系统；但我们可能想玩游戏。这时，你可以轻松地将 GPU 传递到你的 Windows 系统并在那里使用。你可能还有需要在虚拟机内部访问的 USB 设备或其他硬件设备。要设置硬件直通设备，请查看虚拟机的设置页面。

### 其他虚拟化工具

KVM 是 Linux 的默认虚拟机引擎，但还有很多。当你在一个包含更多操作系统的环境中工作时，使用一个支持更多操作系统的虚拟化引擎是一个好主意。

Oracle 的 VirtualBox 是一个很好的工具，可以用于许多不同的操作系统。它的工作运行方式与 KVM 相同。下载 VirtualBox，访问以下链接：

https://www.virtualbox.org/

另一个虚拟机工具是 VMware Player，可以在以下链接找到：

https://www.vmware.com/se/products/workstation-player.html

这也是一个很好的工具，工作原理与 VirtualBox 类似。

如果你用过其中一种虚拟化工具，你将拥有操作所有这些工具的基础知识。

> 注意：如果你正在运行 KVM，它已经拥有内核访问权限。如果你尝试运行任何其他虚拟化引擎，可能会看到错误。

在 VirtualBox 上，我们将得到错误：VirtualBox 无法启用 AMD-V 扩展。

### 在 KVM 内部构建并运行 Vagrant box

来自 HashiCorp 的 Vagrant 是一种创建虚拟机并将其上传到其云存储的方法。然后，其他人就可以下载并运行该虚拟机。这使得与其他示例构建和共享镜像变得简单。如果你是一个开发者并想与同事共享虚拟机，或者你有一台测试服务器。对于 WordPress 等不同服务也有预制镜像。

在 Vagrant 中，不同的虚拟机被称为 box。因此，在本指南中，box 和 VM 是同一个东西。

首先访问 Vagrant 首页并下载、设置 Vagrant。

https://www.vagrantup.com/

### 在 KVM 内部运行 VirtualBox

为了能够使用 Vagrant 和 VirtualBox 进行测试，我们可以在 KVM 宿主机内部安装它们。

在这里，我们通过 SSH 和桌面从宿主机访问虚拟机，然后直接在终端中运行 vm cli 命令，并查看 VirtualBox GUI，如下所示：

![](img/729ff652633ff312828be609e679849e_125_0.png)

图 5.5：KVM 运行 VirtualBox 和 Vagrant

按照给定的指南在 Ubuntu 上安装 Vagrant。

https://www.vagrantup.com/

### 镜像转换 (Converting images)

创建一个文件夹，并在其中启动 Vagrant：

- 1. `mkdir vagrant`
- 2. `cd vagrant`
- 3. `vagrant box add hashicorp/bionic`
- 4. `vagrant init hashicorp/bionic`
- 5. `vagrant up`

要查找不同的镜像，请访问：

https://www.vagrant.com/boxes/search

正如前一节所述，我们可以在其他工具之间转换镜像。运行虚拟机时，每个镜像都有自己的格式。

在这里，文件位于宿主机上。默认情况下，KVM 镜像位于 `/var/lib/libvirt/images`。

- 1. `root@hr/var/lib/libvirt/images# ls`
- 2. `ubuntu22.04-2.qcow2 ubuntu22.04.qcow2`
- 3. `root@hr/var/lib/libvirt/images#`

让我们一个镜像转换为 vmdk 格式：
