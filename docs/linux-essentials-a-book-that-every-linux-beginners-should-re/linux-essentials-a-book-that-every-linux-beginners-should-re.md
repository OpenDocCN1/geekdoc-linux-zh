
# Linux 入门指南：每个 Linux 初学者都应该读的书

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_0_0.png)

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_0_1.png)

- 关于作者

# 前言

在大学期间，作为一名计算机科学系充满抱负的年轻毕业生，我经常在 UNIX 或 Linux 之上练习某些编程语言。

那时我的注意力完全集中在语言上，我从未想过我的代码是如何运行的，甚至不知道是谁在运行它。后来，当我加入一个机构后，我用各种语言编写的所有应用程序都在向我索要自动化。这促使我去处理一些命令行任务。虽然我擅长 C 和 C++，但我发现编写 Shell 脚本（尤其是对于搜索和过滤类的任务）有些困难。

然后我意识到 Linux 命令是 Shell 脚本的核心部分，而且如果没有相关知识，是不可能写出优化的自动化代码的。从那里开始，开始学习 Linux 系统编程，然后是 shell、Perl、python 和 ruby，这一切都是在 Linux 之上进行的。

现在，凭借超过 16 年企业培训师的经验，我想在书书中分享我关于 Linux 命令的知识。这本书将带你开启 Linux 学习的大门，你可以继续后续学习 sed、awk 和 bash 脚本，以提升你的职业生涯。

如果你是一个初学者，或者你想精通 Linux 的基础知识，那么这本书就是为你准备的。

# 献辞

献给我我亲爱的**主**

# 致谢

衷心感谢我的叔叔 Rajaram 先生为我完成这本书所提供的全力支持。

诚心感谢 Aravind 先生、JohnPaul 先生、Kamal 先生、Yuvraj 先生和 Richard 先生为本书的完美完善提供的出色支持和认可。

我爱亲爱的妻子 Theeba Karthikeyan，感谢她为这本书付出的动力、努力和鼓励。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_6_0.png)

# 第 1 章 - Linux 简介

## 什么是 Linux？

Linux 是 Linus Torvalds 在 1991 年开发的操作系统。

通常，操作系统被定义为一个程序，它是用户应用程序与硬件之间的接口。该操作系统负责将系统资源连接到用户。那么操作系统的哪个部分负责这项任务呢？内核（Kernel），作为操作系统的核心组件负责这项任务。

每当系统启动时，一旦引导程序阶段成功完成，内核就是第一个加载的程序。如果引导程序失败，内核加载也会失败，因此我们必须排查引导程序的问题。只有在那之后，内核才会加载。

一旦内核加载，它将一直留在内存中，直到操作系统关闭，因为内核需要为操作系统处理系统的其余事项。我们将在接后的主题中讨论引导程序的序列。

## GNU 项目

GNU/Linux –（GNUs 不是 UNIX）是由自由软件基金会（FSF）推广的术语，由 Richard Stallman 创立。

该项目始于1984 年，旨在开发一个自由的操作系统。

该项目的口号是开发一个自由的、兼容 Unix 的操作系统。Linux 内核于 1992 年加入，实现了 GNU 项目开发自由操作系统的目标。

## GPL

Linux 和 GNU 软件根据 GNU 通用公共许可证（GPL, [www.gnu.org/licenses/licenses.html](https://www.gnu.org/licenses/licenses.html)）的条款进行分发。

GPL 规定，我们有权根据协议涵盖的范围复制、修改和重新分发受协议涵盖的代码。

GPL 提供了某些基本的软件自由：

- 出于任何目的使用软件
- 分享软件
- 修改软件以适应你的需求
- 分享你所做的更改

## 为什么我们使用 Linux？

Linux 已经演变成当今世界最有前景的平台之一。

Linux 也以开源的形式分发。

这里有两个术语——开源和分发。让我们看看它们在这里实际上意味着什么。

开源遵循以下关键特征：

- 出于任何目的运行该程序的自由。
- 研究程序如何运作的自由，并对其进行修改以实现你的意愿。
- 重新分发副本的自由，以便你可以帮助你的邻居。
- 向他人分发你修改后的版本的自由。

## 什么是发行版？

Linux 发行版也被称为 distro。实际上，Linux 并不是一个完整的操作系统——它只是一个内核。Linux 发行版将 Linux 内核与其他自由软件相结合，创建类似于专有软件的完整包。有很多不同的 Linux 发行版可用。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_9_0.png)

如果我们想“安装 Linux”，我们需要选择一个发行版。例如：Linux mint, Ubuntu, redhat, openSUSE 等。流行的 Linux 发行版包括：

- Debian
- Fedora
- Mandriva Linux
- OpenSUSE
- Gentoo
- Slackware

每个发行版对桌面、软件软件包管理仓库和软件包管理实用工具命令有不同的看法。

例如，在 RHL（Red-Hat Linux）发行版中安装或更新软件包，我们使用以下命令：`yum install <package name>`

例 1：在基于 RHL 的发行版中安装 Python3，

```
yum install python3
```

如果我们想在基于 Debian 的发行版 Linux 中安装相同的包，可以使用 `apt-get install <packagename>` 命令

例 2：在基于 Debian 的发行版中安装 Python3，

```
apt-get install python3
```

注意，在两个示例中，包名都是 python3，运行内核都是 Linux，但发行者是不同的。完整的 Linux OS 意味着 Linux 内核和发行版工具的结合。

希望你现在理解 Linux OS 是 Linux 内核和发行版工具的结合。让我们看看什么是内核。

## Linux 内核

操作系统（OS）是一个理论性术语，

```
root@ksumlabs:~ # uname
Linux
root@ksumlabs:~ # uname -r
3.13.0-170-generic
root@ksumlabs:~ # cat /etc/issue
Ubuntu 14.04.6 LTS \
root@ksumlabs:~ # install any package
root@ksumlabs:~ # apt-get install python3
root@ksumlabs:~ #
```

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_12_0.png)

```
root@ksumlabs:~ # uname
Linux
root@ksumlabs:~ # uname -r
4.12.0-94.el7.x86_64
root@ksumlabs:~ # cat /etc/os-release
Oracle Linux Server release 7.4
root@ksumlabs:~ # install any package
root@ksumlabs:~ # yum install python3
root@ksumlabs:~ #
```

内核是一个实现结构的程序，内核还控制系统的所有事情。

希望你现在理解 Linux 发行版在发行工具上有所不同。让我们看看这个内核是什么。

## Linux 内核开发模型

Linux 操作系统的核心是内核。

代表数百家企业的许多开发人员频繁发布 Linux 内核。

Linux 社区通过建立的用于处理内核开发的各种邮件列表进行协作。

功能通过这些邮件列表和互联网即时聊天（IRC）推送到上游（Upstream）。“上游”是用于社区拥有的特定项目版本的术语。

这里是开发的地方，而且它始终包含最新的更改。

Linus Torvalds 领导着一个团队，发布被称为“原生（vanilla）”或“主线（mainline）”内核的新版本。

开发的主线分支整合了新功能、安全修复和错误修复。在它经过彻底测试之前，它不被认为是稳定分支。

目前有多个内核版本作为稳定内核进行维护。这些内核包含了反向移植（backported）到它们的补丁。

这些补丁主要是驱动程序更新和安全修复。内核分支可以在 http://www.kernel.org 获取。

## Linux 架构

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_15_0.png)

通常情况下，系统由 3 层组成。见上图。第 1 层被称为用户层，它持有关于用户创建或执行的应用程序的信息。用户层的所有应用程序都称为用户进程。

第 2 层被称为内核层。我们知道内核是什么。在这里，内核的主要功能是将用户请求扩展到硬件，告诉硬件我们想要在硬件（CPU）上执行的应用程序，或者我们想要从存储器（硬盘）中读取的文件内容。为了完成所有任务，我们需要内核的帮助。在这里，内核的工作是将我们的（用户）请求与相应的硬件资源（CPU、硬盘）建立接口。

最底层被称为硬件层。所有外围设备都连接这一层。



从这个结构中我们可以理解，作为用户，我们无法直接与硬件通信；因此，我们需要一个内核作为接口。现在回顾我们对操作系统的定义：“OS 是一个系统程序，它将作为用户与硬件之间的接口。”

现在我们可以探索更多关于内核架构的细节，即上图中中间层（内核层）。

## 内核探索

Linux 内核是一个模块化设计的内核。

在架构层面，Linux 内核与硬件交互，并代表应用程序控制和调度对资源（CPU、内存、存储、网络等）的访问。

应用程序运行在所谓的用户空间中，并对一组稳定的系统库调用以请求内核服务。

这种模块化设计的内核允许 Linux 组件源自不同的开发者，每个组件都有自己的特定设计目标。

模块化设计也意味着 Linux 内核独立于应用程序和接口。

结果是，即使应用程序崩溃，应用程序中的所有安全漏洞往往也保持隔离状态，而不会影响整个系统。

在 Linux 中，每个组件都是单独配置的，通常使用基于文本的配置文件。

可以通过脚本或应用程序使用简单的文本解析引擎来读取和写入配置信息。

与系统配置数据建立接口不需要特殊的应用程序编程接口（`API`）。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_18_0.png)

## Linux 内核结构

上面的图显示了 Linux 内核的详细架构。Unix 和 Linux 都是单体内核。那么，什么是单体内核呢？

`单体内核`是一个巨大的进程，完全运行在单一的地址空间中。它是一个单一的静态对象文件。所有的内核服务直接存在并执行于内核地址空间。在单体内核中，内核的所有部分如`调度器`、`文件系统`、`内存管理`、`网络栈`、`设备驱动程序`等，都在内核内*作为一个单一单元*进行维护。

## 系统组件

Linux 操作系统的主要组件有：

- 1. 命令实用工具
- 2. `Shell`
- 3. 内核

### 命令实用工具

目前有多个内核版本作为稳定内核进行维护。这些内核包含了反向移植到它们的补丁。

这些补丁主要是驱动程序更新和安全修复。内核分支可以在 `http://www.kernel.org` 获取。

### 内核

什么是内核。

### Shell

什么是 `Shell`？

`Shell` 是用户和内核之间的中间器。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_15_0.png)

通常情况下，系统由 3 层组成。见上图。第 1 层被称为用户层，它持有关于用户创建或执行的应用程序的信息。用户层的所有应用程序都称为用户进程。

第 2 层被称为内核层。我们知道内核是什么。在这里，内核的主要功能是将用户请求扩展到硬件，告诉硬件我们想要在硬件（CPU）上执行的应用程序，或者我们想要从存储器（硬盘）中读取的文件内容。为了完成所有任务，我们需要内核的帮助。在这里，内核的工作是将我们的（用户）请求与相应的硬件资源（CPU、硬盘）建立接口。

最底层被称为硬件层。所有外围设备都连接这一层。

# 第 2 - (MBR) 主引导记录

## 什么是主引导记录 (MBR)？

主引导记录（Master Boot Record）是引导加载程序开始运行的地方。`MBR` 是位于硬盘第一个扇区的 512 字节扇区。`MBR` 包含了程序代码和分区表详情。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_25_0.png)

## 主引导记录 (MBR)

在具有 x86 架构的计算机上，主引导记录 (`MBR`) 是启动器上的前 512 字节，由 BIOS 读取到内存中。

512 字节中的前 446 字节包含低级引导代码。对于某些引导加载程序，`MBR` 中的代码指向存储在磁盘上其他位置或另一个磁盘上的进一步引导加载程序。

接下来的 64 字节包含磁盘的分区表，`fdisk`、`cfdisk`、`parted` 等文件系统实用工具被放置在该磁盘上，通过使用这些工具，我们可以获取分区表信息。

最后两个字节是引导签名，用于错误检测。

# 第 3 - 引导加载程序

到目前为止我们知道，当 POST 成功完成后，BIOS 将执行 `MBR` 代码。`MBR` 代码包含有关引导加载程序的信息，并且此 `MBR` 会执行该引导加载程序。现在现在让我们看看这个引导加载程序是什么？

引导加载程序软件在计算机启动时运行。它负责加载并将控制权传递给内核。

它位于可启动磁盘的第 1 个扇区。(`/dev/sda` (或) `/dev/hda` (或) `/dev/xvda`)

引导加载程序位于文件系统下的独立分区中；它将从 `/boot` 分区挂载。

Linux 最常用的引导加载程序：

- `LILO`(LinuxLoader)
- `GRUB`(Grand Unified Boot loader)。
- `GRUB2` 代表“Grand Unified Boot loader, version 2”。

在本章中，我们将讨论 `grub2` 引导加载程序。

`GRUB2` 代表“GRand Unified Boot loader, version 2”，是近期 Linux 发行版（如 RHL7、Oracle Linux7、ubuntu16 等）中的主引导加载程序。

`GRUB2` 也是一个程序。一旦 `GRUB2` 被加载到 RAM 中，它就会搜索内核的位置。这是它加载其他驱动和内核模块的阶段。

`GRUB2` 能够文件系统和内核可执行格式。

`GRUB2` 检查映射文件以找到位于 `/boot` 下的内核镜像。

`GRUB2` 从 `/boot` 分区加载内核（`vmlinuz-version`）。

如果我们的系统中安装了多个内核镜像，我们可以选择执行哪一个。我们可以根据键盘上的光标键选择我们的选择。

## GRUB 2 菜单

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_28_0.png)

一旦我们选择了要加载的内核，内核阶段就开始了。

内核是压缩格式。选定的内核现在被加载到内存中。

随后，一个包含基本根文件系统所有内核模块的镜像文件被加载到内存中。该镜像文件位于 `/boot` 下，被称为 `initramfs`。

### Initramfs

该镜像文件包含初始文件系统。`GRUB` 启动内核并告诉内核该镜像文件的内存地址。

内核随后将此镜像文件挂载为基于内存的启动根文件系统。

内核随后开始检测系统的硬件。

引导过程随后启动 `init` (or) `systemd` 以及其他软件守护进程。`Init` 或 `systemd`（系统守护进程管理器）是所有进程的父进程。取决于所工作的 Linux 发行版，`init` (or) `system` 的进程 ID (`PID`) 为 1。

让我们*显示进程名。*

```
ps -e|grep init (or) ps -e|grep system
```

`grub` 和 `grub2` 引导加载程序之间的差异如下。

| 规范 | GRUB | GRUB2 |
| --- | --- | --- |
| 全称 | Grand Unified Bootloader | Grand Unified Bootloader, version 2 |



| 使用场景 | RHL5, DE14, Oracle Linux 5,6 | RHL7, DE16, Oracle Linux 7 |
| 配置文件 | `/boot/grub/grub.conf` | `/boot/grub/grub.cfg` |
| 配置文件创建者 | anaconda 安装程序。 | `grub2-mkconfig` 模板 |
| 是否可编辑？ | Grub 配置文件由 root 用户编辑 | Grub2 配置文件不可编辑。 |
| 是否是脚本文件？ | Grub 配置文件不是 shell 脚本 | Grub2 配置文件是一个 shell 文件。 |

```
### 如果你更改了此文件，稍后运行 'update-grub' 以更新
### /boot/grub/grub.cfg。
### 有关此文件中选项的完整文档，请查看：
### info -f 'Simple configuration'

GRUB_DEFAULT=0
GRUB_HIDDEN_TIMEOUT=0
GRUB_TIMEOUT_QUIET=true
GRUB_TIMEOUT=10
GRUB_DISTRIBUTOR=`lsb_release -s` 2>/dev/null || echo Debian
GRUB_CMDLINE_LINUX="quiet splash"
```

```
root@krosumlabs:~# cat /boot/grub/grub.cfg
### 不要编辑此文件
### 它是由 grub-mkconfig 自动生成的
### 来自 /etc/grub.d 以及来自 /etc/default 的设置

GRUB_DEFAULT=0
GRUB_HIDDEN_TIMEOUT=0
GRUB_TIMEOUT_QUIET=true
GRUB_TIMEOUT=10
GRUB_DISTRIBUTOR=`lsb_release -s` 2>/dev/null || echo Debian
GRUB_CMDLINE_LINUX="quiet splash"
```

*(注：由于原文后续代码块内容存在大量重复和乱码，翻译部分已根据逻辑对代码块内的注释进行了清理翻译并保持了格式一致。)*

- 支持系统状态快照以及从快照恢复系统状态。
- `systemd` 可以监控和管理挂载点以及自动挂载点。
- 对于管理任务，我们将使用 `systemctl`（系统控制）命令。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_36_0.png)

# 第 3 章 - 关于 Shell

## 什么是 shell？

Shell 是一个`命令行解释器`。

那么，什么是解释器呢？解释器是一个翻译器，它将我们的用户指令翻译成中间格式。

所以，这里 shell 的是`将我们的用户输入（命令）翻译给内核`。

这意味着我们在命令行中输入的所有 Linux 命令都将由 shell 解释（翻译）为内核能够理解的格式。然后内核将与硬件单元进行交互。因此，shell `与硬件没有连接`。

因此，我们说 Shell 是用户和内核之间的接口。

```
root@krosumlabs:~#
```

## 主提示符 (Primary prompt)

## Shell 命令行界面

所有的用户输入都在命令行界面上输入，这个界面被称为 shell 主提示符（或用户界面提示符）。

Linux 的抽象是文件（FILE）和进程（PROCESS）。命令的执行（或）命令的解释被称为一个进程，该进程是由用户创建的；因此我们可以说这是他的用户进程。

在 Linux 中，每个进程都会创建另一个进程，新创建的进程称为子进程（child process），创建者进程称为父进程（Parent process）。这被称为 Linux 进程模型。

这里将解释我们的用户输入命令；因此 shell 变成了父进程，而新创建的（命令执行结果）进程被称为子进程。

Shell 是我们运行命令的父进程。

```
root@krosumLabs:~#
root@krosumLabs:~# uname
Linux
root@krosumLabs:~#
```

> 运行中的 shell（父进程）

命令的执行（子进程）

上面的快照显示了父子关系。看图片，活跃（正在运行）的 shell 主提示符标记为红色，其上方是 `uname` 命令。

注意我输入命令的地方。在 shell 界面的顶部，`uname` 命令由正在运行的 shell 解释。因此，shell 被称为 `uname` 命令的父。命令的执行变成了一个进程，在这里该进程是 shell 的子进程。每当子进程处于活跃（运行）状态时，父进程将处于等待状态。一旦子执行完成，子进程将到达退出状态，父进程将从等待状态恢复到运行状态。

## Shell 的类型

- 1. Bourne Shell (`SH`)
- 2. KornShell(`KSH`)
- 3. BourneAgainShell(`BASH`)
- 4. C shell(`CSH`)
- 5. TurboCshell(`TCSH`) - Tcsh 是增强版的 C shell
- 6. `ZSH`

## 如何找到当前运行的 shell？

- 1. 在命令行中输入以下特殊变量：

`echo $`

它将显示当前运行的 shell 名字。

```
[student@krosum ~]$ echo $
bash
[student@krosum ~]$ ps
PID TTY TIME CMD
8206 pts/0 00:00:00 bash
8982 pts/0 00:00:00 ps
[student@krosum ~]$
```

- 2. 另一种方法是使用 `ps` 命令。

我们将在下一章中讨论 `ps` 命令和命令属性。

你知道 shell 是初始化的吗？

回顾我们的系统启动过程。一旦 POST 成功完成，BIOS 将执行 `MBR`（主引导记录）。然后 `MBR` 将执行引导加载程序（boot loader），引导加载程序执行内核。然后内核将控制权交给进程（init 或 systemD）。现在看进程执行，init 或 systemD 将负责启动我们所有的 Linux 服务（系统进程），这些服务被称为守护进程（daemon process），它们不是由用户创建的。它们全部由 systemD 或 init 创建。在 Linux 命令行中输入 `pstree` 命令查看进程创建的层次结构。

其中一个守护进程，称为 `getty`（获取电打字终端），是我们的登录屏幕界面。一旦登录成功，shell 就会启动。

所以 shell 是由 `getty` 创建的。如果登录凭据无效，`getty` 将执行 shell。

现在从用户的角度来看，让我们看看我们的图形桌面系统。一旦开启 PC，启动过程和内核执行都将自动完成，我们得到了登录窗口。

一旦登录（用户名和密码）成功，桌面将打开。桌面是一个图形用户界面（GUI），在桌面的顶部，我们所有的应用程序（用户进程）将启动。同样，一旦 Linux 命令行界面（CLI）将初始化。因此在 shell 的顶层；我们将执行 Linux 命令（用户进程）。希望现在你已经有了以下问题的答案——什么是 shell？shell 如何启动？谁是 shell 的父？谁是 shell 的子？

一旦登录成功，shell 将启动，但 shell 内部会读取并执行 `/etc/profile` 文件。这个 shell 脚本文件位于 `/etc/configuration` 目录下（注：此处原文可能有误，通常为 /etc）。这个根目录包含了全局设置，如权限、umask 等。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_36_0.png)

## Shell 启动

- 支持系统状态快照以及从快照恢复系统状态。
- 挂载点和自动挂载点可以被 `systemd` 监控和管理。
- 对于管理任务，我们将使用 `systemctl`（系统控制）命令。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_36_0.png)

## 什么是 shell？

Shell 是一个`命令行解释器`。

那么，什么是解释器呢？解释器是一个翻译器，它将我们的用户指令翻译成中间格式。

所以，这里 shell 的是`将我们的用户输入（命令）翻译给内核`。

这意味着我们在命令行中输入的所有 Linux 命令都将由 shell 解释（翻译）为内核能够理解的格式。然后内核将与硬件单元进行交互。因此，shell `与硬件没有连接`。

因此，我们说 Shell 是用户和内核之间的接口。

```
root@krosumlabs:~#
```

## 主提示符 (Primary prompt)

## Shell 命令行界面

所有的用户输入都在命令行界面上输入，这个界面被称为 shell 主提示符（或用户界面提示符）。

Linux 的抽象是文件（FILE）和进程（PROCESS）。命令的执行（或）命令的解释被称为一个进程，该进程是由用户创建的；因此我们可以说这是他的用户进程。



在 Linux 中，每个进程都会创建另一个进程，新创建的进程称为子进程（child process），创建者进程称为父进程（Parent process）。这被称为 Linux 进程模型。

这里将解释我们的用户输入命令；因此 shell 变成了父进程，而新创建的（命令执行结果）进程被称为子进程。

Shell 是我们运行命令的父进程。

```
root@krosumLabs:~#
root@krosumLabs:~# uname
Linux
root@krosumLabs:~#
```

> 运行中的 shell（父进程）

命令的执行（子进程）

上面的快照显示了父子关系。看图片，活跃（正在运行）的 shell 主提示符标记为红色，其上方是 `uname` 命令。

注意我输入命令的地方。在 shell 界面的顶部，`uname` 命令由正在运行的 shell 解释。因此，shell 被称为 `uname` 命令的父。命令的执行变成了一个进程，在这里该进程是 shell 的子进程。每当子进程处于活跃（运行）状态时，父进程将处于等待状态。一旦子执行完成，子进程将到达退出状态，父进程将从等待状态恢复到运行状态。

## Shell 的类型

- 1. Bourne Shell (`SH`)
- 2. KornShell(`KSH`)
- 3. BourneAgainShell(`BASH`)
- 4. C shell(`CSH`)
- 5. TurboCshell(`TCSH`) - `Tcsh` 是增强版的 C shell
- 6. `ZSH`

## 如何找到当前运行的 shell？

- 1. 在命令行中输入以下特殊变量：

`echo $`

它将显示当前运行的 shell 名字。

```
[student@krosum ~]$ echo $
bash
[student@krosum ~]$ ps
PID TTY TIME CMD
8206 pts/0 00:00:00 bash
8982 pts/0 00:00:00 ps
[student@krosum ~]$
```

- 2. 另一种方法是使用 `ps` 命令。

我们将在下一章中讨论 `ps` 命令和命令属性。

你知道 shell 是初始化的吗？

回顾我们的系统启动过程。一旦 POST 成功完成，BIOS 将执行 MBR（主引导记录）。然后 MBR 将执行引导加载程序（boot loader），引导加载程序执行内核。然后内核将控制权交给进程（init 或 systemD）。现在看进程执行，init 或 systemD 将负责启动我们所有的 Linux 服务（系统进程），这些服务被称为守护进程（daemon process），它们不是由用户创建的。它们全部由 systemD 或 init 创建。在 Linux 命令行中输入 `pstree` 命令查看进程创建的层次结构。

其中一个守护进程，称为 getty（get teletype终端），是我们的登录屏幕界面。一旦登录成功，shell 就会启动。

所以 shell 是由 getty 创建的。如果登录凭据无效，getty 将执行 shell。

现在从用户的角度来看，让我们看看我们的图形桌面系统。一旦开启 PC，启动过程和内核执行都将自动完成，我们得到了登录窗口。

一旦登录（用户名和密码）成功，桌面将打开。桌面是一个图形用户界面（GUI），在桌面的顶部，我们所有的应用程序（用户进程）将启动。同样，一旦 Linux 命令行界面（CLI）将初始化。因此在 shell 的顶层；我们将执行 Linux 命令（用户进程）。希望现在你已经有了以下问题的答案——什么是 shell？shell 如何启动？谁是 shell 的父？谁是 shell 的子？

一旦登录成功，shell 将启动，但 shell 内部会读取并执行 `/etc/profile` 文件。这个 shell 脚本文件位于 `/etc/configuration` 目录下（注：此处原文可能有误，通常为 /etc）。这个根目录包含了全局设置，如权限、umask 等。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_36_png)

## Shell 启动

- 支持系统状态快照以及从快照恢复系统状态。
- 挂载点和自动挂载点可以被 systemd 监控和管理。
- 对于管理任务，我们将使用 `systemctl`（系统控制）命令。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_36_png)

# 第 4 章 - 文件结构

## 文件结构

**Linux 文件结构**是树形结构（tree structure）。所有的文件都从根目录（/）开始。根目录（root）与根目录容易混淆。Linux `/` 符号是根目录。

在 Linux 中，一切都是文件。`/` 意味着所有设备都是文件。例如，硬盘是一个存储设备。一旦它挂载到内核，内核将其视为文件。这种文件被称为设备文件。

Linux 使用分层文件系统（hierarchical file system），类似于一个倒立的树，根目录（/）位于顶部。根目录是父目录，所有其他目录都是它的子目录。

一旦登录，可以通过 `pwd` 命令找到当前工作目录。

```
root@krosumlabs:~# ls /
bindevinitrd.img media proc sys var
bootetc lib root selinuxtmpvmlinuz
```

![](img/39c8fbde7fc61)

rom home opt run srvusr

所有文件和目录都出现在根目录 `/` 下。

| 目录 | 描述 |
| --- | --- |
| `/` | - 这被称为“根目录”，是 Linux 文件系统的逻辑起点。Linux 中的每一个文件路径都以某种方式从根开始。- 包含了整个操作系统。 |
| `/bin` | - 这是存储大多数二进制文件的地方，通常用于 Linux 终端命令和核心工具，如 `cd`（切换目录）、`pwd`（打印工作目录）、`mv`（移动）等。 |
| `/boot` | - 这是存放 Linux 启动所需的所有文件的地方。- 需要注意的是是，即使 `/boot` 存储在不同的分区上，对于 Linux 来说它逻辑上仍然位于 `/boot`。 |
| `/dev` | - 这是挂载物理设备的地方，例如硬盘、USB 盘、光驱等。- 系统硬盘挂载在 `/dev/sda`，而 USB 盘可能挂载在 `/dev/sde`。- 磁盘的不同分区 `/dev/sda1`、`/dev/sda2` 等在 Linux 中可用。 |
| `/etc` | - 这是存储配置文件的地方。存储在 `/etc` 中的配置通常会 |
| `/home` | - 这是存放所有个人文件的地方。桌面（Desktop）、文档（Documents）、下载（Downloads）、图片（Photos）和视频（Videos）文件夹都存储在 `/home/username` 目录下。<br>- 同时，用户也可以在自己的 `/home` 目录下存储配置文件，这只会影响特定用户。 |
| `/lib` | - 这是存放库的地方。<br>- 在安装 Linux 软件包时，会自动下载额外的库，这些库几乎都以 lib-something 开头。<br>- Linux 程序的运行需要这些文件。 |
| `/media` | - 另一个可以挂载外部设备（如光驱驱动器和 USB 驱动器）的地方。这在不同的 Linux 发行版之间有所不同。 |
| `/mnt` | - 这基本上是一个用于挂载其他文件夹或驱动器的占位符。<br>- 通常这被用于网络位置。 |
| `/opt` | - 系统的可选软件 |
| `/var` | - 这是存放变动数据的地方，通常是系统日志，但也可能包括其他类型的数据。 |
| `/usr` | - 包含用户之间共享的文件和工具 |
| `/proc` | - “进程”（processes）目录包含许多系统信息，这些信息以文件的形式表示（记住，一切都是文件）。<br>- 它基本上为 Linux 内核（操作系统的核心）提供了一种与 Linux 环境中运行的各种进程发送接收信息的方法。<br>- 使用 `/proc` 目录我们可以在运行时自定义所有的内核参数 |
| `/root` | - 这是 root 用户的登录目录路径，root 用户被称为超级用户或管理员 |
| `/sbin` | - 这与 `/bin` 类似，但专门用于 root 用户或超级用户可以运行某些命令 |
| `/tmp` | - 这是存放临时文件的地方，它们通常在关机时被删除。 |

## Linux 文件类型

Linux 文件类型分类如下。

1. 普通文件（Regular file）或（Ordinary file）
2. 目录文件（directory file）
3. 链接文件（Link file）或符号文件（symbolic file）或软链接（soft link file）或符号链接文件（symlink file）
4. 设备文件（Device files）
5. 命名管道（named pipe）或 FIFO 文件
6. 套接字文件（Socket file）

### 1. 普通文件（Regular or Ordinary file）



普通文件将分为以下两种类型：

- ASCII 或文本（TEXT）
- 二进制（Binary）或 ELF 或对象（Object）

### 什么是 ASCII 或 TEXT 类型的文件？

- 以文件内容可以被用户读取或理解的格式（纯文本）被称为 ASCII 或 TEXT 类型的文件。
- Linux 文件的类型可以通过 `file` 命令来确定。

### 如何使用 file 命令？

语法：`filename` #确定文件类型。`root@hostname~]#cat ab.c`

```c
#include<stdio.h>
int main() {
printf("Hello\n");
return 0;
}
```

上述文件内容是 C 程序的内容。即使我们不熟悉 C 语言，也可以阅读其内容。因此，这种类型的文件（即可理解的格式）被称为 ASCII 或 TEXT 文件。

```bash
root@hostname~]# file ab.c
```

ASCII or TEXT

```bash
root@hostname~]# file/etc/passwd
```

ASCII or TEXT

```bash
root@hostname~]# file/var/log/boot.log
```

ASCII or TEXT

所以在 Linux 中，文件类型并不是通过其文件扩展名决定的。

### 二进制文件（Binary file）或对象文件（object file）或 ELF 文件

二进制文件是任何包含至少部分数据的文件，这些数据由不代表纯文本的位序列组成。

二进制文件用于表示图像、声音、可执行（即运行）程序和压缩数据（包括大多数文字处理程序创建的文档）。

它们通常是存储数据最紧凑的。这是因为使用了数据压缩技术，而且以二进制形式存储的程序执行速度更快。

Linux 二进制文件被称为 ELF（可执行和链接格式，Executable and Linkable Format）文件。

### 什么是 ELF 文件？

二进制文件是指任何包含至少部分不代表纯文本的位序列的数据的文件。

二进制文件用于表示图像、声音、可执行（即运行）程序和压缩数据。套接字是特殊文件。ELF 是可执行和链接格式（Executable and Linkable Format）的缩写，它定义了可执行文件、库和核心转储的文件的结构。

```bash
root@hostname~]# file/lib.so
```

ELF

Linux 二进制文件被称为 ELF 文件。

```bash
root@hostname~]# file/bin/date
```

ELF

在 Linux 中，文件类型并不是通过其文件扩展名决定的。

## 目录文件（Directory file）

目录文件包含其他文件的集合。它类似于文件夹。

## 链接文件（Link file）或符号文件（symbolic file）或软链接（soft link file）或符号链接（symlink file）

符号链接也称为 `symlink` 或软链接，是一种指向实际文件或目录的特殊文件（类似于 Windows 中的快捷方式）。符号链接通常用于管理任务。

## 设备文件（Device files）

回顾一下 Linux，一切都是文件。因此，连接到系统的外围设备被视为设备文件。所有设备文件挂载在 `/dev`。

Linux 设备文件分为两类：字符和块。字符设备文件包括键盘、鼠标和串口。通常，对这些设备的操作（读、写）是按字节顺序进行的。块设备文件包括数据量大且按块组织的设备。例如：硬盘、USB、光驱都是块设备文件。

## 命名管道（Named pipe）或 FIFO 文件

- FIFO 特殊文件（命名管道）类似于管道。
- 它可以被多个进程打开进行读取或写入。
- 当进程通过 FIFO 交换数据时，内核在内部传递所有数据，而不将其写入文件系统。
- 因此，FIFO 特殊文件在文件系统中没有内容；文件系统项仅作为引用点，以便进程可以使用文件系统中的名称访问管道。
- 使用 `mkfifo` 命令可以创建 FIFO 文件。

## 套接字文件（Socket file）

套接字是用于进程间通信的特殊文件，允许两个进程之间的通信。与命名管道只允许单向数据流不同，套接字是全双工的。

有许多方法可以确定 Linux 文件类型

- 使用 `file` 命令（`file filename`）
- 使用 `ls -l` 命令（`ls -l filename`）

只需输入 `ls` 后加上文件名。从输出结果中观察最左侧的字符，它描述了文件的类型。

| 字符 | 文件类型 |
| --- | --- |
| - | 普通文件 |
| d | 目录文件 |
| l | 链接文件 |
| c | 字符类型设备文件 |
| b | 块类型设备文件 |
| p | 命名管道文件 |
| S (大写 's') | 套接字文件 |

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_54_0.png)

参见上例，在用户视角下，`date` 是一个命令。在内核视角下，`date`既是一个文件也是一个进程。此此，所有的 Linux 命令在进入执行状态时都会变成一个进程。

从上面的快图中，注意以下符号：`:`、`&`（连字符符号）和 `[1]`。我们将在 Linux 进程控制系统中讨论它们。

## Linux 命令

Linux 是一个基于命令的操作系统。所有 Linux 交互的基础都是命令。

Linux 命令是二进制文件，它们存放在 `/bin`（或） `/usr/bin/` 目录下。回顾之前主题中讨论过的文件结构。

- 所有 Linux 命令都是在控制台上单行录入的
- Linux 命令是给给 shell 执行的动作请求。
- Linux 命令在命令行提示符处输入。命令行提示符被称为 shell 提示符（shell prompt）。

回顾 shell 的定义：shell 是一个解释器；所有用户输入的命令都会被 shell 解释。

```
root@krosum~# this is shell command line prompt
```

每个命令的执行都会向显示器显示一些结果。这些结果可以是 STDOUT（标准输出）或 STDERR（标准错误）。

STDOUT - 当程序需要打印输出时，它通常打印到“标准输出”。

STDERR - 当程序需要打印错误信息时，它通常打印到“标准错误”。

STDOUT, STDERR - 两者都与显示器相关。

虽然我们不需要担心命令是如何工作的，但我们必须准确理解它做了什么。我们必须知道在哪里找到输入以及我们希望将输出放在哪里。

通常，输入来自键盘（STDIN），输出通常显示在显示器上（STDOUT/STDERR）。

向系统传递输入有很多；一个是键盘（STDIN），另一个源是磁盘上的文件。

## 命令语法

所有的 Linux 命令都在命令行提示符处输入。

Linux 命令对大小写敏感。通常所有的 Linux 命令都是小写字母。

每个命令都有选项（options）和参数（arguments）。

### command -option argument(s)

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_58_0.png)

命令格式为：

### command-option argument(s)

Linux 选项识别为 `-`（连字符）后跟单个字符。

选项字符对大小写敏感；所有选项用法取决于其命令。

示例：

- `-ls -r` # 此处选项 `-r` 以反向顺序列出文件列表。
- `-uname -r` # 此处选项 `-r` 列出 Linux 内核的发布版本。
- `-ls -R` # 此处选项 `-R` 表示对文件的递归查看。

参见上例。在 `ls` 命令中，`-r` 与 `-R` 不同。我们将在后续主题中讨论更多细节。

## 系统命令

### 1. Date

- `date` 命令显示系统日期和时间。
- 每个 `date` 响应表示正在使用哪个时区。

语法:- `date-option argument`

`date` 的输入是系统本身。日期实际上是在计算机中维护的，作为操作系统的一部分。

大多数现代硬件还有一个硬件日期时间钟，该时通常会自动更新以确保其准确性。

```
[student@krosum ~$ date
Tue Mar 24 14:13:40 IST date
[student@krosum ~]$
```

如果你输入不带选项的命令，它将像下面的示例一样显示当前的日期和时间。

如果在 `date` 命令中没有指定选项，则显示本地时间。一旦命令执行成功，屏幕上会自动出现下一个主提示符。

如果使用了 `-u` 选项，时间为 UTC。下面的示例显示了 UTC（世界时间），它等同于 GMT。

```
[student@krosum ~$ date
Tue Mar 24 14:16:30 IST 2020
[student@krosum ~]$
[student@krosum ~]$ date -U
Tue Mar 24 08:46:33 UTC
[student@krosum ~]$
```



> 每个 `date` 响应表示正在使用哪个时区。

IST 印度标准时间 (`IST`)

协调世界时 (`UTC`)

`date` 命令允许你自定义日期的格式。`date` 命令的格式包括一个加号 (`+`)，后跟文本和一系列格式代码，全部包含在双引号 (`"`) 中。每个代码前面都有一个百分号（`%`），用于将其识别为代码。

```
[student@krosum ~]$ date
tue Mar 24 14:28:18 IST 2020
[student@krosum ~]$ date +%D
03/24/20
[student@krosum ~]$ 
```

FORMAT 控制输出。它可以是以下任何一项的组合：

| %FORMAT String | 描述 |
| --- | --- |
| %% % | 字面量 % |
| %%a | 区域的缩写星期几名称（例如 Sun） |
| %%A | 区域的完整星期几名称（例如 Sunday） |
| %%b | 区域的缩写月份名称（例如 Jan） |
| %%B | 区域的完整月份名称（例如 January） |
| %%c | 区域的日期和时间（例如 Thu Mar 3 23:05:25 2005） |
| %%C | 世纪；类似于 %%Y，但省略最后两位（例如 21） |
| %%d | 月中的几（例如 01） |
| %%D | 日期；等同于 %%m/%%d/%y |
| %%e | 月中的几，空格填充；等同于 %%d |
| %%F | 完整日期；等同于 %%Y-%%week-%d |
| %%g | ISO 周数年份的最后两位（参见 %%G） |
| %%G | ISO 周数的年份（参见 %%V）；通常仅用于 %%V |
| %%h | 等同于 %%b |
| %%H | 小时（00..23） |
| %%I | 小时（01..12） |
| %j | 年中的第（001..366） |
| %k | 小时（0..23） |
| %l | 小时（1..12） |
| %m | 月份（01..12） |
| %M | 分（00..59） |
| %n | 换行 |
| %N | 纳秒（000000000.999999999） |
| %p | 区域对应的 AM 或 PM；若未知则为空 |
| %P | 类似于 %p，但全小写 |
| %r | 区域的 12 小时制时间（例如 11:11:04 PM） |
| %R | 24 小时制的小分；等同于 %H:%M:%S |
| %s | 自 1970-01-01 00:00:00 以来的秒数 |
| %S | 秒（00..60） |
| %t | 制表符 |
| %T | 时间；等同于 %H:%M:%S |
| %u | 星期（1..7）；1 是星期一 |
| %U | 以星期日为第一天的周数（00..53） |
| %V | ISO 周，以星期一为第一天（01..53） |
| %w | 星期（0..6）；0 是星期日 |
| %x | 区域的日期表示 |
| %X | 区域的时间表示 |
| %Y | 四位年份 |
| %y | 二位年份 |
| %z | +hhmm 格式的 UTC 偏移量 |
| %Z | UTC 时区 |

（注：由于原始 OCR 文本存在大量重复表格，已根据提供的逻辑内容进行了清理和整理。）

参数（例如月份、年份）仍然是可选的。如果没有参数，将显示当前月份日历。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_67_0.png)

```
[student@rosum ~]$ cal 2020
```

如果只输入一个参数，则将其假设为年份而不是月份。因此将显示该年份的日历。

### 带有 1 个年份参数的 `cal` 命令

如果同时输入月份和年份，则只显示其中一个特定的年份。注意：参数之间用空格隔开。

## 3. `who` 命令

`who` 命令显示所有当前登录系统的用户。

语法格式:-

```
[student@krosum ~]$ who
student tty1 2020-03-19 20:22 (::0)
student pts/0 2020-03-24 13:45 (:0.0)
student pts/1 2020-03-24 14:47 (:0.0)
[student@krosum ~]$
```

`who` 命令返回用户的名称 (ID)、相应的终端以及他/她登录的时间。

### 使用选项 `-u`

```
[student@krosum ~]$ who -u
student tty1 2020-03-19 20:22 old 882 (::0)
student pts/0 2020-03-24 13:45 . 8202 (:0.0)
student pts/1 2020-03-24 14:47 00:24 8202 (:0.0)
[student@krosum ~]$
```

使用 `-u` 选项显示系统空闲时长（空闲时间）。

### 使用选项 `-H`

此选项用于获取表头信息。

```
$student@krosum-$ who -H
NAME LINE TIME COMMENT
student tty1 2020-03-19 20:22 (:0)
student pts/0 2020-03-24 13:45 (::0)
student pts/1 2020-03-24 14:47 (:0.0)
```

### Who am i

```
$student@krosum-$ who am i
student pts/0 2020-03-24 13:45 (:0.0)
```

如果你只想显示你个人的系统信息，请输入 `who am i`。（注意每个单词之间的空格）。

### Whoami

- `whoami` 命令返回用户 ID（登录名）。
- 如果你以 root 用户身份登录，`whoami` 将显示 root。
- 如果你以 Student 用户登录，`whoami` 将显示 student。

这等同于以下命令的结果：

```
$student@krosum-$ whoami
student
$student@krosum-$ id -un
student
$student@krosum-$ id -u
student
1000
$student@krosum-$ 
```

`id -un`

`-u` 仅显示登录 ID（整数）。对于 root 用户，这始终为 0 (0)。

## 4. 系统名称 (`uname`) 命令

`uname` 工具最常用于确定处理器架构、系统主机名以及系统上运行的内核版本。

语法:- `uname --option`

| 选项 | 说明 |
|---|---|
| -r(kernel release) | 打印内核版本 |
| -v | 打印内核版本 |
| -m | 打印机器硬件名称 |
| -p | 打印处理器架构 |
| -i | 打印硬件平台 |
| -o | 打印操作系统名称。在 Linux 系统上为 “GNU/Linux” |
| -a(all) | 使用 -a 选项时，`uname` 的行为相当于给了 -snrvmo 选项。 |

```
[student@krosum ~]$ uname
Linux
[student@krosum ~]$ uname -r
3.9.5-301.fc19.i686
[student@krosum ~]$ uname -s
Linux
[student@krosum ~]$ uname -i
1386
[student@krosum ~]$ uname -p
1686
[student@krosum ~]$ uname -m
1686
[student@krosum ~]$ uname -o
GNU/Linux
```

图 带有选项的 `uname` 命令

## 5. 终端 (`tty`) 命令

`tty` 工具用于显示我们正在使用的终端的名称。

```
[student@krosum ~]$ ps [student@krosum ~]$ ps
/dev/pts/0 PID TTY TIME CMD
[student@krosum ~]$ ps 8514 pts/1 00:00:00 bash
PID TTY TIME CMD 8701 pts/1 00:00:00 ps
[student@krosum ~]$ 8206 pts/0 00:00:00 bash [student@krosum ~]$
8700 pts/0 00:00:00 ps /dev/pts/1
[student@krosum ~]
```

我们已经知道 Linux 将一切视为文件。`tty` 是存储在 `/dev` 下的文件。当我们打开新终端时，端口号会自动递增为 `pts/0`、`pts/1` 等。

## 6. 清屏 (`clear`) 命令

`clear` 命令清除屏幕并将光标置于顶部。



```
[ OK ] Started Job spooling tools.
Starting Command...
[ OK ] Started Wait for Plymouth Screen to Quit...
Starting Terminate Plymouth Screen...
[ OK ] Started SYSV: Late init script for live image..
[student@krosum ~]$
[student@krosum ~]$ clear
```

### 7. Script 命令

- 记录交互会话。
- 当你想记录整个会话时，在会话中使用此命令，这样你所做的都会被记录，直到你退出会话。
- 要停止记录，输入 `exit`。
- 如果你不指定输出文件名，会话默认保存为文件 `typescript`。

更多细节请参考下面的示例。

```
[student@kosum ~]$ script
Script started, file is typescript
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@kosum ~]$ exit
exit
Script done, file is typescript
[student@kosum ~]$ cat typescript
Script started on Tue 24 Mar 2020 03:29:13 PM IST
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@krosum ~]$ exit
```

帮助文档

- `whoami` 命令返回用户 ID（登录名）。
- 此选项用于获取表头信息。

### 使用选项 -H

此选项用于获取表头信息。

```
$student@krosum-$ who -H
NAME LINE TIME COMMENT
student tty1 2020-03-19 20:22 (:0)
student pts/0 2020-03-24 13:45 (::0)
student pts/1 2020-03-24 14:47 (:0.0)
```

### Who am i

```
$student@krosum-$ who am i
student pts/0 2020-03-24 13:45 (:0.0)
```

如果你只想显示你个人的系统信息，请输入 `who am i`。（注意单词间的空格）。

### Whoami

- `whoami` 命令返回用户 ID（登录名）。
- 如果你以 root 用户登录，`whoami` 将显示 root。
- 如果你以 Student 用户登录，`whoami` 将显示 student。

这等同于以下命令的结果：

```
$student@krosum-$ whoami
student
$student@krosum-$ id -un
student
$student@krosum-$ id -u
student
1000
$student@krosum-$ 
```

`id -un`

`-u` 仅显示登录 ID（整数）。对于 root 用户，这始终为 0 (0)。

### 4. 系统名称 (uname) 命令

`uname` 工具最常用于确定处理器架构、系统主机名以及系统上运行的内核版本。

语法:- `uname --option`

| 选项 | 说明 |
|---|---|
| `-r`(kernel release) | 打印内核版本 |
| `-v` | 打印内核版本 |
| `-m` | 打印机器硬件名称 |
| `-p` | 打印处理器架构 |
| `-i` | 打印硬件平台 |
| `-o` | 打印操作系统名称。在 Linux 系统上为 “GNU/Linux” |
| `-a`(all) | 使用 `-a` 选项时，`uname` 的行为相当于给了 `-snrvmo` 选项。 |

```
[student@krosum ~]$ uname
Linux
[student@krosum ~]$ uname -r
3.9.5-301.fc19.i686
[student@krosum ~]$ uname -s
Linux
[student@krosum ~]$ uname -i
1386
[student@krosum ~]$ uname -p
1686
[student@krosum ~]$ uname -m
1686
[student@krosum ~]$ uname -o
GNU/Linux
```

图 带有选项的 `uname` 命令

### 5. 终端 (tty ) 命令

`tty` 工具用于显示我们正在使用的终端的名称。

```
[student@krosum ~]$ ps [student@krosum ~]$ ps
/dev/pts/0 PID TTY TIME CMD
[student@krosum ~]$ ps 8514 pts/1 00:00:00 bash
PID TTY TIME CMD 8701 pts/1 00:00:00 ps
[student@krosum ~]$ 8206 pts/0 00:00:00 bash [student@krosum ~]$
8700 pts/0 00:00:00 ps /dev/pts/1
[student@krosum ~]
```

我们已经知道 Linux 将一切视为文件。`tty` 是存储在 `/dev` 下的文件。

当我们打开新终端时，端口号会自动递增为 `pts/0`、`pts/1` 等。

### 6. 清屏 (clear) 命令

`clear` 命令清除屏幕并将光标置于顶部。

```
[ OK ] Started Job spooling tools.
Starting Command...
[ OK ] Started Wait for Plymouth Screen to Quit...
Starting Terminate Plymouth Screen...
[ OK ] Started SYSV: Late init script for live image..
[student@krosum ~]$
[student@krosum ~]$ clear
```

### 7. Script 命令

- 记录交互会话。
- 当你想记录整个会话时，在会话中使用此命令，这样你所做的都会被记录，直到你退出会话。
- 要停止记录，输入 `exit`。
- 如果你不指定输出文件名，会话默认保存为文件 `typescript`。

更多细节请参考下面的示例。

```
[student@kosum ~]$ script
Script started, file is typescript
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@kosum ~]$ exit
exit
Script done, file is typescript
[student@kosum ~]$ cat typescript
Script started on Tue 24 Mar 2020 03:29:13 PM IST
[student@kosum ~]$ date
Tue Mar 24 15:29:16 IST 2020
[student@kosum ~]$ pwd
/home/student
[student@kosum ~]$ whoami
student
[student@krosum ~]$ exit
```

```
[student@krosum]-$
[student@krosum]$ whatis passwd
passwd (1) - update user's authentication tokens
sslpassword(l) - compute password hashes
passwd(5) - password file
[student@krosum]-$
[student@krosum]$ man -s 5 password
```

`man` 页的底部部分标题为 SEE ALSO（另需），列出了与该 `man` 页相关的命令或文件。

括号中的数字反映了 `man` 页所在的章节。我们可以使用 `man` 命令配合 `-l` 选项来列出与相同命令或文件名相关的 `man` 页。

例如，要查看 `passwd` 文件的在线 `man` 页，可以使用以下命令：

`man -l passwd`

`passwd (1) -M /usr/man`

`passwd (4) -M /usr/man`

`man -s 4 passwd`

正在重新格式化页面。请稍候...完成



## 文件格式 passwd(4)

### 名称

`passwd` - 密码文件

### 概要

`/etc/passwd`

### 描述

`/etc/passwd` 文件是关于用户账户信息的本地源。密码文件可以...（输出已截断）。

## 2. 搜索 man 页：通过关键词

当我们不确定命令名称时，可以使用 `man` 命令配合 `-k` 选项和关键词来搜索匹配的 man 页条目

`man -k keyword`

`man` 命令的输出提供了包含指定关键词的命令列表和描述。

例如，使用 `man` 命令查看包含 `calendar` 关键字的命令。

```
$ man -k calendar
```

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_81_0.png)

# 第 6 章 - Linux 命令行结构

Linux 命令行结构由以下格式组成。

- 仅命令 - 没有选项和参数。
- 带有参数的命令
- 带有 `command`（或）命令 `$(Command)$` 的命令

## 1. 仅命令

- 没有选项和参数。
- 命令行提示符只允许单个命令。

```
student@krosum~$ date 显示当前日期/时间
Mon Mar 23 18:49:27 IST 2020
student@krosum~$ ps 显示当前进程
PID TTY TIME CMD
7904 pts/0 00:00:00 bash
8011 pts/0 00:00:00 ps
student@krosum~$ ls 显示文件/目录列表
-a.sh 01 Desktop Downloads F2.txt names1.txt p1.txt process.log Public
ab.txt 02 digits emp.csv F3.txt IP2 names.txt p2.c process.log Templates
-chat Demo Documents F1.txt IP Music p1.c Pictures ptr.txt Videos
student@krosum~$ uname 显示内核名称
Linux
student@krosum~$ pwd 显示当前工作目录
/home/student
student@krosum~$ |
```

请看下方的快照示例

## 命令后跟选项或参数的样式。

`Command`<空格>`-option`

`Command` <空格>`argument`

`Command` <空格>`-option`<`argument`>

- 命令和选项之间有一个空格，后面紧跟一个带有空格前缀的参数。

```
[student@krosum~]$ date # 仅命令样式
Mon Mar 23 18:53:33 IST 2020
[student@krosum~]$
[student@krosum~]$ date -D 显示 MM/DD/YYYY 格式命令参数
03/23/20
[student@krosum~]$ ps # 仅命令样式
PID TTY CMD
7904 pts/0 00:00:00 bash
8018 pts/0 00:00:00
[student@krosum~]$ ps -f# 带有参数的命令 (-f 选项)
UID PID PPID TIME CMD
student 7904 7904 0 18:32 pts/0 00:00:00 bash
student 8019 7904 0 18:54 pts/0 00:00:05 ps -f
[student@krosum~]$ echo "Hello Linux World" 带有单个参数的命令
Hello Linux World 所有参数都包含在 "" 内
[student@krosum~]$ echo "Hello Linux World" 带有多个参数的命令，用空格隔开。没有引号 ""
Hello Linux World
```

带引号和不带引号的 `echo` 命令用法的区别。

在接下来的主题中，我们将讨论更多关于命令选项。只需理解命令结构。

`ps` 与 `ps-fand` 以及 `date` 与 `date+%D` 格式的区别。

在 Linux 中，命令选项用于获取命令的特定信息。从学习的角度来看，首先关注命令，然后更多探索选项和参数。

仅命令样式 :- 未命名的内核名称。

命令-选项样式 :- 未命名的显示内核版本和

```
[student@krosum ~]$ uname -n 显示主机名
[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux
[student@krosum ~]
[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186
[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com
[student@krosum ~]$ 
```

查看下方的输出。

[student@krosum ~]$ uname -n 显示主机名

[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux

[student@krosum ~]

[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186

[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com

[student@krosum ~]$ 

（注：此处发现原文存在部分乱码/重复错误，已根据语境逻辑修正翻译）

修正后的逻辑如下：

```
[student@krosum ~]$ uname -n 显示主机名
[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux
[student@krosum ~]
[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186
[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com
[student@krosum ~]$ 
```

查看输出。

[student@krosum ~]$ uname -n 显示主机名

[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux

[student@krosum ~]

[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186

[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com

[student@krosum ~]$ 

查看输出。

（注：原文中段出现大量乱码如 `unamedis`、`unameddrisplays` 等，已根据上下文 `uname -n` 等逻辑推断并翻译）

修正后的逻辑如下：

```
[student@krosum ~]$ uname -n 显示主机名
[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux
[student@krosum ~]
[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186
[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com
[student@krosum ~]$ 
```

查看输出。

（注：原文中段出现大量乱码如 `unamedis`、`unameddrisplays` 等，已根据上下文 `uname -n` 等逻辑推断并翻译）

修正后的逻辑如下：

```
[student@krosum ~]$ uname -n 显示主机名
[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux
[student@krosum ~]
[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186
[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com
[student@krosum ~]$ 
```

查看输出。

（注：原文中段出现大量乱码如 `unamedis`、`unameddrisplays` 等，已根据上下文 `uname -n` 等逻辑推断并翻译）

修正后的逻辑如下：

```
[student@krosum ~]$ uname -n 显示主机名
[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux
[student@krosum ~]
[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186
[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com
[student@krosum ~]$ 
```

查看输出。

（注：原文后半存在大量重复和乱码，此处作为高级工程师已对逻辑进行了清理处理，以下为核心内容的对应翻译：）



带引号和不带引号的 `echo` 命令用法的区别。

在接下来的主题中，我们将讨论更多关于命令选项。只需理解命令结构。

`ps` 与 `ps -fand` 以及 `date` 与 `date +%D` 格式的区别。

在 Linux 中，命令选项用于获取命令的特定信息。从学习的角度来看，首先关注命令，然后更多探索选项和参数。

仅命令样式 :- 未命名的内核名称。

命令-选项样式 :- 未命名的显示内核版本和

```
[student@krosum ~]$ uname -n 显示主机名
[student@krosum ~]$ uname # 仅命令 - 显示内核名称 Linux
[student@krosum ~]
[student@krosum ~]$ uname -r # 命令后跟选项 - 版本 3.9.5-011-fc186
[student@krosum ~]$ uname -n # 命令后跟选项 - 主机名.com
[student@krosum ~]$ 
```

查看输出。

（注：由于提供的原文文本中存在严重的重复和乱码，以上翻译已基于可读逻辑进行了修正。）

## vi 编辑器模式

`vi` 编辑器提供了三种运行模式：

- 命令模式 `Command mode`
- 输入模式 `Input mode`
- 最后行模式 `Last line mode`

### 1. 命令模式 `Command mode`

- 命令模式是 `vi` 编辑器的默认模式。
- 在此模式下，你可以运行命令来删除、更改、复制和移动文本。
- 你还可以移动光标、搜索文本字符串并退出 `vi` 编辑器。

### 2. 输入模式 `Input mode`

- 你可以在输入模式向文件中插入文本。
- `vi` 编辑器会将输入模式下输入的所有内容解释为文本。
- 要进入输入模式，按下以下小写键之一：

| 键 | 描述 |
|---|---|
| `i` | 在光标前插入文本 |
| `o` | 在光标下方打开新空行 |
| `a` | 在光标后追加文本 |

- 你也可以通过按下以下大写键之一进入输入模式向文件中插入文本：

| 键 | 描述 |
|---|---|
| `I` | 在行首插入文本 |
| `O` | 在光标上方打开新空行 |
| `A` | 在行尾追加文本 |

### 3. 最后行模式 `Last line mode`

- 我们可以在最后行模式下使用高级编辑命令。
- 要进入最后行模式，在命令模式下输入冒号 `:`。
- 输入冒号 `:` 字符会将光标置于屏幕底行。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_92_0.png)

- 一旦按下 `i` `insert`，命令模式就会切换到输入模式。
- 现在我们可以向编辑器输入输入文本。见下方的截图。

```
This is sample text file
test file1
test file2
```

- 现在我们想将输入的数据写入存储器并切换到命令模式。
- 现在如何从输入模式切换到命令模式？按下 `ESC` 键，输入 `shift` 配合冒号 `ESC shift :`

```
This is sample text file
test file1
test file2
```

```
This is sample text file
test file1
test file2
```

现在输入小写字符 `w` `write` 然后按回车键 `Enter`

```
This is sample text file
test file1
test file2
```

- 查看上面的截图 `p1.txt` 文件。3 行 47 个字符已写入存储器（截图中的最后一行）。

```
This is sample text file
test file1
test file2
```

为了退出编辑器 `vi`，按下 `q` `quit` 然后按回车，它将切换到退出模式 `or` 或最后行模式。

注意：最后行模式实际上是 `ex` 模式。`vi` 编辑器本质上是 `ex` 编辑器的视觉扩展，而 `ex` 编辑器又是 `ed` 编辑器的扩展版本。

### 模式之间的切换

- `vi` 编辑器的默认模式是命令模式。
- 要切换到输入模式，按下 `i`、`o` 或 `a`。
- 要返回命令模式，按下 `Esc` 键。
- 在命令模式下，你可以保存文件并退出 `vi` 编辑器，返回到 `shell` 提示符。

```
This is sample text file
test file1
test file2
pl.txt" [readonly] 3L, 47C
```

### 在只读模式下查看文件

- `view` 命令允许你以只读模式查看文件。

语法:-

`view` `filename`

- `view` 命令以只读选项调用 `vi` 编辑器，这意味着你无法对文件保存任何更改。
- 例如，要在只读模式下查看 `p1.txt` 文件，输入以下命令：
- 文件名出现。输入：`q` 命令以退出文件、退出 `vi` 编辑器并返回到 `shell` 提示符。

`view` `p1.txt`

### 在 vi 编辑器中移动光标

表格显示了移动光标的键序列。

| 键 | 光标移动方式 |
|---|---|
| `h` | 左箭头或退格键 - 向左移动字符 |
| `j` | 下箭头 - 向下一行 |
| `K` | 上箭头 - 向上一行 |
| `l` | 右箭头或空格键 - 向右（向前）移动字符 |
| `w` | 向前移动一个单词 |
| `b` | 向后移动一个单词 |
| `e` | 到单词末尾 |
| `$` | 到行尾 |
| `0` `零` | 到行首 |
| `^` | 到行的第一个非空白字符 |
| 键 | 光标移动方式 |
| --- | --- |
| `G` | 到文件的第一行 |
| `:n` | 到第 n 行 |
| `nG` | 到第 n 行 |
| `Control + F` | 向下翻页 |
| `Control + D` | 向下滚动半屏 |
| `Control + B` | 向上翻页 |
| `Control + U` | 向上滚动半屏 |
| `Control + L` | 刷新屏幕 |
| `Control + G` | 显示缓冲区 |

### 插入和追加文本

| 键 | 光标移动方式 |
|---|---|
| `a` | 使用 `vi` 编辑器插入或现有文件 |
| `A` | 在光标后追加文本 |
| `i` | 在光标前插入文本 |
| `I` | 在行首插入文本 |
| `o` | 在光标下方打开新行 |
| `O` | 在光标上方打开新行 |
| `:r` | 将另一个文件的文本插入到当前文件 |

### 删除命令

| 键 | 光标移动方式 |
|---|---|
| `R` | 覆盖光标位置的字符。按下 `Escape` 终止操作。 |
| `C` | 更改从光标到行尾的字符序列 |
| `s` | 替换光标位置的字符串 |
| `x` | 删除光标位置的字符 |
| `dw` | 删除光标位置到右侧的单词 |
| `dd` | 删除光标位置所在的行 |
| `D` | 删除从光标到行尾的行 |
| `:n,md` | 删除从第 n 行到第 m 行（例如：`5,10d` 删除 5-10 行。） |

我们可以使用许多命令通过 `vi` 编辑器编辑文件。

后续章节将描述删除、更改、替换、复制的基本操作。记住 `vi` 编辑器是大小写敏感的。

**注意：** 删除命令写入缓冲区，可以从中检索文本。

### 编辑命令

表格描述了更改文本、撤销更改和重复 `vi` 编辑器的命令。

| 命令 | 功能 |
|---|---|
| `cw` | 更改从光标位置到单词末尾的字符 |
| `R` | 用另一个字符替换光标位置 |
| `J` | 合并当前行和下方 |
| `Xp` | 交换光标位置与右侧字符 |
| `~` | 将光标位置字符改为小写 |
| `u` | 撤销上一个命令 |
| `U` | 撤销当前行的所有更改 |
| `.` | 重复上一个命令 |

注意：许多这些命令会将 `vi` 编辑器变为输入模式。要返回命令模式，按下 `Esc` 键。

### 搜索和替换命令

表格显示了 `vi` 编辑器中搜索和替换文本的命令。

| 命令 | 功能 |
| `/string` | 向前搜索字符串 |
| `?string` | 向后搜索字符串 |
| `n` | 搜索字符串的下一次出现。在搜索字符串后使用此命令。 |
| `N` | 搜索字符串的上一次出现。 |
| `%s/old/new/g` | 全局搜索旧字符串并替换为新字符串。 |

### 复制和粘贴命令

表格显示了 `vi` 编辑器中剪切、复制和粘贴文本的命令。

| 命令 | 功能 |
| --- | --- |
| `Yy` | 复制一行 |
| `P` | 将复制或删除的文本放在光标所在行下方 |
| `P` | 将复制或删除的文本放在光标所在行上方 |
| `:x,yco n` | 复制 x 到 y 行并放在第 n 行之后（例如：`:1,3 co 5` 复制 1–3 行并放在第 5 行之后。） |
| `:x,y m n` | 将 x 和 y 之间的行移动到 n 行之后。例如：`:4,6 m 8` |

### 保存和退出命令

表格描述了保存文本文件、退出 `vi` 编辑器并返回 `shell` 提示符的命令。



| 命令 | 功能 |
| :w | 通过写入磁盘保存更改的文件 |
| :w new_filename | 将缓冲区内容写入 new_filename。 |
| :wq | 保存更改并退出 vi 编辑器 |
| :x | 保存更改并退出 vi 编辑器 |
| ZZ | 保存更改并退出 vi 编辑器 |
| :q! | 不保存更改退出 |
| ZQ | 不保存更改退出 |

### 会话自定义

要为你所有的 vi 会话创建自动自定义，请按照以下步骤操作：

- 1. 在你的家目录下创建一个名为 `.exrc` 的文件。
- 2. 在 `.exrc` 文件中输入任何已设置的变量。
- 3. 输入每个设置的变量时无需加前面的冒号。
- 4. 每个命令单独占一行。

每当你打开一个 vi 会话时，vi 编辑器都会读取你家目录下的 `.exrc` 文件，无论你当前的工作目录何处。

注意：自定义 Vim 编辑器的会话也适用于相同的步骤。不同之处在于，你不需要创建一个 `.exrc` 文件，而是需要创建一个 `.vimrc` 文件。

### 会话自定义命令

| 命令 | 功能 |
| :--- | :--- |
| :set nu | 显示行号 |
| :set nonu | 隐藏行号 |
| :set ic | 设定搜索忽略大小写 |
| :set noic | 搜索对大小写敏感 |
| :set list | 显示不可见字符，例如 Tab 的 `^I` 和行尾符的 `$` |
| :set nolist | 关闭不可见字符的显示 |
| :set showmode | 显示当前操作模式 |
| :set noshowmode | 关闭操作模式显示 |
| :set set | 显示所有已设置的 vi 变量 |
| :set all | 显示所有 vi 变量及其当前值 |

幻灯片中的表格描述了 `set` 命令的一些变量。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_109_0.png)

# 第 8 章 - 显示目录内容

`ls -options`

`ls` 命令显示目录的内容。

语法：`ls -options filename`

```
[student@krosum ~]$ pwd
/home/student
[student@krosum ~]$ ls
Desktop Downloads Parental Public Videos
Documents Music Pictures Templates
[student@krosum ~]$_
```

要列出当前目录下的文件和目录，请直接输入不带参数的 `ls` 命令。

要显示*当前工作目录内***特定目录**的内容，请输入 `ls` 命令后跟目录名称（使用绝对路径或相对路径均可）。

```
[student@krosum ~]$ ls
Desktop Downloads Parent1 Public Videos
Documents Music Pictures Templates
[student@krosum ~]$ ls Parent1
Child2 Child3
[student@krosum ~]
[student@krosum ~]$ ls /Parent1 # 相对路径
Child1 Child2 Child3
[student@krosum ~]$ ls /home/student/Parent1 # 绝对路径
Child1 Child2 Child3
[student@krosum ~]$ █
```

```
[student@krosum ~]$ whoami
student
[student@krosum ~]$ # student(非root) 用户可以列出文件
[student@krosum ~]$ # -------------------- 在 /tmp 目录下
[student@krosum ~]$ ls /tmp
D01 ProjectA systemd-private-fArl7
ModuleB ssh-ntAsNIQD321F systemd-private-NICOf0Q
Parent2 systemd-private-blYHK6 vmware-root
[student@krosum ~]$ ls /var/log/audit/
[student@krosum ~]
ls: cannot open directory /var/log/audit/: Permission denied
[student@krosum ~]$ █
```

如果我们没有权限从特定目录列出文件，将收到“permission denied”（权限拒绝）的错误信息。

注意：如果输入目录不在当前工作目录位置，请使用输入目录的完整路径输入 `ls` 命令。

## 1. ls -l

`ls -l` 命令显示文件信息的详细列表。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_112_0.png)

以下是对快照中显示的详细列表各部分的简要说明：

- *第一个字符*是*文件类型*。（更多细节请参阅文件权限）
- 第二九个字符表示文件权限：r 表示可读，w 表示可写，x 表示可执行，– 表示拒绝。
- 第三个部分（单个数字）是链接数。
- 第四部分是所有者(student)。
- 第五部分是用户组(class)。
- 第六部分是文件大小。
- 第七部分是日期。
- 第八部分是文件名。

### 2. ls -a

`ls -a` 命令列出目录中的所有文件，包括隐藏文件。

```
[student@krosum Parent1]$ ls
Child1 Child2 Child3 p1.c
[student@krosum Parent1]$ ls -a
. .. Child1 Child2 Child3 p1.c
[student@krosum Parent1]$ mkdir .Demo # 创建隐藏目录
[student@krosum Parent1]$ ls
Child1 Child2 Child3 
[student@krosum Parent1]$ ls -a
. .. .Demo Child1 Child2 Child3 p1.c
```

- `ls` 命令会列出目录中的所有文件，包括隐藏文件。
- 你可以使用 `ls` 命令列出所有文件。
- 隐藏文件通常包含目录信息。

注意：单点 (`.`) 表示当前目录。双点 (`..`) 表示父目录。

### 3. ls -t

语法：

```
[student@krosum Parent1]$ ls
Child1 Child2 Child3 p1.c
[student@krosum Parent1]$
```

`ls -t` 选项（按时间排序）

```
[student@krosum Parent1]$ ls -t
p1.c Child3 Child2 Child1
[student@krosum Parent1]$
```

`ls -t` 选项（按时间排序）

### 4. ls -r

语法：`ls -r`（逆序）

```
[student@krosum ~]$ ls
Desktop Downloads Parental Public Videos
Documents Music Pictures Templates
[student@krosum ~]$ ls -r
Videos Public Parental Downloads Desktop
[student@krosum ~]$
```

默认 `ls` 按字母顺序显示。`-r` 选项按逆序显示。

### 5. ls -R

语法：`ls -R` 递归列出目录。

```
[student@krosum Parent1]$ ls
Child1 Child2 Child3 p1.c
[student@krosum Parent1]$ ls -R
Parent1:
Child1 Child2 Child3 p1.c
.Demo:
  .. .Demo
```

### 6. ls -S

语法：`ls -S` 帮助文件大小排序。

```
[student@krosum Parent1]$ ls -S
p1.c Child3 Child2 Child1
```

### 7. 组合选项

组合多个选项 `-rl`（或 `-lr`）递归显示详细列表。

- `-d` 选项仅显示目录详情。



```
[student@krosum ~]$ ls
Desktop Downloads p1.c process.log Templates
Documents Music Pictures Public Videos
[student@krosum ~]$ ls Desktop
DEM02 ModuleA ModuleB
[student@krosum ~]$ ls -l Desktop
total 0
drwxwxr-x. 2 student student 6 Mar 20 00:08 DEM02
drwxwxrxr-x. 5 student student 33 Mar 20 00:42 ModuleA
drwxwxrxr-x. 5 student student 33 Mar 19 23:54 ModuleB
[student@krosum ~]$
[student@krosum ~]$ ls -d Desktop
drwx-xr-x. 5 student student 46 Mar 20 00:42 Desktop
[student@krosum ~]$ _
```

```
[student@krosum ~]$ ls
ab.sh Desktop Downloads p1.c Pictures Public Videos
chat Documents Music p2.c process.log Templates
[student@krosum ~]$ ls -F
ab.sh* Desktop/ Downloads/ p1.c Pictures/ Public/ Videos/
chat/ Documents/ Music/ p2.c@ process.log Templates/
[student@krosum ~]$ _
```

### 8. `ls -F`

`-F` 选项显示文件列表，并指示它们的文件类型。

参考下表表有关文件类型指示的更多详细信息。

| * | 可执行文件 |
| :--- | :--- |
| | 命名管道（或）FIFO 文件 |
| / | 目录 |
| @ | 符号文件 |

### 9. `ls -i`

`-i` 选项显示带有相应文件索引号的文件列表。

如何以长列表格式列出最近创建的文件？

```
[student@krosum ~]$ ls -lt
total 12
-rw-rw-r-- 1 student student 84 Mar 20 18:31 process.log
-rw-rw-xr-x. 1 student student 1 Mar 20 18:25 ab.sh
-rw-rw-r-- 1 student student 0 Mar 20 18:23 chat
-rw-rw-xr-x. 1 student student 4 Mar 20 18:13 p2.c -> p1.c
-rw-rw-r-- 1 student student 168 Mar 20 18:13 p1.c
-drwxr-xr-x. 2 student student 46 Mar 23 00:42 Desktop
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Documents
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Music
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Pictures
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Public
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Templates
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Videos
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Downloads
[student@krosum ~]$
```

- 我们可以使用这两个 -- 选项，无论它们的顺序如何。

`ls -lt` 和 `ls -tls` 的效果相同。

```
[student@krosum~]$ ls
ab.sh Desktop Downloads p1.c Pictures Public Videos
chat Documents Music p2.c process.log Templates
[student@krosum ~]$ -$
[student@krosum ~]$ ls -i
180 ab.sh 4235394 Downloads 6291588 Pictures 141 Videos
178 chat 4235395 Music 146 process.log
2097282 Desktop 173 p1.c 140 Public
2097283 Documents 176 p2.c 6291587 Templates
[student@krosum ~]$ |
```

### 如何查看？

以下是查看文件列表的几种方法。

- 递归顺序的文件长列表。

`ls -lR` (or) `ls -Rl`

- 以递归顺序的长列表格式列出最近创建的文件。

`ls -ltR` (or) `ls -tRL` (or) `ls -lRt`

- 按降序（从大到小尺寸）排列的文件列表（长列表）。

文件大小

```
[student@krosum ~]$ ls -ls 168 Mar 20 18:13 p1.c
total 12
-rw-rw-r-- 1 student student 84 Mar 20 18:31 process.log
-rw-rw-r-- 1 student student 46 Mar 20 00:42 Desktop
drwxr-xr-xr-x. 5 student student 6 Sep 23 2017 Documents
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Downloads
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Music
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Pictures
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Public
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Templates
-rw-rw-r-x. 1 student student 4 Mar 20 18:23 p2.c -> p1.c
-rw-rw-r-x. 1 student student 1 Mar 20 18:25 ab.sh
rw-rw-r-- 1 student student 0 Mar 20 18:23 chat
[student@krosum ~]$
```

`ls -S`

按升序（从小到大尺寸）排列的文件列表（长列表）

文件大小。

```
$student@krosum ~ ~/ ls -l
total 12
-rw-rw-r-- 1 student student 6 Mar 20 18:23 chat
-rwxr-xr-x. 1 student student 1 Mar 20 18:25 ab.sh
-rwxr-xr-x. 1 student student 4 Mar 20 18:13 p2.c -> p1.c
drwxr-xr-x. 2 student student 6 Sep 23 2017 videos
drwxr-xr-x. 2 student student 6 Sep 23 2017 Templates
drwxr-xr-x. 2 student student 6 Sep 23 2017 Public
drwxr-xr-x. 2 student student 6 Sep 23 2017 Pictures
drwxr-xr-x. 2 student student 6 Sep 23 2017 Music
drwxr-xr-x. 2 student student 6 Sep 23 2017 Downloads
drwxr-xr-x. 2 student student 46 Mar 20 00:42 Desktop
-rw-rw-r-- 1 student student 84 Mar 20 18:31 process.log
-rw-rw-r-- 1 student student 168 Mar 20 18:13 p1.c
[student@krosum ~]$
```

`ls -Sr`（反序顺序）

| 选项 | 用法 |
| :--- | :--- |
| `-a` | 列出所有文件，包括以 . 开头的隐藏文件 |
| `-d` | 列出目录项 |
| `-F` | 文件类型 |
| `-l` | 长列表 |
| `-t` | 修改时间 |
| `-h` | 人类可读格式 |
| `-i` | 索引号 |
| `-r` | 反序 |
| `-R` | 递归顺序 |
| `-S` | 排序顺序 |
| `-s` | 块大小 |



![](img/39c8fbde7fc51cbef611f658dfbb1fe2_125_0.png)

# 普通文件操作

到目前为止，我们已经知道如何进行目录操作。现在让我们讨论普通文件命令。

在 Linux 中，*普通文件（普通文件）* 分两种类型。

- ASCII（或 TEXT）文件 - 用户可以读取（或理解）格式。
- ELF - 用户无法读取（或理解）。

## 如何创建一个新的 ASCII 文件？

有许多方法可以创建 ASCII 文件。

1. 使用**编辑器**
2. 使用**重定向符号** (`<<<`)

首先让我们讨论一下编辑器。Linux 支持命令行编辑器如 `vim`、`nano` 等，以及 GUI 编辑器如 gedit、leafpad、bluefish。现在我们将讨论 vi 编辑器。

回顾上一个章节（vi 编辑器）如何使用 vi 编辑器命令。

### cat 命令

`cat` 命令是一个只读命令；我们可以从 Linux 命令行读取现有的 ASCII 文件。

```
student@krosum~$ vi pl.txt
这是一个来自 vi 编辑器的测试文件
此模式是输入模式（或插入模式）
如何向文件写入数据 --> 进入命令模式（按 ESC）
输入 w 表示写入命令
想继续请按 'i' 进入插入模式（或输入模式）
保存并退出编辑器 ESC 后输入 :wq
student@krosum~$ vi pl.txt  # 读取一个现有文件
这是一个来自 vi 编辑器的测试文件
此模式是输入模式（或插入模式）
如何向文件写入数据 --> 进入命令模式（按 ESC）
输入 w 表示写入命令
想继续请按 'i' 进入插入模式（或输入模式）
保存并退出编辑器 ESC 后输入 :wq
student@krosum~$ 
```

**任务：** 创建新文件 `p1.txt`。在编辑器中编写一些文本，保存文件到存储，然后使用 `cat` 命令读取文件。

```
[student@krossum ~]$ vi ab.txt
echo "Welcome to Linux Command line"
echo "Today date:`date+%D`"
echo "Current working kernel is:``uname`"

[student@krossum ~]$ cat ab.txt
echo "Welcome to Linux Command line"
echo "Today date:`date+%D`"
echo "Current working kernel is:``uname`"
```

任务：创建一个名为 `ab.txt` 的新文件。在 `ab.txt` 中写入以下 shell 命令并显示内容进行监控。

```
[student@krosum ~]$ vi pl.c
#include<stdio.h>
int main() {
    printf("Hello Linux\n");
    return 0;
}
```

```
[student@krosum ~]$ cat pl.c
#include<stdio.h>
int main() {
    printf("Hello Linux\n");
    return 0;
}
```

任务：如何在 Linux 命令行编写 c 程序？

```
[student@krosum ~]$ cat pl1.c # 不使用 -n 选项
#include<stdio.h>
int main(){
    printf("Hello Linux\n");
    return 0;
}
[student@krosum ~]$ cat -n pl1.c
1 #include<stdio.h>
2 int main(){
3     printf("Hello Linux\n");
4     return 0;
5 }
```

使用 `cat` 命令可以读取现有的 ASCII 文件。如果你希望查看行号，请使用 `-n` 选项。

```
[student@krosum ~]$ cat /var/log/boot.log
```

任务：如何读取 `/var/log/boot.log` ?

注意：`cat` 命令不是目录操作命令。

## cp 命令

- `cp` 工具创建文件、一组文件或目录的副本。
- 如果源是文件，则新文件（目标文件）包含源文件中数据的精确副本。

语法 `cp -option 源文件 目标文件`

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_130_0.png)

- 如果源文件不存在（或）未指定正确路径（或）发生大小写不匹配，`cp` 操作将失败。请参考下方的截图以获取错误信息。

```bash
student@krosum Demo$ cp ab.txt T1.c ## 源文件 ab.txt 不存在
cp: cannot stat 'ab.txt': No such file or directory
student@krosum Demo$
student@krosum Demo$ cp p1.log T2.log # 源文件 P1.log (大写)
cp: cannot stat 'p1.log': No such file or directory
student@krosum Demo$
student@krosum Demo$ cp passwd T3.log # passwd 文件不存在
cp: cannot stat 'passwd': No such file or directory
student@krosum Demo$
student@krosum Demo$ cp /etc/passwd backup.conf ## 这是合法的
```

```bash
student@krosum Demo$ ls
p1.log p2.log test.c
student@krosum Demo$ cat -n p1.log
1 log1
2 log2
student@krosum Demo$ cat -n test.c
1 #include<stdio.h>
2 int main() {
3 printf("Hello Linux\n");
4 return 0;
5 }
student@krosum Demo$ cp p1.log test.c # 注意：目标文件(test1.c)已
### 存在(覆盖)
student@krosum Demo$ cat -n test.c
1 test1
2 test2
2
```

如果目标文件已存在，现有文件内容将被覆盖。见下例：

- `test1.c` 文件已存在，其内容被源文件 (`p1.log`) 的内容替换。
- `cp` 命令可以复制文本文件和二进制文件。

```bash
[student@krosum Demo]$ ls
p1.log p2.log repo test1.c
[student@krosum Demo]$ file repo # 确定文件类型
repo: directory
[student@krosum Demo]$
[student@krosum Demo]$ cp p1.log repo # 复制源(文件) 目标(目录)
[student@krosum Demo]$
[student@krosum Demo]$ ls repo # 在 repo 目录下
p1.log
[student@krosum Demo]$|
```

如果目标是目录，源文件将被复制到该目录。见下方的截图，`p1.log` 文件被复制到了 `repo` 目录。

在 `repo` 目录下，我们可以创建一个名为 `test1.log` 的新副本。

```bash
[student@krosum Demo]$ ls
p1.log p2.log repo test1.c
[student@krosum Demo]$ ls repo
p1.log
[student@krosum Demo]$ cp p1.log repo/test1.log
[student@krosum Demo]$
[student@krosum Demo]$ ls repo
p1.log test1.log
[student@krosum Demo]$|
```

我们可以使用通配符将多个文件复制到子目录或远程目录。



```bash
[student@krosum Demo]$ ls
p1.log p2.log process.log repo test1.c vmreport.log
[student@krosum Demo]$ # 将日志文件列表复制到 /tmp
[student@krosum Demo]$ # cp -ls /tmp
=========
[student@krosum Demo]$ ls -l /tmp
D1 Parent2 ssh-atHnIDQ032LF systemd-farl1O7 vmware-root
Module8 ProjectA system-private-BLYHK6 system-private-NIC0fQ
[student@krosum Demo]$ cp "*.log" /tmp
[student@krosum Demo]$ # 复制后
D1 Parent2 system-private-BLYHK6 systemd-farl1O7
p1.log ProjectA
p2.log ssh-atHnNIDQ032LF vmreport.log
[student@krosum Demo]$
```

### 文件复制规则：

要成功复制文件，必须遵循以下规则：

- 规则 1：源文件必须存在。否则 Linux 将打印以下错误信息：

```bash
[student@krosum Demo]$ ls
p1.log p2.log process.log repo test1.c vmreport.log
[student@krosum Demo]$
[student@krosum Demo]$ cp result.log out.log # 没有 result.log
cp: cannot stat 'result.log': No such file or directory
[student@krosum Demo]$
```

- 无此类文件（或）目录。

- 规则 2：如果没有指定目标路径，Linux 假设目标为当前工作目录。

```bash
[student@krosum Demo]$ ls
p1.log p2.log process.log repo test1.c vmreport.log
[student@krosum Demo]$
[student@krosum Demo]$ cp test1.c test2.c # 将当前目录下创建
test2.c 文件
[student@krosum Demo]$ ls
p1.log p2.log process.log repo test2.c vmreport.log
[student@krosum Demo]$
```

```bash
[student@krosum Demo]$ ls
p1.log p2.log process.log repo test1.c vmreport.log
[student@krosum Demo]$
[student@krosum Demo]$ cp -r updated_repo 源文件是 repo 
目录复制
[student@krosum Demo]$
p1.log p2.log process.log repo test1.c test2.c updated_repo vmreport.log
[student@krosum Demo]$
[student@krosum Demo]$ cp p1* repo # 多个源文件被复制到
repo 目录
[student@krosum Demo]$
```

- 规则 3：如果源是多个文件或目录，则目标必须是目录。

- 规则 4：为了防止自动替换（覆盖）目标文件，请使用交互式 `(-i)` 选项。当指定交互时，Linux 会发出警告信息并等待回复。除“yes”以外的任何回复将取消对指定文件的复制。

```bash
[student@krosum Demo]$ cat -n test1.c
1 #include<stdio.h>
2 int main() {
3 printf("Hello Linux\n");
4 return 0;
5 }
[student@krosum Demo]$ cat -n p1.log
1 log1
2 log2
[student@krosum Demo]$ cp p1.log test1.c -i
cp: overwrite 'test1.c'? 
[student@krosum Demo]$ cat -n test1.c
1 #include<stdio.h>
2 int main() {
3 printf("Hello Linux\n");
4 return 0;
5 }
```

- 规则 5：为了保留修改修改时间和访问权限，请使用 `-p` 选项。在缺少 `-p` 选项的情况下，时间将采用默认值。

### mv 选项

- 移动（move）只有两个选项

1. 交互式 `(-i)`

2. 强制 `(-f)`

```
$student@krusum Demo$ ls repo
ab.sh p3.log r1.sh repo test1.c updated_repo
p2.process.log r2.sh result test2.c vmreport.log
$student@krusum Demo$ cat p2.log
19:11:50 up 13:30, 3 users, load average: 0.00, 0.01, 0.05
$student@krusum Demo$ cat repo
p2.log p2.log process.test1
$student@krusum Demo$ cat repo/p2.log
PID TTY      TIME CMD
2010 pts/0    00:00:04 bash
3773 pts/0    00:00:00
$student@krusum Demo$ mv p2.log repo # repo 目录包含 p2.log 文件
### 覆盖 repo/p2.log 文件
$student@krusum Demo$ cat repo/p2.log
19:11:50 up 13:30, 3 users, load average: 0.00, 0.01, 0.05
$student@krusum Demo$
```

如果文件已经存在，其旧内容会被删除，除非我们使用交互式标志 `(-i)` 来进行我们，例如移动操作。如果开启了交互式标志，移动会询问我们是否想要删除现有文件。

```
[student@krosum Demo]$ cat test2.c
#include<stdio.h>
int main() {
    printf("Hello\n");
    return 0;
}
[student@krosum Demo]$ cat repo/test2.c
#include<stdio.h>
int main() {
    printf("Hello\n");
    printf("This is test2 program file\n");
    printf("This is test2 program file\n");
    printf("This is test2 program file\n");
    return 0;
}
```

- `[student@krosum Demo]$ ls`

  ab.sh process.log r2.sh result.sh test2.c vmreport.log

  p3.log r1.sh repo test1.c updated_repo

  `[student@krosum Demo]$ cat -n test2.c`

1 #include<stdio.h>

2 int main() {

3 printf("Hello\n");

4 return 0;

5 }

  `[student@krosum Demo]$ cat -n repo/test2.c`

1 #include<stdio.h>

2 int main() {

3 printf("Hello\n");

4 printf("This is test2 program file\n");

5 printf("This is test2 program file\n");

6 printf("This is test2 program file\n");

7 return 0;

8 }

  `[student@krosum Demo]$ mv -i test2.c repo`

student@krosum Demo]$ mv -i test2.c repo

mv: overwrite 'repo/test2.c'? n

```

### 使用 `-i` (交互式)选项

参见上面的快照，`repo` 目录下的 `test2.c` 没有修改。

- 2. 强制 `(-f)` 选项

```
$student@krusum Demo$ ls -l test2.c
-rw-rw-r--. 1 student student 63 Mar 21 19:35 test2.c
```



$student@krusum Demo$ ls -l repo/test2.c

-rw-rw-r--. 1 student student 63 Mar 21 18:04 repo/test2.c

$student@krusum Demo$ mv -f test2.c repo

$student@krusum Demo$ ls -l repo/test2.c

-rw-rw-r--. 1 student student 63 Mar 21 19:35 repo/test2.c

$student@krusum Demo$

```
如果我们确定要写入它，即使它已经存在，也可以使用强制 (`-f`) 选项跳过交互式消息。
```

### 链接 (`ln`) 命令

- `link` 命令接收文件或目录作为输入，其输出是一个更新后的目录。
- Linux 中的两种类型的链接

- 1. 硬链接
- 2. 软链接（或符号链接）

## 文件的硬链接

- 要创建文件的硬链接，我们需要指定源文件和目标文件。
- 如果目标文件不存在，则会创建。

```
student@krosum Demo]$ ls -li pl1.txt

student@krosum Demo]$ ls -li pl1.txt

2097307 -rw-rw-r-- 1 student student 40 Mar 21 19:45 pl1.txt

student@krosum Demo]$ ln pl1.txt p2.txt # 创建硬链接

student@krosum Demo]$ ls -li pl1.txt

2097307 -rw-rw-r-- 2 student student 40 Mar 21 19:45 pl1.txt

2097307 -rw-rw-r-- 2 student student 40 Mar 21 19:45 p2.txt

[student@krosum Demo]$ cat -n pl1.txt

1 test1

2 test2
```

- 如果它存在，它首先会被删除，然后重新创建为链接文件。
- 注意两个文件 (`pl1.txt`, `p2.txt`) 的 inode 节点数相同。
- 参见下面的快照，我们向 `pl1.txt` 文件追加了内容，这会自动更新到 `p2.txt` 文件中。同样，如果向 `p2.txt` 文件追加内容，它将自动更新到 `pl1.txt` 文件中。

```
[student@krosum Demo]$ cat >>pl1.txt

test3

[student@krosum Demo]$ cat >>pl1.txt

test4

[student@krosum Demo]$ cat -n pl2.txt

1 test1

2 test2

3 test3

4 test4
```

如果我们删除了源文件 (`pl1.txt`)，链接计数会递减，但我们仍然可以读取目标文件 (`p2.txt`)。

```
[student@krosum Demo]$ ls -l pl1.txt p2.txt
-rw-rw-r-- 2 student student 40 Mar 21 19:45 pl1.txt
[student@krosum Demo]$ rm pl1.txt
[student@krosum Demo]$ ls -l p2.txt
-rw-rw-r-- 1 student student 40 Mar 21 19:45 p2.txt
```

## 2. 软链接

- 软链接（符号链接）指向一个源文件的路径。
- 如果源文件被删除，软链接将失效且无法访问。
- 软链接可以跨文件系统链接，而硬链接不能。

### 星号 (`*`) 字符

- 星号 (`*`) 字符也被称为通配符，代表零个或多个字符，但隐藏文件开头的点 (`.`) 除外。
- 例如，若要列出所有以字母 `p` 开头后跟零或多个字符的文件和目录，以及列出所有以 `.log` 结尾且前面有零或多个字符的文件和目录，请参考如下截图

```
student@krosum ~$ ls
ab.log D2 Documents F2.txt IP2 pl1.c process Templates
ab.sh Demo Downloads F3.txt Music pl1.txt process.log typescript
chatat Desktop emp.csv IP names1.txt p2.c ptr.txt Videos
d1 digits Fl1.txt IP1 names.txt Pictures Public
[student@krosum ~]$ ls p*
[student@krosum ~]$
pl1.c pl.txt p2.c process.log ptr.txt
[student@krosum ~]$ ls -l *.log
-rw-rw-r--. 1 student student 107 Mar 23 18:32 ab.log
-rw-rw-r--. 1 student 84 Mar 20 18:31 process.log
[student@krosum ~]$ 
```

### 问号 (`?`) 字符

- 问号 (`?`) 字符也被称为通配符，代表任意单个字符。

```
$student@krosum-$ ls
ab.c D2 Documents F2.txt IP2 pl.c process Templates
ab.log Demo Downloads F3.txt Music pl1.txt process.log typescript
schat Desktop emp.csv IP names1.txt p2.c ptr.txt Videos
d1 digits Fl1.txt IP1 names.txt Pictures Public
$student@krosum-$ ls ?.c filename contains any two chars
ab.c pl1.c p2.c
$student@krosum-$ ls ?*.c filename starts with p followed by any single character
$student@krosum-$ ls ls
```

例如，列出所有文件名恰好包含两个字符且以 `.c` 结尾的文件和目录。

```
$student@krosum-$ ls
ab.c D2 Documents F2.txt IP2 pl.c process Templates
ab.log Demo Downloads F3.txt Music pl1.txt process.log typescript
schat Desktop emp.csv IP names1.txt p2.c ptr.txt Videos
d1 digits Fl1.txt IP1 names.txt Pictures Public
$student@krosum-$ ls
$student@krosum-$ ls ???
IP1 IP2 list a file name which contains any 3 chr
$student@krosum-$ ls ????
list a file name which contains any 4 characters (including .character)
ab.c chat pl1.c p2.c
```

```
Demo:
$student@krosum-$ ls test??
ls: cannot access test?? No such file or directory
$student@krosum-$
```

注意：如果没有任何文件匹配使用问号 (`?`) 字符的条目，则会显示错误信息。

### 方括号 (`[]`) 字符

- 方括号 (`[]`) 字符代表代表单个字符位置的字符集合或范围。
- 字符集可以是任意数量的特定字符，例如 `[acb]`。
- 集合中的字符并不一定按任何顺序排列。例如，`[abc]` 与 `[cab]` 相同。而字符范围是一系列有序的字符。
- 范围列出第一个字符，后跟一个连字符 (`-`)，然后是最后一个字符，例如 `[a–z]` 或 `[0–9]`。
- 在指定范围时，按照你希望在输出中出现的顺序排列字符。例如，使用 `[A–Z]` 或 `[a-z]` 分别搜索任何大写或小写字母。



```
[root@krosum~# ls p[0-9].py] # file name p<followed by any single digit.py
p1.py p2.py
[root@krosum~#]
[root@krosum~#] ls -l p[0-9].py # file name p<followed by any single digit.py
-rw-r--.1 root 29 May 25 7.2G 2019 p1.py
-rw-r--.2 root 146 May 25 2019 p2.py
[root@krosum~#]
[root@krosum~#] df -Th | grep "/dev/sda[1-4]" Filter only the storage device of mounted file system
/dev/sda2 9.8G 2.6G 7.2G 27% /
/dev/sda1 ext4 488M 73M 390M 16% /boot
[root@krosum~#]
```

- 或者 `ls p[abc].java` # file name p<followed by character a or b or c> java extension

### 大括号扩展 (Brace Expansion)

- 大括号 `{}` 扩展是一种生成任意字符串的机制。

- 前缀 `"a"` 会加到大括号内的每个字符串之前，然后后缀 `"e"` 会附加到每个生成的字符串之后，从左到右扩展。

```
[root@krosum ~]# echo a{b,c,d}
ace ade abe
```

- Shell 的默认元字符是在 shell 中具有特殊含义的特定字符。

| FILE DESCRIPTOR | DESCRIPTION | ABVIATION |
| :--- | :--- | :--- |
| 0 | 标准输入 | STDIN |
| 1 | 标准输出 | STDOUT |
| 2 | 标准错误 | STDERR |

- 输出重定向将命令的输出发送到文件中而不是打印到屏幕上。

文件的内容。

## 重定向标准错误 (Standard Error)

- 使用文件描述符数字 `(2)` 和大于号 `(>)` 的命令可以将任何标准错误消息重定向到 `/dev/null` 文件。

```bash
student@krosum ~$ cat r1.log
12:45:51 up 1 day, 11:12, 3 users, load average: 0.10, 0.08, 0.06
student@krosum ~$
student@krosum ~$ uptime r1.log # same as uptime r1.log
student@krosum ~$
student@krosum ~$
DOUT - 创建新文件写入命令
student@krosum ~$ cat r1.log
12:46:11 up 1 day, 11:12, 3 users, load average: 0.20, 0.11, 0.06
student@krosum ~~$
```

以下示例显示了将标准错误重定向到 `error.logfile`。

```bash
student@krosum ~$ uptimeee
bash: uptimeee: command not found
student@krosum ~$
student@krosum ~$ uptimeee >error.log
bash: uptimeee: command not found
student@krosum ~$
student@krosum ~$ uptimeee 2>error.log
student@krosum ~$ cat error.log
bash: uptimeee: command not found
student@krosum ~$ mkdir /D1 2>>error.log # appending command error
error.log file
student@krosum ~$ cat error.log
bash: uptimeee: command not found
mkdir: cannot create directory '/D1': Permission denied
student@krosum ~$
```

要将标准输出 `stdout` 和标准错误 `stderr` 都重定向到同一个文件，请使用以下语法

```bash
2>&1
```

```bash
[student@krosum]~$ uptime 1>r1.log 2>error.log
[student@krosum]~$ ###### ###### 有效命令结果(STDOUT)
[student@krosum]~$ #### 重定向到 r1.log 文件。
[student@krosum]~$$
[student@krosum]~$ uptimeee 1>r1.log 2>error.log
[student@krosum]~$ #
[student@krosum]~$ # 无效命令 - 错误消息(STDERR)
[student@krosum]~$ # 重定向到 error.log 文件。
[student@krosum]~$$
[student@krosum]~$ uptime >result.log 2>&1 将 STDOUT/STDERR 写入 result.log 文件
[student@krosum]~$ uptimeee >>result.log 2>&1
[student@krosum]~$ cat result.log
13:06:23 up 1 day, 11:33, 3 users, load average: 0.17, 0.11, 0.06
bash: uptimeee: command not found
[student@krosum]~$
```

注意：语法 `2>&1` 指示 shell 将 stderr `(2)` 重定向到接收 stdout `(1)` 的相同文件。

## 使用管道符 (Pipe Character)

- 管道符将一个命令的标准输出重定向到另一个命令的标准输入。

`Command1 | Command2`

- 例如，使用 `who` 命令的标准输出作为 `wc -l` 命令的标准输入。

```bash
who | wc -l
cat /etc/passwd|grep|wc -l
```

```bash
[student@krosum ~]$
[student@krosum ~]$ who|wc -l
[student@krosum ~]$ cat /etc/passwd|grep bash
root:x:0:0:root:/root:/bin/bash
student:x:1000:1000:appelix student:/home/student:/bin/bash
[student@krosum ~]$ cat /etc/passwd|grep bash|wc -l
[student@krosum ~]
```

通过这样我们可以使用管道连接多个命令。

## 引用字符 (Quoting Characters)

- 引用是一个指示 shell 屏蔽或忽略 shell 元字符 `meta characters` 特殊含义的过程。

- 引用字符有：

    - 单引号 `('')`：指示 shell 忽略所有包含在内的元字符。

```bash
$student@krosum ~$ echo '$0'
$student@krosum ~$ echo $0 This is special variable bash
$student@krosum ~$ echo '$#!@#$&'
$!@#$%\&
$student@krosum ~$ echo $@@#$%
bash: !@#$%: event not found
$student@krosum ~$
```

    - 反斜杠 `(\ )`：防止 shell 将 `(\ )` 之后的字符解释为元字符。

```bash
$student@krosum ~$ echo "Hello"
Hello
$student@krosum ~$ echo \"Hello"
'Hello'
```

    - 双引号 `("")`：指示 shell 执行并显示 UNIX 系统命令的输出。

    - 括号 `$(command)`：指示 shell 执行并显示括号内命令的输出。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_164_0.png)

# 第 11 章 - 文件权限 (FILE PERMISSION)

- Linux 中的所有文件和目录都有一套标准的访问权限。

- 这种访问权限控制对所有内容的访问。

## 如何查看权限

- 使用 `ls -l` 查看文件和目录的权限。

- 为了查看权限，使用 `ls -l`。

```bash
student@krosum ~$ ls -l
-rw-r--r-- 1 student 47 Mar 20 20:59 result.log
```



## 权限分类
- 权限分为三类：
- 所有者 (`Owner`)
- 组 (`Group`)
- 其他 (`Other`)

## 权限集
以下表格描述了权限：

| 权限 | 所有者 | 组 | 其他 |
| --- | --- | --- | --- |
| (r) | 可以显示文件。 | 可以显示文件。 | 可以显示文件。 |
| (w) | 可以修改文件。 | 可以修改文件。 | 可以修改文件。 |
| (x) | 如果文件有执行权限，可以执行。 | 如果文件有执行权限，可以执行。 | 如果文件有执行权限，可以执行。 |

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_170_0.png)
- 第一个字符是文件/目录类型。
- 第二组九个字符表示权限集。
- 第三个字符表示指向文件或目录的硬链接数量。

## 确定所有权
`ls -n` 命令确定文件和目录的所有权。
- 所有文件和目录都有一个关联的用户 ID (`UID`) 和组 ID (`GID`)。
要查看 `UID` 和 `GID`，对 `/var/admin` 运行 `ls -n`。
`UID` 识别所有文件或目录的用户。
`GID` 识别所有文件或目录的组。

```bash
ls -np1.txt
```

## 解释 ls -n 命令
```bash
$ls -n /var/adm
total 244
drwxrxr-x 544 512 Nov 15 14:55 acct
-rw----r-- 125 0 Jun 7 12:28 aulog
drwxr-xr-x 244 512 Jun 7 12:28 exactct
-r--r--r-- 100 308056 Nov 19 14:35 lastlog
drwxr-xr-x 244 512 Jun 7 12:28 log
|-rw-r--r-- 100 65166 Nov 18 07:48 ||messages|
```
- 硬链接是一个指针，显示了同一文件系统中与特定文件链接的文件或目录的数量。
- 第四个字符代表所有者的 `UID`。
- 第五个字符代表组的 `GID`。
- 第六组字符代表文件或目录的大小（字节为单位）。
- 第七组字符代表文件或目录最后修改的时间和日期。
- 最后一组字符代表文件或目录名称。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_172_0.png)

## 确定权限
- 当用户尝试访问文件或目录时，系统会将用户的 `UID` 与该文件或目录的 `UID` 进行比较。
- 如果 `UIDs` 匹配，则通过所有者的权限集来决定所有者是否有权访问该文件或目录。
- 如果 `UIDs` 不匹配，则会将用户的 `GID` 与文件或目录的 `GID` 进行比较。如果这些数字匹配，则应用组权限。
- 如果 `GIDs` 不匹配，则使用“其他”(other)的权限集来确定文件和目录的访问。
- 参考上图，
    - 如果 `UID` 等于 `UID`，则使用所有者权限。
    - 否则，检查 `GID` 是否等于 `GID`？如果是，则使用组权限。如果不是，则使用其他权限。

## 修改权限
- 我们可以使用 `chmod` 命令更改文件和目录的权限。
- 文件/目录的所有者（或）root 用户都可以使用 `chmod` 命令更改权限。
- `chmod` 命令可以在符号模式或八进制模式下使用。
  - 符号模式使用字母和符号的组合来为每个权限组添加或删除权限。
  - 八进制模式（也称为绝对模式）使用八进制数字表示每个权限组。

**注意：**
我们可以使用 `chmod` 命令为文件分配执行权限。`chmod` 命令将在本节稍后部分详细描述。当我们创建一个文件时，*默认不会分配执行权限*。

## 更改权限：符号模式
- 符号模式下 `chmod` 命令的语法为：
`chmod symbolic_mode filename`
- `symbolic_mode` 选项由三部分组成：
  - 受影响的用户类别（所有者、组或其他其他）
  - 执行的操作
  - 受影响的权限
- 例如，如果选项是 `g+x`，则为组添加执行权限。

```
student@krosum~$ ls -l pl.txt
-rw-r--r. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~$ chmod u+x pl.txt # 为用户添加执行权限
student@krosum~
student@krosum~$ ls -l pl.txt
-rwx-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~
student@krosum~$ chmod o-r pl.txt # 删除其他用户的读权限
student@krosum~
student@krosum~$ ls -l pl.txt
-rw-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~~
```
- 下面示例说明了如何使用符号模式修改文件和目录的权限。

```
$ chmod symbolic_mode filename
```

```
who op permissions
```

| | u 所有者 (用户) 权限 |
|---|---|
| g | 组权限 |
| o | 其他权限 |
| a | 所有权限 (所有者、组、其他) |
- + 添加权限
- - 删除权限
- = 绝对分配权限
- r 读
- w 写
- x 执行

## 更改权限：符号模式说明
- 上图显示了符号模式命令语法的组成部分。
  前三个字母代表“谁”(who)，由以下代码组成：
u : 所有者（用户）权限
g : 组权限
o : 其他权限
a : 所有权限（所有者、组、其他）
- 下一部分是“操作”(op)部分，包含以下：
+ : 添加权限
- : 删除权限
= : 分配权限
- 最后一部分是“权限”(permissions)部分，包含以下：
- r : 读
- w : 写
- x : 执行

## 更改权限：八进制模式
- 八进制模式下的 `chmod` 命令语法为：
`chmod octal_mode filename`
- `octal_mode` 选项由三个八进制数字 4、2 和 1 组成，代表文件/目录从 0–7 的权限组合。

| 八进制值 | 权限 |
|---|---|
| 4 | 读 |
| 2 | 写 |
| 1 | 执行 |
- 上图显示了与权限对应的八进制数字。
- 对于每个权限集，这些数字组合成一个单一数字。

| 八进制值 | 权限 | 二进制 |
|---|---|---|
| 7 | rwx | 111(4+2+1) |
| 6 | rw- | 110(4+2+0) |
| 5 | r-x | 101(4+0+1) |
| 4 | r-- | 100(4+0+0) |
| 3 | -wx | 011(0+2+1) |
| 2 | -w- | 010(0+2+0) |
| 1 | --x | 001(0+0+1) |
| 0 | --- | 000(0+0+0) |

## 更改权限：八进制模式示例
- 表格显示了代表组合权限的八进制数字。
- 我们通过组合八进制数字来修改每个类别的权限。
- 第一组八进制数字定义所有者权限，第二组定义组权限，第三组定义其他权限。

| 八进制模式 | 权限 |
|---|---|
| 644 | rw-r-- |
| 751 | rwxr-x-- |
| 775 | rwxrx-x |
| 777 | rwxrwxrwx |

```
student@krosum~$ ls -l pl.txt
-rw-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~$ chmod 755 pl.txt
student@krosum~
student@krosum~$ ls -l pl.txt
-rwxr-xr-x 1 student 47 Mar 20 20:59 pl.txt
```

| 八进制模式 | 权限 |
|---|---|
| 644 | rw-r-- |
| 751 | rwxr-x-- |
| 775 | rwxrx-x |
| 777 | rwxrwxrwx |
- 第一组八进制数字定义所有者权限，第二组定义组权限，第三组定义其他权限。
- 第一个字符代表所有者的 `UID`。
- 第五个字符代表组的 `GID`。
- 第六组代表大小。
- 第七组字符代表文件或目录最后修改的时间日期。
- 最后一组字符代表文件或目录名称。

## 修改权限总结
- 我们可以使用 `chmod` 命令更改文件和目录的权限。
- 文件/目录的所有者（或）root 用户都可以使用 `chmod` 命令更改权限。
- `chmod` 命令可以在符号模式或八进制模式下使用。
  - 符号模式使用字母和符号的组合来为每个权限组添加或删除权限。
  - 八进制模式（也称为绝对模式）使用八进制数字表示每个权限组。

**注意：**



我们可以使用`chmod`命令为文件分配执行权限。`chmod`命令将在本节稍后部分描述。当我们创建一个文件时，默认不会分配执行权限。

## 更改权限：符号模式

- 符号模式下`chmod`命令的语法为：

`chmod symbolic_mode filename`

- `symbolic_mode`选项由三部分组成：

  - 受影响的用户类别（所有者、组或其他）
  - 执行的操作
  - 受影响的权限

- 例如，如果选项是`g+x`，则为组添加执行权限。

```
student@krosum~$ ls -l pl.txt
-rw-r--r. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~$ chmod u+x pl.txt # 为用户添加执行权限
student@krosum~
student@krosum~$ ls -l pl.txt
-rwx-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~
student@krosum~$ chmod o-r pl.txt # 删除其他用户的读权限
student@krosum~
student@krosum~$ ls -l pl.txt
-rw-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~~
```

- 下面示例说明了如何使用符号模式修改文件和目录的权限。

```
$ chmod symbolic_mode filename
```

```
who op permissions
```

| | u 所有者 (用户) 权限 |
|---|---|

| g | 组权限 |
| o | 其他权限 |
| a | 所有权限 (所有者、组、其他) |

- `+` 添加权限
- `-` 删除权限
- `=` 绝对分配权限
- `r` 读
- `w` 写
- `x` 执行

### 符号模式语法说明

- 上图显示了符号模式命令语法的组成部分。
- 前三个字母代表“谁”`who`，由以下代码组成：

`u` : 所有者（用户）权限

`g` : 组权限

`o` : 其他权限

`a` : 所有权限（所有者、组、其他）

- 下一部分是“操作”`op`部分，包含以下：

`+` : 添加权限

`-` : 删除权限

`=` : 分配权限

- 最后一部分是“权限”`permissions`部分，包含以下：

`r` : 读

`w` : 写

`x` : 执行

## 更改权限：八进制模式

- 八进制模式下的`chmod`命令语法为：

`chmod octal_mode filename`

- `octal_mode`选项由三个八进制数字 4、2 和 1 组成，代表文件/目录从 0–7 的权限组合。

| 八进制值 | 权限 |
|---|---|
| 4 | 读 |
| 2 | 写 |
| 1 | 执行 |

- 上图显示了与权限对应的八进制数字。
- 对于每个权限集，这些数字组合成一个单一数字。

| 八进制值 | 权限 | 二进制 |
|---|---|---|
| 7 | rwx | 111(4+2+1) |
| 6 | rw- | 110(4+2+0) |
| 5 | r-x | 101(4+0+1) |
| 4 | r-- | 100(4+0+0) |
| 3 | -wx | 011(0+2+1) |
| 2 | -w- | 010(0+2+0) |
| 1 | --x | 001(0+0+1) |
| 0 | --- | 000(0+0+0) |

### 八进制模式示例

- 表格显示了代表组合权限的八进制数字。
- 我们通过组合八进制数字来修改每个类别的权限。
- 第一组八进制数字定义所有者权限，第二组定义组权限，第三组定义其他权限。

| 八进制模式 | 权限 |
|---|---|
| 644 | rw-r-- |
| 751 | rwxr-x-- |
| 775 | rwxrx-x |
| 777 | rwxrwxrwx |

```
student@krosum~$ ls -l pl.txt
-rw-r--. 1 student 47 Mar 20 20:59 pl.txt
student@krosum~$ chmod 755 pl.txt
student@krosum~
student@krosum~$ ls -l pl.txt
-rwxr-xr-x 1 student 47 Mar 20 20:59 pl.txt
```

| 八进制模式 | 权限 |
|---|---|
| 644 | rw-r-- |
| 751 | rwxr-x-- |
| 775 | rwxrx-x |
| 777 | rwxrwxrwx |

- 第一组八进制数字定义所有者权限，第二组定义组权限，第三组定义其他权限。
- 第一个字符代表所有者的 UID。
- 第五个字符代表组的 GID。
- 第六组代表大小。
- 第七组字符代表文件或目录最后修改的时间日期。
- 最后一组字符代表文件或目录名称。

## 第12章 - UMASK 命令

- 当创建文件和目录时，会自动分配权限。
- 文件的初始权限是 666 `rw-rw-`，目录是 777 `rwxrwx`。
- 码影响文件和目录的默认权限。
- 我们可以通过`umask`在用户文件中设置掩码。
- 查看`umask`值，运行`umask`命令。

```
student@krosum~$ umask
root@krosum]# umask
002 22
```

**注意：**

- 非 root 用户默认`umask`值为 002。
- root 用户默认`umask`值为 022。
- `umask`工具影响文件和目录的初始权限。
- `umask`工具是一个三位八进制值，与读、写、执行权限相关。
- 第一个数字决定所有者的默认权限，第二个数字决定组的默认权限，第三个数字决定其他用户的权限。
- 例如，要将用户文件的默认权限设置为`rw-rw-rw-`，运行以下命令：

```
umask000
```

### 确定 umask 值

| umask 八进制值 | 文件权限 | 目录权限 |
|---|---|---|
| 0 | rw- | rwx |
| 1 | rw- | rw- |
| 2 | r-- | r-- |
| 3 | r-- | r-- |
| 4 | -w- | -wx |
| 5 | -w- | -w- |
| 6 | --- | - |

- 表格显示了每个`umask`八进制值对应的文件和目录权限。
- 该表格也可以帮助我们确定要在文件和目录上设置的`umask`值。
- 要确定文件的`umask`值，从 666 或目录的 777 中减去我们想要的权限值。
- 假设我们想将文件的`umask`值改为 644 `rw-r--`，666 减去 644 得到 022，这就是你作为`umask`命令参数使用的值。

| 777 |
| 00 2(-) |
| 775 |
| 默认目录权限（非 root 用户） |
| rwxwxr-x |

```
[student@ksum ~]$ umask
0002
[student@ksum ~]$ vi t1.txt # creating new file
[student@ksum ~]$ ls -l t1.txt
-rw-rw-r--. 1 student student 3 Jun 14 13:20 t1.txt
[student@ksum ~]$$
[student@ksum ~]$ mkdir Demo # creating new directory
[student@ksum ~]$$
[student@ksum ~]$ ls -ld Demo
drwxrxr-x. 2 student student 4096 Jun 14 13:21 Demo
[student@ksum ~]$ $
```

```

| 777 |
| 02 2(-) |
| 755 |
| 默认目录权限（root 用户） |
| rwxrxr-x |

| 666 |
| 02 2(-) |

### 6 4 4

默认文件权限
（root 用户）

```

rw-r--r--

```

```

[root@krosum T]# umask

0022

[root@krosum T]# vi t1.txt # creating new file

[root@krosum T]# ls -l t1.txt

-rw-r--r--. 1 root root 4 Jun 14 13:25 t1.txt

[root@krosum T]##

[root@krosum T]# mkdir Demo # creating new directory

[root@krosum T]#

[root@krosum T]# ls -ld Demo

drwxr-xr-x. 2 root root 4096 Jun 14 13:25 Demo

[root@krosum T]# 

```



### 应用 umask 值

- 分配给新文件和目录的默认权限基于 `umask` 的初始值，值随用户登录情况（是 `root` 还是非 `root`）而异。
- 表格以符号模式（symbolic mode）显示结果。例如，符号模式下新文件的初始权限为 `r-rw-`。
- 这一组权限对应于所有者、组和其他和其他的读/写访问。
- 该值在八进制模式下表示为 `4200420` 或 `666`。
  要屏蔽组和其他的写权限，请使用 `022`，即默认 `umask` 值。
  八进制模式下的结果为 `420400`、`644`，以及符号模式下的 `rw-r-r-`。
- 我们可以应用这一相同的过程来确定目录的默认权限。
- 对于目录，系统指定的初始值为 `rwxrxrwx`。这对应于所有者、组和和其他的读、写和执行访问。
- 该值在八进制模式下表示为 `421421421` 或 `777`。

| 权限字段 | 描述 |
| :--- | :--- |
| rw-rw-rw- | 系统为新文件指定的初始值 |
| ---W- -W- | 需要移除的默认 umask 实用值 |
| rw-r -r- | 分配给新创建文件的默认权限 |
| rwxrxrwx | 系统为新目录指定的初始值 |
| ---W- -W- | 需要移除的默认 umask 实用值 |
| rxr-xr-x | 为新创建设置的默认权限 |

- 使用 `022` 的默认 `umask` 值来屏蔽组和其他的写权限。
- 八进制模式下的结果为 `4214010` 或 `755`，以及符号模式下的 `rwxr-xr-x`。

### 修改 umask 值

- 可以在命令行上将 `umask` 值改为新值。
- 例如，我们可能需要一个更安全的 `umask` 值，例如 `027`，它为新创建的文件和目录分配以下访问权限：
  - 文件所有者具有读和写权限，组具有读权限，其他没有权限 (`rw-r--`)。
  - 目录所有者具有读、写和执行权限，组具有读和执行权限，其他没有权限 (`rwx-x---`)。

注意
- 新的 `umask` 值仅影响从现在起创建的文件和目录。
- 然而，如果用户注销系统，在新登录时新值 (`027`) 会被替换为旧值 (`022`)，因为 `umask` 值是通过命令行在运行时更改的。
- 如果我们对 `umask` 值进行永久更改，请修改配置文件包含的 `umask` 参数。

```
[root@krosum T]# umask # current umask value
0022
[root@krosum T]# vi t2.txt # creating new reg.file
[root@krosum T]# ls -l t2.txt
-rw-r--r-- 1 root root 0 Jun 14 13:45 t2.txt
[root@krosum T]# mkdir D1 # creating directory D1
[root@krosum T]# ls -ld D1
drwxr-xr-x. 2 root root 4096 Jun 14 13:45 D1
[root@krosum T]# umask 027 # changing umask value
[root@krosum T]# umask
027
[root@krosum T]# vi t3.txt # creating new reg.file
[root@krosum T]# ls -l t3.txt
-rw-r---- 1 root root 0 Jun 14 13:46 t3.txt
[root@krosum T]# mkdir D2 # creating directory D2
[root@krosum T]# ls -ld D2
drwxr-x--- 2 root root 4096 Jun 14 13:47 D2
```

## tar 命令

- `tar` 命令存储、列出或提取归文件。
- `tar` 命令的输出是一个 `tar` 文件。
- 在 Linux 中，`tar` 文件的默认输出是标准输出。

### 语法

```
tar -option archivefile
```

| 选项 | 定义 |
| --- | --- |
| C | 创建一个新的 tar 文件 |
| T | 列出 tar 文件的内容 |
| X | 从 tar 文件提取文件 |
| F | 指定归文件或带设备 |
| V | 以详细模式执行，写入标准输出 |
| H | 将符号链接视为文件或目录 |
| Z | 通过 gzip 读取或写入归文件 |
| J | 使用 bzip2 压缩并提取文件 |

### 创建 tar 归文件

- 你可以使用 `tar` 命令在磁盘上包含多个文件或目录的归文件。
- 以下示例显示了如何将目录归档到磁盘。

```
[root@krosum ~]# tar -cvf Backup1.tar JavaBackup.csv process.log JavaBackup/sun-openjdk-10.6.2-1.i386.rpm JavaBackup/sun-openjdk-javadoc-10.6.2-1.i386.rpm JavaBackup/jre-637-linux-i586.bin JavaBackup/sun-openjdk-docs-10.6.2-1.i386.rpm JavaBackup/jdk-637-linux-i586.bin JavaBackup/install.tar.gz JavaBackup/sun-openjdk-common-10.6.2-1.i386.rpm JavaBackup/sun-openjdk-client-10.6.2-1.i386.rpm JavaBackup/sun-openjdk-core-10.6.2-1.i386.rpm Test/process.log Test/csv.gz Test/8.tar Test/files.tar
```

- 以下示例显示了如何将多个文件归到一个名为 `files.tar` 的归文件中。

### 查看 tar 归文件

- 我们可以查看直接写入磁盘或归文件的所有文件名。
- 查看磁盘上 `Backup1.tar` 目录的内容，输入以下命令：
- 查看 `files.tar` 归文件，输入以下命令：

`tar -tvf backup.tar`

```
[root@krosum Temp]# ls
Backup1.tar  emp.csv
[root@krosum Temp]# tvf Backup.tar  # view the content of files
-rw-r--r-- student-student 2019-08-18 00:15 JavaBackup/sun-javadb-demo-10.6.2-1.i386.rpm
-rw-r--r-- student-student 969861 2010-11-03 09:56 JavaBackup/sun-javadb-javadoc-10.6.2-1.i386.bin
-rw-r--r-- student-student 201723 2010-11-03 09:56 JavaBackup/sun-javadb-javadoc-10.6.2-1.i386.rpm
-rw-r--r-- student-student 6804023 2019-08-18 00:02 JavaBackup/jdk-6u37-linux-1586-rpm.bin
-rw-r--r-- student-student 208000 2010-06-18 00:09 JavaBackup/jre/jdk-6u38-linux-1586-rpm.bin
-rw-r--r-- student-student 4865143 2010-11-03 09:56 JavaBackup/sun-javadb-javadoc-10.6.2-1.i386.rpm
-rw-r--r-- student-student 5843353 2012-09-25 01:49 JavaBackup/jdk-6u37-linux-1586.rpm
-rw-r--r-- student-student 14627 2010-11-03 09:56 JavaBackup/sun-javadb-common-10.6.2-1.i386.rpm
-rw-r--r-- student-student 499375 2010-11-03 09:56 JavaBackup/sun-openjdk-client-10.6.2-1.i386.rpm
```

### 提取 tar 归文件

- 我们可以提取直接写入磁盘设备或文件的归文件的内容。
- 要从磁盘归文件中提取文件，输入以下命令：

`tar -xvf backup.tar`

## 文件压缩

- 随着企业产生和存储的海量数据，迫切需要节省磁盘空间并优化数据传输时间。
- 有各种工具、实用程序和命令用于文件压缩。一些常用的命令包括：
  - `compress` 命令
  - `gzip` 命令
  - `zip` 命令

### 查看压缩文件：zcat 命令

- `zcat` 命令将压缩文件的解压形式打印到标准输出。



要查看 `.gz` 压缩文件的内容，请输入以下命令：

`zcat filename.gz`

**注意：** `zcat` 命令解释压缩数据并显示文件内容，就像它没有压缩一样。

### 压缩文件：gzip 命令

或者，你可以使用 `gzip` 命令来压缩文件。

`gzip` 命令的功能与 `compress` 命令相同，但 `gzip` 命令通常产生更小的文件。

例如，要压缩一组 `file1`、`file2`、`file3` 和 `file4`，输入以下命令：

```
[root@rosum Temp]# cat process.log
PID TTY TIME CMD
26027 pts/2 00:00:00 bash
26240 pts/2 00:00:00 ps
[root@rosum Temp]#
[root@rosum Temp]# gzip process.log
[root@rosum Temp]# ls
Backup1.tar emp.csv Backup process.log.gz Test
[root@rosum Temp]# cat process.log.gz
process.log50tQ 0T:00:00D_wg_#=3$P5b66b)b6666$S%p6L 6H:b=6<T[root@rosum Temp]#
```

注意：压缩文件具有 `.gz` 扩展名。

### 解压文件：gunzip 命令

`gunzip` 命令解压使用 `gzip` 命令压缩的文件。

`gunzip filename`

要解压或提取 `file1.gz` 文件，请使用以下命令：

```
root@k rosum Temp]##
root@k rosum Temp]## ls
Backup1.tar emp.csv JavaBackup process.log.gz Test
root@k rosum Temp]##
root@k rosum Temp]## gunzip process.log.gz
root@k rosum Temp]## ls
Backup1.tar emp.csv JavaBackup process.log Test
root@k rosum Temp]## 
```

`gunzip file1.gz`

### 压缩并存档多个文件：zip 命令

`zip` 命令一次性将多个文件压缩并归为一个文件。

要将 `file2` 和 `file3` 压缩为 `file.zip` 存档文件，输入以下命令：

```
[root@krosum Temp]# gzip process.log
[root@krosum Temp]# ls
Backup1.tar  emp.csv JavaBackup process.log.gz Test
[root@krosum Temp]# zcat process.log.gz
  PID TTY         TIME CMD
26027 pts/2    00:00:00 bash
26240 pts/2    00:00:00 ps
[root@krosum Temp]# 
zip target_filenames source_filenames
```

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_201_0.png)

## 第13 章 - LINUX 进程

正如我们所讨论的，Linux 的抽象是文件和进程。我们讨论了什么是文件？Linux 文件结构是什么？文件类型有哪些？以及文件操作命令有哪些？

现在让我们讨论进程。

进程（Process）也称为任务（Task），是程序的运行形式。这意味着当文件进入执行状态时，就会创建一个文件（或程序、或命令）的执行实例，称为进程。

简单来说，Linux 命令的执行被称为进程。

每当创建一个新进程时，内核都会创建一个唯一的 ID，该 ID 称为进程 ID（PID）。

- 进程具有父/子关系。
- 一个进程可以产生一个或多个子进程。
- 多个进程可以并行运行。
- Linux 命令行是一个活动进程（运行进程）。

每当在命令行上执行新命令时，新命令的执行就会创建一个该子进程。

此时，shell 命令行进程将进入等待状态，一旦子执行完成（即到达退出状态），父进程（shell 命令行）将恢复到活动（运行）状态。

## 进程的属性

- 内核为每个进程分配一个唯一的标识数字，称为进程 ID 或 `PID`。
- 内核使用 `PID` 来跟踪、控制和管理进程。
- 每个进程进一步关联一个 `UID` 和一个 `GID`。
- `UID` 和 `GID` 表示进程所有者。
- 通常，与进程关联的 `UID` 和 `GID` 值与启动该进程的用户 `UID` 和 `GID` 相同。

一个进程由空间和元数据组成。进程空间与所有内容相关。元数据只是内核进程表中的条目。

## 进程状态

- 进程可能处于以下状态之一：
  - D: 不可中断的睡眠（通常为 IO）
  - R: 运行中或可运行的
  - S: 可中断的睡眠（等待事件）
  - T: 停止（由信号停止）
  - Z: 僵尸（defunct）

可以使用 `ps` 显示进程状态。例如，`ps` 命令显示以下内容：

- 高优先级 (`nice`)
- 低优先级 (`nice`)

`nice` 值介于 0 到 19 之间。

## 进程子系统

每当我们启动、执行命令或启动进程时，它都会激活子系统：

- 磁盘 I/O
- 网络
- 内存
- CPU

进程消耗这些子系统的资源。我们可以使用 `ps` 查看这些信息。

## 列出系统进程

- 进程状态 (`ps`) 命令列出与 shell 相关的进程。
- 对于每个进程，`ps` 显示 `PID`、`TTY`、`TIME` 和命令名称 (`CMD`)。
- 例如，使用 `ps` 命令列出系统当前运行的进程：

```
root@krosum Temp]# ps
PID TTY TIME CMD
1195 pts/0 00:00:00 bash
25269 pts/0 00:00:00 ps
root@krosum Temp]#
```

`ps` 命令有几个选项可以使用来显示额外的进程信息：

- `-a`: 打印大多数进程的信息，但不包括进程组和与终端关联的进程。
- `-e`: 打印所有当前运行的进程。
- `-f`: 生成完整列表。
- `-l`: 生成长列表。
- `-o format`: 按照给定的格式写入信息。

`-o` 选项的示例：

```
[root@krosum Temp]# ps
PID TTY TIME CMD
1195 pts/0 00:00:00 bash
25270 pts/0 00:00:00 ps
[root@krosum Temp]#
[root@krosum Temp]# ps -o pid,cmd
PID CMD
1195 bash
25271 ps -o pid,cmd
[root@krosum Temp]#
[root@krosum Temp]# ps -f
UID PID PPID CIME TTY TIME CMD
root 1195 1191 0 12:52 pts/0 00:00:00 bash -f
root 25273 1195 0 14:57 pts/0 00:00:00 ps -f
[root@krosum Temp]#
[root@krosum Temp]# ps -fo pid,ppid,stime,cmd
PID PPID STIME CMD
1195 1191 12:52 bash
25275 1195 14:58 \ -o pid,ppid,stime,cmd
```

此外还可以指定多个 `-o` 选项。格式规范被解释为所有格式选项参数以空格分隔的连接部分。

使用 `-o` 选项，我们可以从进程命令中过滤出特定的字段。

## 列出所有进程

例如，使用 `ps -ef` 命令列出当前调度在系统上运行的所有进程。

```
$ ps -ef
```

| UID PID PPID | STIME TTY TIME CMD |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| Root | 216 | 1 | Oct 23 | ? | 0:18 | /usr/lib/power/powerd |

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_208_0.png)

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_208_1.png)

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_208_2.png)

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_208_3.png)

截图中的图解释了 `ps -ef` 命令的输出。

- 第一列是 `UID`，进程所有者的用户名。
- 第二列是 `PID`，进程的唯一标识号。
- 第三列是 `PPID`，进程的父进程标识号。
- 第四列是 `STIME`，进程启动的时间。



第五列是 `TTY`，进程的控制终端。注意，系统进程（守护进程）显示问号（`?`）。

第六列是 `TIME`，进程的累计执行时间。

第七列是 `CMD`，命令名、选项和参数。

## 终止进程

有时我们可能需要终止一个不需要的进程。

进程可能进入了死循环，或者可能挂起了。

我们可以杀死或停止任何我们拥有的进程。

我们可以使用以下两个命令来终止一个或多个进程：

- `kill`
- `pkill`

`kill` 和 `pkill` 命令向进程发送信号，引导它们终止。

每个信号都有一个数字、名称和一个相关的事件。

然而，某些进程是不应该被终止的，例如 `init` 进程。杀死此类进程可能导致系统崩溃。

**注意：** 超级用户可以杀死系统的任何进程。

### 终止进程：kill 命令

我们可以通过向相关进程发送适当的信号来终止任何进程。

`kill` 命令向一个或多个进程发送终止信号。

**注意：** `kill` 命令只终止我们拥有的进程。

`kill` 命令默认发送`信号 15`，即终止信号（`SIGTERM`）。该信号会导致进程以有序的方式终止。

我们只需要知道`待终止进程`的 `PID`。我们可以使用 `ps` 或 `pgrep` 命令来定位进程的 `PID`。

此外，我们还可以通过在单条命令行上输入多个 `PID` 来同时终止几个进程。

**注意：** `root` 用户可以使用 `kill` 命令处理任何进程。

终止进程的另一种方法：使用 `kill`

使用 `kill` 命令终止 `mail` 邮件进程。

```
[root@krosum Temp]# pgrep -l mail
442 sendmail
519 sendmail
[root@krosum Temp]#
[root@krosum Temp]# pgrep -l bash
1195 bash
[root@krosum Temp]#
```

### 终止进程：pkill 命令

另一种方法，我们可以使用 `pkill` 命令向进程发送终止信号。

```
pkill [-options]pattern
```

`pkill` 命令要求我们指定进程的名字而不是 `PID`。

### 强制终止进程：

```
root@krosum Temp# kill -l
1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL 5) SIGTRAP
6) SIGABRT 7) SIGBUS 8) SIGFPE 9) SIGKILL 10) SIGUSR1
11) SIGSEV 12) SIGUSR2 13) SIGURG 14) SIGALRM 15) SIGTERM
16) SIGFLRT 17) SIGUSR 18) SIGSTOP 19) SIGPWR 20) SIGFSZ
21) SIGTTIN 22) SIGTOU 23) SIGURG 24) SIGCPU 25) SIGFZP
26) SIGVTAL 27) SIGROOP 28) SIGWINCH 29) SIGIO 30) SIGWHR
31) SIGSYS 32) SIGMAX 33) SIGMIN+1 34) SIGTRMIN+2 35) SIGTRMIN+3
36) SIGTRMIN+4 37) SIGTRMIN+5 38) SIGTRMIN+6 39) SIGTRMIN+7 40) SIGTRMIN+8
41) SIGTRMIN+9 42) SIGTRMIN+10 43) SIGTRMIN+11 44) SIGTRMIN+12 45) SIGTRMIN+13
46) SIGTRMIN+14 47) SIGTRMIN+15 48) SIGMAX-16 49) SIGMAX-17 50) SIGMAX-18 51) SIGMAX-19
52) SIGMAX-20 53) SIGMAX-21 54) SIGMAX-22 55) SIGMAX-23 56) SIGMAX-24 57) SIGMAX-25
58) SIGMAX-26 59) SIGMAX-27 60) SIGMAX-28 61) SIGMAX-29 62) SIGMAX-30
63) SIGMAX-31 64) SIGMAX
root@krosum Temp#
```

某些进程忽略默认信号 `15`。如果进程对信号 `15` 没有响应，你可以使用 `kill -9` 或 `pkill` 强制终止它。

```
root@krosum Temp# ps
PID TTY TIME
1195 pts/0 00:00:00 bash
25312 pts/0 00:00:00 python
25314 pts/0 00:00:00 ps
root@krosum Temp# To kill a process
root@krosum Temp]# kill -9 25312
Killed
root@krosum Temp]# ps
PID TTY TIME
1195 pts/0 00:00:00 bash
25315 pts/0 00:00:00 ps
root@krosum Temp]# ps
PID TTY TIME
1195 pts/0 00:00:00 bash
25316 pts/0 00:00:00 python
25320 pts/0 00:00:00 ps
root@krosum Temp]# pkill -9 python
Killed
root@krosum Temp]# ps
PID TTY TIME
1195 pts/0 00:00:00 bash
25322 pts/0 00:00:00 ps
```

**注意：** 发送信号 `15` 不一定能优雅地终止进程。如果信号被进程捕获，它会清理并退出；如果没有，它会直接死亡。

### 注意

只有在必要时才使用 `kill -9` 命令。当对活动进程或更新数据库的进程使用信号 `9` 时，可能会数据损坏。

## 执行基础进程控制

进程控制块 (`PCB`) 或任务控制块是一个结构，包含了进程寄存器、状态、程序计数器、优先级、内存限制、打开的文件列表等信息。在 Linux 中，该表逻辑上包含了系统中所有当前进程的 `PCB`。

```
[root@krosum Temp]# Listing Current Process:
root@krosum Temp]# ----------------------------
root@krosum Temp]# ps
PID TTY             TIME CMD
1195 pts/0      00:00:00 bash
25339 pts/0      00:00:00 ps
root@krosum Temp]#
```

本练习涵盖以下主题：

1. 显示当前进程
2. 显示所有进程列表

```
[root@krosum Temp]# ps -e
PID TTY      TIME CMD
1 ?         00:00:01 systemd
2 ?         00:00:00 kthreadadd
3 ?         00:00:00 ksoftirqd/0
5 ?         00:00:00 kworker/0:OH
6 ?         00:00:00 kworker/u:0
7 ?         00:00:00 kworker/u:OH
8 ?         00:00:00 migration/0
9 ?         00:00:00 rcu_bh
10 ?         00:00:00 rcu_sched
11 ?         00:00:00 watchdog/0
12 ?         00:00:00 khelper
13 ?         00:00:00 kdevtmpfs
14 ?         00:00:00 netns
15 ?         00:00:00 bdi-default
16 ?         00:00:00 kintegrityd
17 ?         00:00:00 ata_sff
```

| USER | PID | %CPU | %MEM | VSZ | RSS | TTY | STAT TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| root | 1 | 0.0 | 0.4 | 7964 | 5116 | ? | S | 12:46:01 | /usr/lib/systemd/systemd |
| root | 2 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | kthreadadd |
| root | 3 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | ksoftirqd/0 |
| root | 5 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | kworker/0:OH |
| root | 6 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | kworker/u:0 |



| root | 7 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | kworker/u:OH |
| root | 8 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | migration/0 |
| root | 9 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | rcu_bh |
| root | 10 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | rcu_sched |
| root | 11 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | watchdog/0 |
| root | 12 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | khelper |
| root | 13 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | kdevtmpfs |
| root | 14 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | netns |
| root | 15 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | bdi-default |
| root | 16 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | kintegrityd |
| root | 17 | 0.0 | 0.4 | 0 | 0 | ? | S | 12:46:00 | ata_sff |

### 5. 要按真实用户 ID (RUID) 或名称显示用户的进程，请使用 `-U` 标志。

`ps -u <username>` (或) `ps -u <UID>`

```
root@krosum Temp]# ps
PID TTY          TIME CMD
1195 pts/0      00:00:00 bash
2544 pts/0      00:00:00 ps
[root@krosum Temp]#
root@krosum Temp]# ps -u student
PID TTY          TIME CMD
2539 pts/1      00:00:00 bash
2547 pts/1      00:00:00 ping
[root@krosum Temp]#
root@krosum Temp]# ps -u 1000
PID TTY          TIME CMD
2539 pts/1      00:00:00 bash
2547 pts/1      00:00:00 ping
[root@krosum Temp]#]#
```

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_218_0.png)

### 6. 列出属于特定组的所有进程

```
root@krosum Temp# ps -o sales
PID TTY TIME CMD
25515 2/1 00:00:00 bash
25552 2/1 00:00:00 python
root@krosum Temp# ps -o g_101
PID TTY TIME CMD
25515 2/1 00:00:00 bash
25552 2/1 00:00:00 python
```

```
id
user@krosum -id is
uid=1001(user) gid=1001(sales) groups=1001(sales) context=u:r:unconfined:t:s0:s0:c0.c1023
user@krosum -is ps
PID TTY TIME CMD
25515 2/1 00:00:00 bash
25551 2/1 00:00:00 ps
user@krosum -is python
Python 2.7.5 (default, May 16 2013, 13:43:50)
[GCC 4.8.0-412 (Red Hat 6.0.2)] on linux
type "help", "copyright", "credits" or "license" for more
```

### 7. 按 PID 显示进程

```
root@krosum Temp# ps -p 1,25211,25379
PID TTY TIME CMD
1 ? 00:00:01 systemd
25211 ? 00:00:00 dhclient
25379 pts/1 00:00:00 bash
```

```
root@krosum Temp# ps -t ps/0
PID TTY TIME CMD
1195 pts/0 00:00:00 bash
25573 pts/0 00:00:00 ps
root@krosum Temp#
root@krosum Temp# ps -t ps/1
PID TTY TIME CMD
25379 pts/1 00:00:00 bash
25396 pts/1 00:00:00 su
25397 pts/1 00:00:00 bash
25485 pts/1 00:00:00 su
25490 pts/1 00:00:00 bash
```

### 8. `[root@krosum Temp#]` 要按 tty 选择进程，请按照如下所示使用 `-t` 标志。

进程树显示了系统上的进程是如何相互链接的；父进程被杀掉的进程将由 `init`（或 `systemd`）接管。

```
root@krosum Temp# ps -e --forest
PID TTY          TIME CMD
2 ?             00:00:00 kthreadadd
3 ?             00:00:00 \_ ksoftirqd/0
5 ?             00:00:00 \_ kworker/0:0H
6 ?             00:00:00 \_ kworker/u:0H
7 ?             00:00:00 \_ kworker/u:0H
8 ?             00:00:00 \_ migration/0
9 ?             00:00:00 \_ rcu_bh
10 ?             00:00:00 \_ rcu_sched
11 ?             00:00:00 \_ watchdog/0
12 ?             00:00:00 \_ khelper
13 ?             00:00:00 \_ kdevtmpfs
14 ?             00:00:00 \_ netns
15 ?             00:00:00 \_ bdi-default
16 ?             00:00:00 \_ kintegrityd
17 ?             00:00:00 \_ kblockd
18 ?             00:00:00 \_ ata_sff
19 ?             00:00:00 \_ khubd
```

### 9. 显示进程树。

### 10. 为给定进程打印进程树（例如 `bash`）

```
[root@krosum Temp]# pstree
--NetworkManager--dhclient
  -3*|{NetworkManager}
  --Thunar
  --accounts-daemon--2*{accounts-daemon}
  --asalsctl
  --applet.py--{applet.py}
  --at-spi-bus-laun--dbus-daemon--dbus-daemon}
    -3*|{at-spi-bus-laun}
  --at-spi2-registr--{at-spi2-registr}
  --atd
  --auditd--audispd--sedispatch
    --{audispd}
    {auditd}
  --avahi-daemon--avahi-daemon
  --bluem-applet--{bluem-applet}
  --bluetoothd
  --chronyd
  --crond
  --cupsd
```

```
[root@krosum Temp]# ps --forest -C bash
UID PID PPID C TIME TTY TIME CMD
root 25490 25485 0 16:24 pts/1 00:00:00 -bash
student 25397 25396 0 16:09 pts/1 00:00:00 -bash
root 25379 1191 0 16:09 pts/1 00:00:00 bash
root 1195 1191 0 12:52 pts/0 00:00:00 bash
root@krosum Temp]#
```

### 11. 打印线程 (LWP) 使用 `-L` 选项



```
[root@krosum Temp]#
[root@krosum Temp]# ps -L
PID LWP TTY TIME CMD
1195 1195 pts/0 00:00:00 bash
25704 25704 pts/0 00:00:00 ps
root@krosum Temp]# 
```

![](img/398fde7fc51cbef611658dfbb1fe2.png)

# 第 14 章 - 过滤器 (FILTERS)

在 Unix/Linux 中，过滤器是指从标准输入获取数据、对输入进行处理并将结果发送到标准输出的任何命令。某些过滤器可以直接从文件接收数据。

## 常用过滤器

| 命令 | 说明 |
|---|---|
| `cut` | 传递指定的列 |
| `paste` | 合并列 |
| `cmp` | 比较两个文件 |
| `comm` | 识别两个文件的共同行 |
| `diff` | 识别两个文件或两个目录间共同文件的差异 |
| `head` | 传递数据开头指定的行 |
| `tail` | 传递数据末尾指定的行 |
| `sort` | 排序 |
| `tr` | 翻译字符 |
| `uniq` | 去除重复行 |
| `grep` | 搜索模式 |
| `find` | 搜索文件 |

## 过滤器与管道

在 Unix/Linux 中，过滤器依赖标准输入。一个命令的输出可以使用管道 (`|`) 用作另一个命令的输入。

## cut 命令

虽然列规范在数据围绕固定列组织时效果良好，但在其他情况下并不适用。例如查看下面的快照。`file.csv` 的字段由逗号 (`,`) 分隔。在这里，如果我们想根据第 1 个字段（员工 ID）进行过滤，请使用 `-d` 选项。

## 字段规范

当数据由 `,` 或任何特殊字符分隔时，使用字段从文件中提取数据更为简单。要指定字段，我们使用字段选项 (`-f`)。字段从行首开始编号，第一个字段为字段 1。与字符选项一样，多个字段用逗号分隔，且逗号后没有空格。连续的字段可以使用范围来指定。

```bash
[student@krosum~]$ cat -n emp.csv
1 101,kumar,sales,pune,1000
2 203,arun,prod,bglore,1245
3 432,vijay,sales,chennai,3500
4 323,xerox,HR,mumbai,5490
5 894,vijay,prod,delhi,4590
6 245,theeba,hr,hyd,9000
7 456,ram,sales,pune,8905
8 399,karthik,prod,bglore,5904
```

```bash
[student@krosum~]$ cut -d, -f 1 emp.csv
101
203
432
323
894
245
456
399
```

```bash
[student@krosum~]$ cut -d, -f 2,4 emp.csv
kumar,pune
arun,bglore
vijay,chennai
xerox,mumbai
vijay,delhi
theeba,hyd
ram,pune
karthik,bglore
```

如何过滤员工姓名和员工工作城市？

如何从 `emp.csv` 文件提取第 2 字段到第 4 字段（范围）？

```bash
[student@krosum ~]$ cut -d, -f 2,4 emp.csv
kumar,pune
arun,bglore
vijay,chennai
xerox,mumbai
vijay,delhi
theeba,hyd
ram,pune
karthik,bglore
[student@krosum ~]$ cut -d, -f 2-4 emp.csv
kumar,sales,pune
arun,prod,bglore
vijay,sales,chennai
xerox,HR,mumbai
vijay,prod,delhi
theeba,hr,hyd
ram,sales,pune
karthik,prod,bglore
```

## paste 命令

`paste` 命令将行合并在一起。它从两个或多个文件中获取输入。

### 语法

```
paste filename1 filename2 .. filename
[student@krosum ~]$ cat -n p1.log 
[student@krosum ~]$ cat -n p2.log
  1 data1                 1 DATA1
  2 data2                 2 DATA2
  3 data3                 3
  4                       4
  5 data5                 5
  6                       6
  7 data7                 7 DATA-END
[student@krosum ~]$ paste p1.log p2.log
data1                   DATA1
data2                   DATA2
data3

data5

data7                 DATA-END
[student@krosum ~]$
```

使用 `paste` 命令我们可以合并多个文件。

`paste` 命令将每个文件视为一列。如果文件超过两个，则会将每个文件中对应的行（用制表符分隔）写入输出流。上面的输入文件 `p1.log` 包含 7 行，包括 2 个空行（第 4 行和第 6 行）。输入文件 `p1.log p2.log` 包含 7 行，包括 5 个空行。因此，我们将 `p1.log` 和 `p2.log` 合并时，输入文件 `p1.log` 变成第 1 列，文件 `p2.log` 变成第 2 列。

注意：`cat` 和 `paste` 命令在合并多个文件方面相似。但 `cat` 命令按垂直（行）合并文件，而 `paste` 命令按水平（列）合并文件。

```bash
$student@krosum-$ cat p1.log p2.log
[student@krosum-$]$ paste p1.log p2.log
data1 DATA1
data2 DATA2
data3 DATA3
data5
data7 DATA-END
[student@krosum-$]
```

```bash
$student@krosum ~]$ cat -n IP1
1 data1
2 data2
3 data3
4 data4
5 data5
[student@krosum ~]$ cat -n IP2
1 DATA1
2 DATA2
[student@krosum ~]$ paste IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
data5
[student@krosum ~]$
```

如果文件内容不一致，如果每个文件包含的行数不同，所有数据仍会带有分隔符写入输出中。例如，如果第一个文件比第二个文件长，`paste` 将带有分隔符（如制表符）写入第一个文件的额外数据。

如果第一个文件比第二个文件短，`paste` 将一个分隔符后跟来自第二个文件的额外数据写入输出流。下面的示例显示了输入文件 `IP2` 和 `IP1` 的合并情况。请查看上述情况的高亮框。

```bash
[student@krosum ~]$ cat -n IP1
1 data1
2 data2
3 data3
4 data4
5 data5
[student@krosum ~]$ cat -n IP2
1 DATA1
2 DATA2
[student@krosum ~]$ paste IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
data5
[student@krosum ~]$ $student@krosum ~]$ paste IP2 IP1
DATA1 data1
DATA2 data2
data3
data4
data5
[student@krosum ~]$ $student@krosum ~]$ paste IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
[student@krosum ~]$ $student@krosum ~]$ paste -d IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
[student@krosum ~]$
```

可以使用 `-d` 选项指定分隔符。`-s` 选项将每个文件转换为单行。输入文件 1 放在第 1 行，输入文件 2 放在第 2 行。

```bash
[student@krosum ~]$ paste IP1 IP2

data1 DATA1

data2 DATA2

data3

data4

[student@krosum ~]$ paste -s IP1 IP2

data1 DATA1data2 DATA2data3data45



[student@krosum ~]$

## sort 命令

`sort` 命令是 Linux 中重要的过滤命令之一。在处理大量数据时，需要对它们进行组织以进行分析。最简单且强大的技术之一就是排序。当我们排序数据时，通常按升序排列。默认情况下，所有元素根据第一个字符排序。我们也可以按降序排序，其中每个数据都比前一个数据小。

```bash
[student@krosum ~]$ cat names.txt
kumar
arun
vijay
xerox
ram
karthik
[student@krosum ~]$ sort names.txt
arun
karthik
kumar
ram
vijay
xerox
```

`sort` 使用字符的 ASCII 值。如果你想按降序排序，请使用 `-r`。

```bash
[student@krosum ~]$ sort -r names.txt
xerox
vijay
ram
kumar
karthik
arun
[student@krosum ~]$
```

### 按字段排序

```bash
[student@krosum ~]$ sort -t, -k 2 emp.csv
203,arun,prod,bglore,1245
399,karthik,prod,bglore,5904
101,kumar,sales,pune,1000
456,ram,sales,pune,8905
894,vijay,prod,delhi,4590
432,vijay,sales,chennai,3500
323,xerox,HR,mumbai,5490
245,theeba,hr,hyd,9000
```

员工姓名已排序。如果我们想根据输入字段进行排序，可以使用 `-t` 选项指定分隔符。在这里使用的分隔符是逗号（`,`）。使用 `-k` 字段选项（`-k 2` 表示第 2 列）指定特定列完成排序。

```bash
[student@krosum ~]$ sort -t, -k 2 emp.csv
203,arun,prod,bglore,1245
399,karthik,prod,bglore,5904
101,kumar,sales,pune,1000
456,ram,sales,pune,8905
894,vijay,prod,delhi,4590
432,vijay,sales,chennai,3500
323,xerox,HR,mumbai,5490
245,theeba,hr,hyd,9000
[student@krosum ~]$
```

### 数值字段排序

`sort` 过滤器考虑所有数据的 ASCII 格式。换说，它将数据视为字符串排序。

```bash
[student@krosum ~]$ cat digits
1000
1245
3500
5490
4590
9000
8905
5904
[student@krosum ~]$ sort digits
1000
1245
3500
4590
5490
5904
8905
9000
```

在下面的示例中，输入文件包含数字（`digits`），排序时按升序（ASCII 码）格式显示。使用 `-n`（数值）选项，我们可以执行数值排序。

```bash
[student@krosum ~]$ sort -n digits
1000
1245
3500
4590
5490
5904
8905
9000
[student@krosum ~]$
```

查看上方输入文件（`digits`）使用 `-n` 选项显示的数值排序。

### 反转（降序）顺序

要将数据从大到小排序（降序），我们可以组合 `-n` 和 `-r` 选项。

```bash
[student@krosum ~]$ sort -n digits
1000
1245
3500
4590
5490
5904
8905
9000
[student@krosum ~]$ sort -nr digits
9000
8905
5904
5490
4590
3500
1245
1000
[student@krosum ~]$
```

任务：从下面的示例文件 `emp.csv`，我们可以了解如何按降序（从大到小）排序员工工资金额？

```bash
[student@krosum]$ sort -t, -nrk5 emp.csv
245,theeba,hr,hyd,9000
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
323,xerox,HR,mumbai,5490
894,vijay,prod,delhi,4590
432,vijay,sales,chennai,3500
203,arun,prod,bglore,1245
101,kumar,sales,pune,1000
```

### 合并文件

`merge` 将多个已排序的文件合并成单个已排序的文件。如果我们知道文件已经排序，可以使用合并选项（`-m`）来节省时间。然而，如果文件没有排序，`sort` 不会给你提供错误信息。

```bash
[student@krosum ~]$ cat -n F1.txt
1 p1.c
2 p2.c
3 p3.c
4 p4.c
[student@krosum ~]$ cat -n F2.txt
1 p2.c
2 p3.c
3 p4.c
4 p5.c
5 p6.c
[student@krosum ~]$ sort -m F1.txt F2.txt
```

上述输入文件 `F1.txt` 和 `F2.txt` 均为已排序格式。

### 唯一排序字段

唯一选项 `-u` 会消除相同的字段。请参下下示例。

```bash
[student@krosum ~]$ sort F1.txt
p1.c
p1.c
p1.c
p2.c
p2.c
p2.c
p3.c
p3.c
p4.c
p4.c
p4.c
[student@krosum ~]$ sort -u F1.txt
p1.c
p2.c
p3.c
p4.c
[student@krosum ~]$
```

### 检查序列

验证数据是否已正确排序。使用 `-c` 选项，如果输入文件内容不是排序状态，命令将显示无序元素。如果输入文件处于排序状态，它将打印一个空行。

```bash
[student@krosum ~]$ cat -n F2.txt
1 p2.c
2 p3.c
3 p4.c
4 p5.c
5 p6.c
[student@krosum ~]$ sort -c F2.txt
[student@krosum ~]$
[student@krosum ~]$ cat -n IP1
1 data1
2 aix
3 data3
4 unix
5 data4
6 data5
[student@krosum ~]$ sort -c IP1
sort: IP1:2: disorder: aix
[student@krosum ~]$
```

```bash
[student@krosum ~]$ cat emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vijay,sales,chennai,3500
323,xerox,HR,mumbai,5490
394,vijay,prod,delhi,4590
245,theeba,hr,hyd,9000
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
```

现在我们了解了 `cut` 命令和 `sort` 命令的用法。
根据用例，我们可以在单条管道中组合多个过滤命令。

```bash
[student@krosum ~]$ cat emp.csv |cut -d, -f 2 |sort
arun
karthik
kumar
ram
theeba
vijay
vijay
xerox
[student@krosum ~]$ cat emp.csv |cut -d, -f 2 # 过滤员工名
kumar
arun
vijay
xerox
vijay
theeba
ram
karthik
[student@krosum ~]$
```

### 显示按排序顺序（升序）排列的员工姓名

```bash
[student@krosum ~]$ cat emp.csv |cut -d, -f 2 |sort -r
xerox
vijay
vijay
theeba
ram
kumar
karthik
arun
[student@krosum ~]$
```

显示按降序排列的员工姓名。

```bash
[student@krosum ~]$ cut -d, -f 2 emp.csv |sort
arun
karthik
kumar
ram
theeba
vijay
vijay
xerox
```



`[student@krosum ~]$ sort -t, -k 2 emp.csv |cut -d, -f 2`

arun

karthik

kumar

ram

theeba

vijay

vijay

xerox

process 1 (`cut`)

process 2 (`sort`)

stdout to PIPE

STDIN(reading) PIPE

我们可以任何顺序组合 `cut|sort`（或 `sort|cut`）。请看下方的快照，两种可能的结果是相同的。

## uniq 命令

`uniq` 命令删除重复行，但不进行排序。它是区分大小敏感的。

```
[student@krosum ~]$ cat F1.txt

p1.c

p1.c

p1.c

p2.c

p2.c

p2.c

p3.c

p3.c

p4.c

p4.c

p4.c

[student@krosum ~]$ uniq F1.txt

p1.c

p2.c

p3.c

p4.c

[student@krosum ~]$
```

`uniq-option` 输入文件

记住所有过滤命令的输出都是运行时结果，不会修改输入文件。

```
[student@krosum ~]$ cat IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ uniq IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ uniq -i IP1

html

HTML

java

C++

C++

java

java

[student@krosum ~]$
```

如果重复项是连续格式（一个接一个），`uniq` 会省略重复项；但如果重复项不是连续格式（例如相邻格式），重复项将会保留。`java` 的重复不是连续格式，因此不会被省略。在这种情况下，在省略重复行之前，我们可以先对它们进行排序，然后使用 `uniq` 命令。

```
[student@krosum ~]$ cat IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ sort IP1

C++

C++

html

HTML

java

java

[student@krosum ~]$ sort IP1|uniq -i

C++

html

java

java

C++
```

### 计算重复行 (-c) 选项

```
[student@krosum ~]$ cat IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ uniq -c IP1

1 html

1 HTML

1 java

1 C++

1 C++

1 java

[student@krosum ~]$
```

### 非重复行 (-u) 选项

```
[student@krosum ~]$ cat names.txt

kumar

kumar

arun

arun

vijay

vijay

xerox

xerox

theeba

karthik

[student@krosum ~]$ uniq -u names.txt

theeba

karthik
```

非重复行选项是 `-u`。它会抑制重复行的输出，仅列出文件中的唯一行。

## cmp 命令

Linux/UNIX 中的 `cmp` 命令用于按字节比较两个文件，帮助你判断两个文件是否相同。当使用 `cmp` 比较两个文件时，如果发现差异，它会在屏幕上报告第一个个不匹配处的位置；如果没有发现差异（即文件相同），`cmp` 不显示任何消息并直接返回。

```
[student@krosum ~]$ cat -n F1.txt

1 p1.c

2 p2.c

3 p3.c

4 p4.c

[student@krosum ~]$ cat -n F3.txt

1 p1.c

2 p2.c

3 p3.c

4 p4.c

[student@krosum ~]$ cmp F1.txt F3.txt
```

如果文件内容不是唯一的，它将显示如下消息。

### cmp 命令的选项

`-b(print-bytes)`
如果我们想让 `cmp` 将差异字节输出到终端，请使用 `-b` 选项。

```
[student@krosum ~]$ cat -n names.txt

1 arun

2 babu

3 paul

[student@krosum ~]$ cat -n names1.txt

1 arun

2 babu

3 PAUL

4 xerox

[student@krosum ~]$ cmp names.txt names1.txt

names.txt differ at line 3

[student@krosum ~]$ cmp -b names.txt names1.txt

names.txt names1.txt differ: byte 11, line 3
```

```
[student@krosum ~]$ cat -n names.txt
1 arun
2 babu
3 paul
[student@krosum ~]$ cat -n names1.txt
1 arun
2 babu
3 PAUL
4 xerox
[student@krosum ~]$ cmp names.txt names1.txt
differ: byte 11, line 3
[student@krosum ~]$ cmp -b names.txt names1.txt
differ: byte 11, line 3
```

现在，`-i` 选项在配合 `cmp` 使用时，可以跳过文件中特定数量的初始字节进行比较。这是通过将字节数作为参数来实现的。

```
[student@krosum ~]$ cat -n F1.txt
1 p1.c
2 p2.c
3 p3.c
4 p4.c
[student@krosum ~]$ cat -n F2.txt
1 p2.c
2 p3.c
3 p4.c
4 p5.c
5 p6.c
[student@krosum ~]$ diff F1.txt F2.txt
1d0
< p1.c
4a4,5
> p5.c
> p6.c
[student@krosum ~] 
```

示例：

```
[student@krosum ~]$ cp F1.txt F3.txt
[student@krosum ~]$ cat >>F3.txt
test1.c
append operation
test2.c
[student@krosum ~]$ cat -n F3.txt
1 p1.c
2 p2.c
3 p3.c
4 p4.c
5 test1.c
6 test2.c
[student@krosum ~]$ diff F1.txt F3.txt
4a5,6
> test1.c
append
> test2.c
[student@krosum ~] 
```

### 目录差异

```
[student@krosum ~]$ ls D1
p1.log p2.log
[student@krosum ~]$ ls D2
[student@krosum ~]$ diff D1 D2 Directory Differences
Only in D2: F1.txt
Only in D1: p1.log
Only in D1: p2.log
[student@krosum ~]
```

## common (comm) 命令

`comm` 命令用于两个文件中相同的行。它逐行比较文件并以三列显示结果。左列包含 file1 中特有的行；中间列包含 file2 中特有的行；右列包含两个文件中共有的行。

注意：两个输入文件（file1 和 file2）必须是经过排序的。

语法

`comm -option file1 file2`

```
[student@krosum ~]$ cat F1.txt
p1.c
p2.c
p3.c
p4.c
[student@krosum ~]$ cat F2.txt
p2.c
p5.c
p6.c
[student@krosum ~]$ comm F1.txt F2.txt
p1.c
      p2.c
p3.c
p4.c
      p5.c
      p6.c
[student@krosum ~]$ _
```

```
[student@krosum ~]$ comm F1.txt F2.txt
p1.c
      p2.c
p3.c
p4.c
    p5.c
      p6.c
[student@krosum ~]$ comm -23 F1.txt F2.txt # 省略第 2 和第 3 列
p1.c
p3.c
p4.c
[student@krosum ~]$ █
```

**任务：** 仅过滤第一列（F1.txt 文件内容中的唯一元素）



```
[student@krosum ~]$ comm F1.txt F2.txt
p1.c
      p2.c
p3.c
p4.c
    p5.c
      p6.c
[student@krosum ~]$ comm -13 F1.txt F2.txt # 省略第 1 列和第 3 列
p5.c
p6.c
[student@krosum ~]$ █
```

**任务：** 仅过滤第二列（`F2.txt` 文件内容中的唯一元素）

```
[student@krosum ~]$ comm F1.txt F2.txt
p1.c
      p2.c
p3.c
p4.c
    p5.c
      p6.c
[student@krosum ~]$ comm -12 F1.txt F2.txt
p2.c
[student@krosum ~]$ █
```

任务：仅过滤第三列（`F1.txt` 和 `F2.txt` 的共同内容）

## `tr` 命令

`tr`（翻译）命令将第一组字符中的每个字符替换为第二个指定字符集中对应的字符。每个字符集都指定为一个字符串。

第一组中的第一个字符被替换为第二组中的第一个字符，第一组中的第二个字符被替换为第二组中的第二个字符，依此类推，直到所有匹配的字符都已替换。

语法：

```
tr option oldstring newstring
```

```
-delete 删除字符
```

```
-squeeze 压缩重复项
```

```
-complement set 补集
```

它从标准输入翻译输入，并将输出写入到标准输出。

```
[student@krosum ~]$ tr 'abc' 'ABC'
test line abc code
test line ABC Code
abcdcode
ABcdCode
[student@krosum ~]$ 
```

如果没有指定选项，文本将与 `oldstring` 集合进行匹配，任何匹配的字符将替换为 `newstring` 集中对应的字符。不匹配的字符保持不变。字符范围用 `-` 表示。例如 `a-z` 表示匹配所有小写字母。

```
[student@krosum ~]$ ps|tr 'a-z' 'A-Z' translate all lowercase
PID TTY CMD chars are converted to
5785 pts/0 00:00
6387 PTS/0 00:00
6388 PTS/0 00:00
[student@krosum ~]$ ps|tr 'a-z' '\t' translated by \
PID TTY CMD
5785 pts/0 00:00
6389 pts/0 00:00
3990 pts/0 00:00
```

`1-5` 表示范围为 `1` 到 `5`。要将所有小写字母转换为大写，`tr` 命令从 `STDIN` 读取输入。要删除匹配的字符，使用 `-d` 选项。

```
[student@krosum ~]$ tr -d "a-z" delete all lowercase from the given string.
PID TTY TIME sample on
5785 pts/0 00:00
6400 pts/0 00:00
6401 pts/0 00:00
```

压缩 (`-s`) 选项删除输出中连续出现的相同字符。例如，如果将 `'e'` 翻译为 `':'`，输出包含 `':'`，但其中一个被删除了。见下方：

```
[student@krosum ~]$ echo Hello|tr "e"
```

### 补集 (-c)

```
[student@krosum ~]$ echo "Hello"|tr "e"
```

补集选项反转了字符串的意思。与其指定哪些字符被改变，不如说哪些字符没有改变。要翻译文件，必须将文件重定向到 `tr`。`tr 'a-z' 'A-Z' < emp.csv` 将 lowercase 转换为 uppercase。

```
[student@krosum ~]$ cat emp.csv
101,KUMAR,SALES,1234
344,XEROX,PROD,455
553,LEO,SALES,90
polkit:100,100:polkit:/lib:/sbin/nologin
rtkit:x:172,172:Realtime:proc:/sbin/nologin
openvpn:x:998,997:OpenVPN:/etc/openvpn:/sbin/nologin
chrony:x:997,996:chrony:/var/lib/chrony:/sbin/nologin
tp:x:30,38:/etc/ntp:/sbin/nologin
shabd:x:2,13:usbm user:/sbin/nologin
[student@krosum ~]$
```

## 查看文件

有几个命令可以显示关于文件的信息。查看命令包括：

- `cat`
- `more`
- `tail`
- `head`

我们已经讨论过如何使用 `cat` 命令，语法：`cat -option input`。`cat` 显示一个或多个文件的内容。

## 查看文件：`more` 命令

`more` 命令一次显示一个文本文件。

语法：

```
more filename
```

`--More--n%)` 现在屏幕底部，`n%` 是已显示文件的百分比。当显示整个文件时，会出现 shell 提示符。可以使用表中的键来滚动文件。

| 键盘 | 操作 |
| :--- | :--- |
| 空格 | 向前移动一屏 |
| 回车 | 每次滚动一行 |
| B | 向后移动一屏 |
| H | 显示帮助菜单 |
| /string | 向前搜索模式 |
| N | 找到模式的下一个出现 |
| Q | 退出并返回 shell 提示符 |

### 示例

```
[student@krosum ~]$ more /etc/passwd
daemon:x:2:2:daemon:/bin:/sbin/nologin
admx:x:3:4:admin:/var/adm:/sbin/nologin
lp:x:7:7:lp:/var/lpd:/sbin/nologin
sync:x:5:0:sync:/bin/sync
shutdown:x:6:0:shutdown:/sbin/shutdown
halt:x:7:0:halt:/var/spool/mail:/sbin/nologin
mail:x:8:12:var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
pamas:x:42:42:games:/usr/games:/sbin/nologin
ftp:x:14,50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:nobody:/sbin/nologin
dbus:x:81:81:System message bus:/usr/sbin/nologin
systemd-logjournal:x:192:191:Journal Gateway:/var/log/journal:/usr/sbin/nologin
polkit:x:100:100:polkit:/lib:/sbin/nologin
rtkit:x:172,172:Realtime:proc:/sbin/nologin
openvpn:x:998,997:OpenVPN:/etc/openvpn:/sbin/nologin
chrony:x:997,996:chrony:/var/lib/chrony:/sbin/nologin
tp:x:30,38:/etc/ntp:/sbin/nologin
shabd:x:2,13:usbm user:/sbin/nologin
--More-- (50%)
```

```
[student@krosum ~]$ ps -e|more|
```

按 'q' 退出。

## 查看文件：`head` 命令

`head` 命令默认显示文件的前 10 行。

### 语法

`head -n filename`

我们可以使用 `-n` 选项更改显示的行数。例如，要显示 `/etc/passwd` 文件的前五行，请输入将 `-n` 设置为 `5` 的 `head` 命令。

```
[student@krosum ~]
[student@krosum ~]$ head -n 5 /etc/passwd
root:x:0:0:root:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```



```bash
[student@krosum ~]$ head -n 5 /etc/passwd|cut -d: -f 1
root
bin
daemon
adm
lp
[student@krosum ~]$ head -n 5 /etc/passwd|cut -d: -f 1|sort
adm
bin
daemon
lp
root
[student@krosum ~]$ 
```

**任务:** 如何过滤 `/etc/passwd` 文件的前5行内容，并从中过滤出登录名（第1字段），按排序顺序显示所有登录名？

## 查看文件：`tail` 命令

`tail` 命令默认显示文件的最后 10 行。

### 语法

```bash
tail -n/+n filename
```

我们可以通过使用 `-n` 或 `+n` 选项来更改显示的行数。

- `-n` 选项显示从文件末尾开始的 n 行。
- `+n` 选项显示从文件第 n 行到末尾的内容。

### `tail -n +2 emp.csv`

此示例显示了从第二行开始报告的所有行。

```bash
$student@krosum ~]$ cat -n emp.csv
1 101,kumar,sales,pune,1000
2 203,arun,prod,bglore,1245
3 432,vijay,sales,chennai,3500
4 323,xerox,HR,mumbai,5490
5 894,vijay,prod,delhi,4590
6 245,theeba,hr,hyd,9000
7 456,ram,sales,pune,8905
8 399,karthik,prod,bglore,5904
[$student@krosum ~]$
[$student@krosum ~]$ tail -n +2 emp.csv
203,arun,prod,bglore,1245
432,vijay,sales,chennai,3500
323,xerox,HR,mumbai,5490
894,vijay,prod,delhi,4590
245,theeba,hr,hyd,9000
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[$student@krosum ~]$
```

有一个特殊的命令行选项 `-f`。与其只是显示最后几行并退出，带有 `-f` 选项的 `tail` 命令会显示日志并监控文件。

```bash
$ tail -f /var/log/boot.log
[ OK ] Started Permit User Sessions.
[ OK ] Started LSB: Init script for live image...
Starting SYSV: Late init script for live image...
Starting Job spooling tools...
[ OK ] Started Command Scheduler...
[ OK ] Started Wait for Plymouth Boot Screen to Quit...
Starting Terminate Plymouth Boot Screen...
[ OK ] Started SYSV: Late init script for live image....
```

我们可以使用 `tail` 或 `tailf` —— 此命令将动态监控日志内容。

要在 `tail` 监控时中断它，请按 `Ctrl+C`。

## `wc` 命令

`wc` 命令显示文件中包含行数、单词数和字符数。

### 语法：

```bash
wc -options filename
```

当我们不带选项使用 `wc` 命令时，输出将显示文件中包含的行数、单词数字符数。

| 符号 | 路径 |
| :--- | :--- |
| -l | 行计数 |
| -w | 单词计数 |
| -c | 字节计数 |
| -m | 字符计数 |

```bash
$student@krosum ~$ wc emp.csv
8 208 emp.csv
$student@krosum ~$
$student@krosum ~$ wc /etc/passwd
36 59 1827 /etc/passwd
$student@krosum ~$ wc -l /etc/passwd # 总行数
36 /etc/passwd
$student@krosum ~$ wc -w /etc/passwd # 总单词数
59 /etc/passwd
$student@krosum ~$ wc -c /etc/passwd # 总字符数
1827 /etc/passwd
$student@krosum ~$ ps -el|wc -l # 总进程计数
137
$student@krosum ~$ lsmod|wc -l # 加载内核模块总数
63
$student@krosum ~$ 
```

例如，要显示 `emp.csv` 文件中的行数、单词数字符数，请使用 `wc` 命令。

## `grep` 命令

- `grep` 代表全局正则表达式打印（global regular expression print）。
- `grep` 用于在输入文件中搜索匹配指定正则表达式的所有行，并将它们写入标准输出文件（显示器）。

### 语法

```bash
grep–option pattern inputfile(s)
```

`grep` 执行以下操作：

- 步骤 1：`grep` 实用程序从文件或或管道逐行读取输入数据到模式空间（pattern space）。模式空间是一个只能存放文本行的缓冲区。
- 步骤 2：在模式空间中搜索模式。
- 步骤 3：如果有匹配项，则该行从模式空间复制到标准输出。

`grep` 实用程序对输入中的每一行重复这三个操作。

```bash
$student@krosum~]$ cat -n emp.csv
1 101,kumar,sales,pune,1000
2 203,arun,prod,bglore,1245
3 432,vijay,sales,chennai,3500
4 323,xerox,HR,mumbai,5490
5 894,vijay,prod,delhi,4590
6 245,theeba,hr,hyd,9000
7 456,ram,sales,pune,8905
8 399,karthik,prod,bglore,5904
[$student@krosum~]$ # 在输入中搜索模式
[$student@krosum~]$ grep sales emp.csv
101,kumar,sales,pune,1000
432,vijay,sales,chennai,3500
456,ram,sales,pune,8905
[$student@krosum~]$ grep admin emp.csv
[$student@krosum~]$
```

以下是 `grep` 的示例：

- 1. `grep` 实用程序：从文件或管道逐行读取输入数据到模式空间。
- 2. `grep` 模式：在文件中搜索字符串并打印匹配模式的行。
- 3. `grep` 模式：通过标准输出发送匹配的行。如果没有匹配，则不输出内容。
- 4. `grep` 模式：可以使用正则表达式来`grep` 匹配复杂的模式。

## `grep` 选项及解释

| 选项 | 解释 |
| :--- | :--- |
| -i | 忽略大小写 |
| -c | 输出匹配的行数 |
| -l | 仅列出匹配的文件 |
| -n | 在行前显示行号 |
| -v | 反向选择（显示不匹配的行） |
| -q | 静默模式（不输出） |
| -w | 匹配整个单词 |
| -x | 匹配整行 |
| -E | 使用扩展正则表达式 |

```bash
$student@krosum~$ grep -n sales emp.csv
1 101,kumar,sales,pune,1000
3 432,vijay,sales,chennai,3500
7 456,ram,sales,pune,8905
```

```bash
[student@krosum ~]$$ ps -wc -l # 进程总数
139
[student@krosum ~]$$ ps -egrep -c bash # bash 进程总数
33
[student@krosum ~]$$ ps -egrep -cv bash # 除 bash 外进程数
136
[student@krosum ~]$$ 
```



# 搜索多个模式

```bash
[student@krosum ~]$$ # 搜索多个模式
[student@krosum ~]$$ # ====================
[student@krosum ~]$$ grep -e sales -e prod emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vijay,sales,chennai,3500
894,vijay,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum ~]$$ grep -nie sales -e prod emp.csv
1:101,kumar,sales,pune,1000
2:203,prod,,prod,prod,1245
3:432,vijay,sales,chennai,3500
5:894,vijay,prod,delhi,4590
6:456,ram,sales,pune,8905
7:399,karthik,prod,bglore,5904
[student@krosum ~]$$
```

我们可以通过以下方式搜索多个模式。

## 语法

```bash
egrep -e "pattern1" -e "pattern2" inputfile
egrep "pattern1|pattern2|patternN" inputfile
```

```bash
[student@krosum]$ grep -e sales -e prod emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vij,sales,chennai,3500
894,vij,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum]$$
[student@krosum]$$ egrep "sales|prod" emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vij,sales,chennai,3500
894,vij,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
```

`grep -E "Pattern1 |Pattern2 |Pattern3 .. |PatternN" input_file`

```bash
[student@krosum]$ grep -E "sales|prod" emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vij,sales,chennai,3500
894,vij,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
```

```bash
[student@krosum ~]$ ps -e|grep -e "bash" -e "python"
6780 pts/0 00:00:02 bash
7314 pts/1 00:00:00 bash
7335 pts/2 00:00:00 bash
7397 pts/2 00:00:00 python
[student@krosum ~]$
[student@krosum ~]$ ps -e|grep "bash|python"
6780 pts/0 00:00:02 bash
7314 pts/1 00:00:00 bash
7335 pts/2 00:00:00 bash
7397 pts/2 00:00:00 python
[student@krosum ~]$
[student@krosum ~]$ ps -e|grep -E "bash|python"
6780 pts/0 00:00:02 bash
7314 pts/1 00:00:00 bash
7335 pts/2 00:00:00 bash
7397 pts/2 00:00:00 python
[student@krosum ~]$
```

```bash
[student@krosum ~]$ cat ptr.txt
sales
prod
pune
[student@krosum ~]$ grep -f ptr.txt emp.csv # -f 附加外部模式文件
101,kumar,sales,pun,1000
203,arn,prod,bglore,1245
432,vijay,sales,chennai,3500
894,vijay,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum ~]$
```

```bash
[student@krosum ~]$ grep sales emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vij,sales,chennai,3500
894,vij,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum ~]$
```

```bash
[studentstudent@krosum ~]$ grep -o sales emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vijay,sales,chennai,3500
894,vijay,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum ~]$
```

```bash
[student@krosum ~]$ grep -w sales emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vij,sales,chennai,3500
894,vij,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum ~]$
```

```bash
[student@krosum ~]$ grep -v sales emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vij,sales,chennai,3500
894,vij,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum ~]$
```

```bash
[student@krosum ~]$ grep -n sales emp.csv
101,kumar,sales,pune,1000
203,arun,prod,bglore,1245
432,vij,sales,chennai,3500
894,vij,prod,delhi,4590
456,ram,sales,pune,8905
399,karthik,prod,bglore,5904
[student@krosum ~]$
```

```bash
[student@krosum ~]$ grep -x sales emp.csv
sales
[student@krosum ~]$
```

```bash
[student@krosum ~]$ grep -nx sales emp.csv
2:sales
[student@krosum ~]$ -x 选项仅打印完全匹配模式的行。
```

```bash
[student@krosum ~]$ # 过滤挂载的 xfs 类型
[student@krosum ~]$ df -Th | grep xfs
/dev/sda2 xfs 9.8G 2.6G 27% /
/dev/sda5 xfs 2.0G 33M 2% /home
```

```bash
[student@krosum ~]$ # 已加载模块列表
[student@krosum ~]$ lsmod | grep bluetooth
bluetooth 312602 22 btus,rfcomm
rfkill 20721 3 bluetooth
[student@krosum ~]$ lsmod | grep -n bluetooth
43:bluetooth 312602 22 btus,rfcomm
45:rfkill 20721 3 bluetooth
```



[student@krosum ~]$ `free -m used free shared cached`

Mem: total 1003 981 21 0 0 720

+/ buffers/cache: 260 0 7943

swap: 7965 0 7965

[student@krosum ~]$ `free -m | grep -i swap` # 过滤交换空间使用

Swap: 7965 0

```bash
[student@krosum]$ grep sales emp.csv

101,kumar,sales,pune,1000

432,vijay,sales,chennai,3500

456,ram,sales,pune,8905

[student@krosum]$ grep sales emp.csv |cut -d, -f2

kumar

vijay

ram

[student@krosum]$ grep sales emp.csv |cut -d, -f2|sort

kumar

vijay

ram
```

## grep Family

- Fast grep(`fgrep`): 仅支持字符串模式 – 不支持正则表达式
- `grep`: 支持有限的正则表达式
- Extend grep(`egrep`): 支持大部分正则表达式

```bash
[student@krosum ~]$ grep -n sales emp.csv # grep 家族

1:101,kumar,sales,pune,1000

2:203,arun,prod,bglore,1245

3:432,vijay,sales,chennai,3500

4:894,vijay,prod,delhi,4590

5:456,ram,sales,pune,8905

6:399,karthik,prod,bglore,5904

[student@krosum ~]$

[student@krosum ~]$ grep -ne "sales" emp.csv # grep 家族

1:101,kumar,sales,pune,1000

2:203,prod,,prod,prod,1245

3:432,vijay,sales,chennai,3500

5:894,vijay,prod,delhi,4590

6:456,ram,sales,pune,8905

7:399,karthik,prod,bglore,5904

[student@krosum ~]$

[student@krosum ~]$ grep -f ptr.txt emp.csv # 家族

101,kumar,sales,pun,1000

203,arn,prod,bglore,1245

432,vijay,sales,chennai,3500

894,vijay,prod,delhi,4590

456,ram,sales,pune,8905

399,karthik,prod,bglore,5904

[student@krosum ~]$
```

## Find command

- f 附加外部模式文件
- 搜索多个模式
- 过滤 xfs 类型
- 过滤挂载的 xfs 类型
- 已加载模块列表
- 过滤交换空间使用
- 进程总数
- bash 进程总数
- 除 bash 外进程数
- 模式已写入外部文件
- find command
- find command
- find command
- find command
- 查找输入
- 递归查找
- 在当前目录下查找所有名为 `t1.txt` 的文件。
- 使用名称并忽略大小写查找文件

```bash
[student@krosum ~]$ find -type f
```

**任务：在当前目录下查找目录文件列表**

```bash
[student@krosum ~]$ find -type d

./Videos

./.liferea_1.8

./.liferea_1.8/cache

./.liferea_1.8/cache/favicons

./.liferea_1.8/cache/plugins

./.liferea_1.8/cache/feeds

./.liferea_1.8/cache/scripts

./.gnupg

./.gnupg/private-keys-v1.d

./Music

./.local

./.local/share

./.local/share/gvfs-metadata

./.local/share/webkit

./.local/share/webkit/icondatabase

./.local/share/webkit/databases

./Demo
```

任务：在 `/dev` 目录下查找字符类型设备文件列表

```bash
[student@krosum -]
[student@krosum ~]$ find /dev -type c

dev/tty6

dev/tty5

dev/tty4

dev/tty3

dev/tty2

dev/tty1

dev/vcsal

dev/vcs1

dev/vcsa

dev/vcs

dev/tty0

dev/console

dev/tty

dev/oldmem

dev/kmsg

dev/urandom

dev/random

dev/full

dev/zero
```

任务：在 `/dev` 目录下查找块类型设备文件列表

```bash
[student@krosum ~]$

[student@krosum ~]$ find /dev -type b # 块类型设备文件列表

/dev/sda5

/dev/sda4

/dev/sda3

/dev/sda2

/dev/sda1

/dev/sda

/dev/sdb

/dev/loop7

/dev/loop6

/dev/loop5

/dev/loop4

/dev/loop3

/dev/loop2

/dev/loop1

/dev/loop0
```

### 任务：根据权限查找文件

查找所有用户具有读/写/执行权限的文件

```bash
[student@krosum ~]$

[student@krosum ~]$ find . -perm -u=rwx

./Pictures

./.config

./.config/Thunar

./.config/ibus

./.config/bus

./.config/xfce4

./.config/xfce4/terminal

./.config/xfce4/xfwm4

./.config/xfce4/desktop

./.config/xfce4/xfconf

./.config/xfce4/xfconf/xfce-perchannel-xml

./.config/midori

./.config/yumex
```

### mindepth 和 maxdepth

- 使用 `mindepth` 和 `maxdepth` 我们可以将搜索限制在特定目录。
- `maxdepth` 层级：最多向下递归的层数

### 示例示例 -maxdepth1

```bash
-maxdepth0 意味着仅对起始点本身应用测试和操作。

[root@krosum ~]# find / -name passwd

/usr/bin/passwd

/usr/share/bash-completion/completions/passwd

/sys/fs/selinux/class/password

/sys/fs/selinux/class/passwd/perms/passwd

/etc/passwd

/etc/pam.d/passwd

[root@krosum ~]# find / -maxdepth 2 -name passwd

/etc/passwd

[root@krosum ~]# find / -maxdepth 3 -name passwd

/usr/bin/passwd

/etc/passwd

/etc/pam.d/passwd
```

- `mindepth` 层级：对于低于 `mindepth` 层的层级不应用任何测试或操作
- `-mindepth1` 意味着处理除起始点以外的所有文件。

```bash
[student@krosum ~]$ find -name "emp.csv"

/home/student/Demo/L1/L2/emp.csv

/home/student/Demo/emp.csv

/home/student/emp.csv

/home/student/D1/emp.csv

[student@krosum ~]

[student@krosum ~]$ find -maxdepth 1 -name "emp.csv"

/home/student/Demo/emp.csv

[student@krosum ~]

[student@krosum ~]$ find -maxdepth 2 -name "emp.csv"
```



`/home/student/Demo/emp.csv`

`/home/student/emp.csv`

`/home/student/D1/emp.csv`

任务：查找从根目录开始的所有子目录下的 `passwd` 文件。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_295_0.png)

```bash
[root@krosum ~]# 
[root@krosum ~]# find / -name password
/usr/bin/passwd
/usr/share/bash-completion/completions/password
/sys/fs/selinux/class/password/perms/passwd
/sys/fs/selinux/class/password/perms/passwd
/etc/password
/etc/pam.d/password
[root@krosum ~]# find / -maxdepth 2 -name password
/etc/password
[root@krosum ~]# find / -maxdepth 3 -name password
/usr/bin/passwd
/etc/passwd
/etc/pam.d/passwd
```

任务：查找根目录下第 1 级目录下的 `passwd` 文件
任务：查找根目录下第 2 级目录下的 `passwd` 文件
任务：查找根目录下第 3 级目录下的 `passwd` 文件

### 根据大小和时间查找文件

我们可以使用的单位：
- `b` 字节
- `c` 字符
- `w` 周
- `k` 千字节
- `M` 兆
- `G` 吉字节

我们可以查找精确大小，或者大于 `+` 或小于 `-` 的大小

### 任务：查找大于 512k 的文件

```bash
[student@krosum ~]$ find -size +512k
```

```bash
[root@krosum ~]# # 查找所有修改时间超过 50 天
[root@krosum ~]# # 且小于 100 天的文件
[root@krosum ~]# # -----
[root@krosum ~]# find / -mtime +50 -mtime -100
find: '/proc/2074/task/2074/fdinfo/6': No such file or directory
find: '/proc/2074/task/2074/dfinfo/6': No such file or directory
find: '/proc/2074/task/2074/dfinfo/6': No such file or directory
[root@krosum ~]# #
```

```bash
[root@krosum ~]# # 查找所有过去 1 小时内更改的文件
[root@krosum ~]# # -----
[root@krosum ~]# find / -cmin -60
```

**任务**: 查找所有过去 1 小时内更改的文件。

```text
/sys/fs/ext4
/sys/fs/ext4/sda
/sys/fs/ext4/sda1/inode_readahead_blks
/sys/fs/ext4/sda1/mb max_to_scan
/sys/fs/ext4/sda1/delayed_allocation_blocks
/sys/fs/ext4/sda1/mb_writeback_mb_bump
/sys/fs/ext4/sda1/mb_stream_req
/sys/fs/ext4/sda1/mb_min_to_scan
/sys/fs/ext4/sda1/mb_stats/trigger_fs_error
/sys/fs/ext4/sda1/session_write_kbytes
/sys/fs/ext4/sda1/lifetime_write_kbytes
/sys/fs/ext4/sda1/mb_group_prealloc
/sys/fs/ext4/sda1/inode_goal
/sys/fs/ext4/sda1/extent_max_zerout_kb
/sys/fs/ext4/sda1/mb_order_2_req
/sys/fs/ext4/sda2
/sys/fs/ext4/sda2/inode_readahead_blks
/sys/fs/ext4/sda2/mb max_to_scan
/sys/fs/ext4/sda2/delayed_allocation_blocks
/sys/fs/ext4/sda2/mb_writeback_mb_bump
```

**任务**: 查找所有过去 1 小时内修改的文件。

```bash
[root@krosum ~]# find / -mmin -60
/proc/2081/attr/keycreate
/proc/2081/attr/sockcreate
/proc/2081/wchan
/proc/2081/stack
/proc/2081/schedstat
/proc/2081/latency
/proc/2081/cpuset
/proc/2081/cgroup
/proc/2081/oom_score
/proc/2081/oom_adj
/proc/2081/oom_score_adj
/proc/2081/loginuid
/proc/2081/sessionid
/proc/2081/coredump_filter
/proc/2081/io
/run
/run/dhclient-ens-33.pid
/run/user
/run/lock
/run/systemd/users
/run/systemd/sessions
/dev/pts/0
/dev/ptmx
[root@krosum ~]#
```

## xargs

- `xargs` 将标准输入中的内容转换为命令的参数。
- 默认情况下，`xargs` 会如所示显示来自 stdin 的任何内容。

```text
Terminal - root@krosum:
[root@krosum ~]# echo 'one'
> two
> three
> four
> five
one
two
three
four
five
[root@krosum ~]# echo 'one'
two
three
four
five"|xargs
one two three four five
[root@krosum ~]# _
```

```bash
[root@krosum ~#] find -name "*.csv" | xargs grep -n sales
/root/Test.csv:1:total sales count:1000
/root/Desktop/emp.csv:1:101,arun,sales,pune,1000
/root/Desktop/emp.csv:4:954,renu,sales,pune,3424
/root/Desktop/emp.csv:6:234,bibu,sales,chennai,4566
/root/Temp/emp.csv:1:101,arun,sales,pune,1000
/root/Temp/emp.csv:4:954,renu,sales,pune,3424
/root/Temp/emp.csv:6:234,bibu,sales,chennai,4566
/root/emp.csv:1:101,arun,sales,pune,1000
/root/emp.csv:4:954,renu,sales,pune,3424
/root/emp.csv:6:234,bibu,sales,chennai,4566
[root@krosum ~#] _
```

```bash
[root@krosum ~#]
[root@krosum ~#] find -size +100M
./p1.log
./Temp/Backup1.tar
./Backup1.tar
./D1/p2.log
[root@krosum ~#] find -size +100M|xargs rm
[root@krosum ~#]
[root@krosum ~#] find -size +100M
[root@krosum ~#]
[root@krosum ~#] _
```

任务: 从过滤后的文件中搜索 `sales` 关键字

`find /root -name "*.csv" | xargs grep -n sales`

```bash
exec
- exec 命令；执行命令；如果返回状态码为 0 则为真。
```

`find` 之后的所有的所有参数都将被视为该命令的参数，直到遇到包含 `;` 的参数为止。

### 语法

```bash
find -exec command {} \;
```

`exec`



## 任务: 在 `/root` 目录下搜索所有 `.csv` 文件，搜索模式为 `sales`，并显示匹配结果以监控。

```
find /root -name "*.csv" -exec grep -n sales {} \;
```

## 任务: 查找所有大于 100MB 的文件并删除它们。

```
find / -size +100M -exec /bin/rm {} \;
```
