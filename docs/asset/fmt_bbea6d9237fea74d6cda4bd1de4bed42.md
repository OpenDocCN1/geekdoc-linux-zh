
# 第 6 章 启动与关机

Linux 管理：初学者指南

随着现代操作系统复杂性的不断增加，其启动和关机过程的复杂性也随之增长。任何经历过从纯 DOS 扩展到微软 Windows 系统转变的人，都亲身体验过这一点。现在是核心操作系统的启动和关机，但与 Windows 一样，必须启动并停止大量的服务和进程（其中一些至关重要，另一些则没那么重要）。

在本章中，我们将讨论使用 GRUB 和 Linux 加载器（LILO）进行 Linux 操作系统的自引导。随后，我们将逐步介绍 Linux 环境的启动和关机过程，以及在脚本中某些可能需要的修改。最后，我们将介绍一些与启动和关机相关的杂项。

> 注意：在真实/生产系统执行本章的实践练习时，请务必常识。在实验修改启动和关机脚本时，请记住，可能会导致系统进入无法通过重启恢复的非正常状态。不要对生产系统进行乱操作；如果必须这样做，请确保已备份所有想要更改的文件，最重要的是要准备好一张可以启动的救援盘。

## 引导加载器

任何操作系统要在标准 PC 硬件上启动，都需要一个所谓的引导加载器（boot loader）。如果你只在 PC 上处理过 Windows，你可能从未需要直接与引导加载器交互。引导加载器是计算机启动时运行的第一个软件程序。它负责将系统的控制权交给操作系统。

通常，引导加载器存在于磁盘的主引导记录（MBR）中，它知道如何让操作系统启动并运行。Linux 发行版的主要选择是 GRUB，以及较少的 LILO。本章重点关注 GRUB，因为它是较新 Linux 发行版中自带的最常见引导加载器，而且它提供的功能比 LILO 多得多。GRUB 目前有两个版本——GRUB Legacy 和 GRUB 版本 2 (`GRUB 2`)。

出于历史原因，此处简要提到 LILO。LILO 和 GRUB 都可以配置为启动其他非原生操作系统。

## GRUB Legacy

大多数现代 Linux 发行版在安装期间都使用 GRUB 作为默认引导加载器，包括 Fedora、Red Hat Enterprise Linux (`RHEL`)、openSUSE、Debian、Mandrake、CentOS、Ubuntu 等许多。GRUB 的目标是兼容多启动规范（Multiboot Specification）并提供许多功能。

GRUB 的引导过程分阶段进行。每个阶段都由特殊的 GRUB 镜像文件加载，每个阶段都会帮助下一个阶段。其中两个阶段是必不可少的，其他阶段是可选的，并取决于特定的系统设置。

> 警告：请记住，本 GRUB Legacy 部分中的大部分信息和所有示例练习也适用于运行旧版本 GRUB 的系统。这包括 GRUB 版本 0.99 及更早版本。

在基于 RPM 的系统上，可以通过运行以下命令检查 GRUB 版本：

```bash
# rpm -qa | grep -i grub
```

在基于 Debian 的系统上，你可以运行以下命令检查你的 GRUB 版本

```bash
# dpkg -l | grep -i grub
```

如果输出显示你正在运行 GRUB 2 或更高版本（版本 1.98、1.99 等），那么在不先降级到 GRUB Legacy 的情况下，你将无法进行练习。

### 第 1 阶段

在此阶段使用的镜像文件是关重要的，它首先用于启动 GRUB。它通常嵌入在磁盘的 MBR 或分区的引导区中。此阶段使用的镜像文件命名为 `stage1`。阶段 1 镜像可以加载阶段 1.5，也可以直接加载阶段 2。

### 第 2 阶段

阶段 2 实际上由两种类型的镜像组成：中间镜像（可选镜像）和实际的 `stage2` 镜像。为了区分起，可选镜像被称为阶段 1.5。阶段 1.5 镜像充当阶段 1 和阶段 2 之间的桥梁。阶段 1.5 镜像是特定于文件系统的；也就是说，它们理解某个文件系统的语义。

阶段 1.5 镜像的名称为 `x_stage_1_5`，其中 `x` 可以是 `e2fs`、`ReiserFS`、`JFS`、`MINIX` 等类型的文件。例如，加载位于文件分配表 (`FAT`) 文件系统的操作系统所需的阶段 1.5，其名称类似于 `fat_stage1_5`。阶段 1 镜像允许 GRUB 访问多个文件系统。当使用时，阶段 1.5 有助于在文件系统中定位阶段 2。

接下来是实际的 `stage2` 镜像。它是 GRUB 的核心。它包含了加载启动操作系统内核的实际代码，显示引导菜单，还包含一个可以执行 GRUB 命令的 GRUB shell。GRUB shell 是交互式的，有助于让 GRUB 变得灵活。例如，可以使用 shell 启动当前未列在 GRUB 引导菜单中的项目，或从备选的支持介质自引导（bootstrap）操作系统。

其他类型的阶段 2 镜像还有 `stage2_forter` 镜像、`nbgroup` 镜像和 `pxegrub` 镜像。`stage2_forter` 用于光盘。`nbgroup` 和 `pxegrub` 镜像都是网络类型，可以通过网络（DHCP、PXE 或 TFTP）使用。下面是这些内容的简要列表。

## GRUB 中使用的约定

GRUB 有自己的一套引用设备的方式。GRUB 从 0 开始计数。例如，GRUB 将主磁盘标记为 `hd0`。分区位于括号内，例如 `(hd0,0)`。

> 注意：GRUB 不区分不同的接口类型（例如 IDE、SATA）。

## 安装 GRUB Legacy

大多数 Linux 发行版在正常安装期间提供安装 GRUB 的选择。然而，在某些情况下，由于意外或设计，你拥有另一种类型的引导加载器（如 LILO 或 NT 加载器），但你想用 GRUB 替换或覆盖该引导加载器。

本节将向你展示如何安装 GRUB。将在运行系统中使用 `grub` 命令原生安装。

### 备份 MBR

在进行后续练习之前，为你的“良好”MBR 备份是一个好主意。使用 `dd` 命令可以轻松实现。由于 PC 的 MBR 位于磁盘的前 512 字节，你可以通过输入以下命令将这 512 字节拷贝到文件中：

```bash
dd if=/dev/sda of=/tmp/COPY_MBR bs=512 count=1
```

此命令将 MBR 保存到 `/tmp` 目录下的 `COPY_MBR` 文件。

### 从 GRUB Shell 安装 GRUB

现在我们已经处理了安全措施，可以全方位探索 GRUB 了。在这里，你将在如何在运行系统中使用 `grub` 命令原生安装 GRUB。

通过执行 `grub` 命令启动 GRUB shell：

```bash
server:~ # grub
正在探测设备以猜测 BIOS 驱动器。这可能需要很长时间。
```

显示 GRUB 的根设备：

```bash
grub> root
root
(fd0): 文件系统未知，分区类型 0x0
```

输出显示，除非另有说明，否则 GRUB 默认使用第一个软磁盘驱动器 (`fd0`) 作为其根设备。

将 GRUB 的根设备设置为本地磁盘上包含（boot 目录的分区：

```bash
grub> root (hd0,0)
root (hd0,0)
文件系统类型为 ext2fs，分区类型为 0x83
```

> 注意：`/boot` 目录可能也可能可能与根目录 (`/`) 位于同一个分区上。在我们的示例系统上安装操作系统期间，`/boot` 目录存储在 `/dev/sda1` 分区上，因此，我们使用 GRUB `(hd0,0)` 设备。

4. 确保可以在根设备上找到 stage 镜像：

```bash
grub> find /grub/stage1
find /grub/stage1
(hd0,0)
```

输出意味着 `stage1` 镜像文件位于 `(hd0,0)` 设备上。

5. 最后，将 GRUB 引导加载程序直接安装到硬盘的 MBR 上：

```bash
grub> setup (hd0)
setup (hd0)
Checking if "boot/grub/stage1" exists... no
Checking if "/grub/stage1" exists... yes
Checking if "/grub/stage2" exists... yes
Checking if "/grub/e2fs_stage1_5" exists... yes
Running "embed /grub/e2fs_stage1_5 (hd0)"... 26 sectors are embedded.
succeeded
Running "install /grub/stage1 (hd0) (hd0)l+26 p (hd0,0)/grub/stage2
/grub/grub.conf"... succeeded
Done.
```

6. 退出 GRUB shell：

```bash
grub> quit
```

158 Linux 管理：初学者指南
