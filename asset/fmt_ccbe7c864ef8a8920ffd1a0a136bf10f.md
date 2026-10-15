
# Ubuntu 和 CentOS Linux 服务器管理

献给我的女儿 Safiyyah Nawar 和 Nuzairah Zainab

# 绪言

操作系统运行在我们计算机上的软件。它处理用户与计算机硬件之间所有的指令。但操作系统不仅仅是一个软件，它还由许多运行在该操作系统上的较小程序组成，帮助用户完成工作。我们在操作系统之上运行这些较小的程序来完成一切。

Linux 只是另一个操作系统。它是一个非常可靠的操作系统。Linux 既可以作为服务器操作系统，也可以作为桌面操作系统。

Linux 操作系统优秀有很多很多优点，原因如下：

## Tanvir Rahman

- 多用户操作系统：Linux 是一个多用户操作系统。这意味着多一个用户可以同时在一个系统上工作。

- 多任务操作系统：Linux 是一个多任务操作系统，你可以同时运行多个程序。这允许操作系统同时运行多个进程。

- 多平台操作系统：Linux 目前可以运行在 24 多种类型的平台上，以及基于 Intel 的 64 位个人电脑。所有的 Apple Mac 变体、Sun Spark、iPod，甚至是微软的 Xbox。

- 互操作性操作系统：Linux 可以与大多数网络协议和语言配合；它可以轻松与 Windows 操作系统、NOVEL、UNIX 以及市场份额较小的操作系统进行交互。

- 可扩展性操作系统：Linux 操作系统支持从信用卡大小的计算机（树莓派）到强大的服务器。世界上大多数服务器都在运行 Linux OS。它们也运行在低功耗计算机上。

- 可移植操作系统：Linux 是一个可移植的操作系统。Linux 主要用 C 语言编写。C 语言是一种专门为编写操作系统级软件设计的语言。它可以被移植到新的计算机上运行。

- 灵活性操作系统：Linux 操作系统可以用于制作路由器、图形工作站、家庭娱乐电脑、文件服务器、Web 服务器、邮件服务器、集群，任何计算目的。

- 稳定性：Linux 内核非常成熟。因为其稳定性，它被世界上大多数服务器使用。

- 高效性：Linux 的设计允许你只包含需要的内容，这就是为什么它可以既运行在树莓派上，也可以运行在大服务器上。

- 免费：Linux 是一个免费的操作系统。

## GNU 项目

GNU 代表（GNU 并非 UNIX）。为了创建一个 UNIX 操作系统的免费克隆版本，GNU 项目于 1984 年启动。为了维护自由软件，创建了 FSF（自由软件基金会）。它创建了 GNU C 编译器、EMACS 文本编辑器以及许多其他软件。

GNU 通用公共许可证（GPL）是一项极具创造意的执照许可证，用于通过版权来保护软件用户的自由。当软件在 GPL 下许可时，接收者受到版权的约束，必须尊重任何人使用和共享该软件的自由，并在必要时更改源代码。

## LINUX 历史

Linux 是基于 UNIX 的操作系统的克隆版本。Unix 是在贝尔实验室为 AT&T 公司创建的。为了制作 Unix 的免费克隆版本，Linus Torvalds 创建了 MINIX。他编写了作为 Linux Core 的内核。之后，许多开发者帮助他添加了更多功能和特性，当时 GNU 项目正在为计算机开发自由软件，为了创建一个操作系统，他们需要一个与硬件通信的功能性内核。他们采用了 Linux 内核并在内核之上添加了 GNU 软件，制作了 GNU/LINUX 操作系统。

Linus Torvalds 仍然被视为 Linux 内核的独裁。他最终决定哪些特性将添加到 Linux 内核中，哪些特性不会。

## Linux 打包：发行版

一个完整的 Linux 系统被称为发行版（Distribution）。Linux 发行版包含 Linux 内核、GNU 项目工具以及任何可以使操作系统功能多样化的软件。

Linux 有很多发行版。其中一些专门用于服务器，另一些用于桌面。每个定制的发行版都包含针对不同用户的软件包。

单一 Linux 发行版通常以不同的版本出现。例如，Centos 发行版带有完整的核心发行和一个 LIVE CD 版本。

Ubuntu 基于 Debian 发行版，而 CentOS 是商业版 RedHat Linux 发行的社区版本。

## 核心 Linux 发行版

核心 Linux 发行版包含 Linux Kernel 和 GNU 操作系统、一个或多个 DE（桌面环境）以及可以直接安装运行的应用。核心 Linux 发行版是完整的 Linux 发行版。以下是流行的发行版：

- Red Hat linux
- Fedora Core
- Centos Linux
- SUSE linux
- Ubuntu Linux
- Gentoo Linux
- Debian Linux
- Slackware Linux
- Mandriva Linux
- Turbo Linux
- Puppy Linux

我们使用 Ubuntu Linux 和 Centos Linux 来演示服务器是如何工作的。

## LINUX 原则

- 一切都作为文件运行，即使是系统硬件
- 小工作由单个程序完成
- 任何完成的工作将拆分为更小的部分，然后由不同的模块处理
- 所有配置将存储在文本文件中
- Linux OS 使用标准的分级文件结构，文件/用户文件在其中排列

## UBUNTU 服务器

Ubuntu 构建在 Debian 架构之上，由 Linux 服务器和桌面组成。Ubuntu 每六个月更新一次；Ubuntu 软件包基于 Debian 不稳定分支的包。Ubuntu 目前由 Canonical LTD 资助。从 17.10 版本开始，GENOME 3 是 Ubuntu 的默认 GUI 界面。我们将使用 Ubuntu Server 18.04.3 LTS 进行工作。你可以在此 URL 下载最新的长期支持 ubuntu server：

https://ubuntu.com/download/server

## CENTOS 服务器

CentOS 项目是一项社区驱动的自由软件努力，专注于围绕 Linux 平台提供一个稳健的开源生态系统。它基本上是 Redhat 的克隆。CentOS Linux 是一个一致、可管理的平台，适用于各种部署。对于某些开源社区来说，它是一个坚实、可预测的基础。你可以在此 URL 下载最新的长期支持 CentOS server：

https://centos.org/download/

## VMWARE 安装

### 第 1 步

安装所需的构建包

=> `sudo apt install build-essential`

### 第 2 步

从网站下载 VMware workstation player。

![](img/b48bb5eea64d70d0c5160c63325a327c_17_0.png)

### 第 3 步

进入安装目录，赋予文件执行权限

=> `chmod 777 vmware-Player*`

## Tanvir Rahman

[稍后会讨论 `chmod 777`，现在直接使用即可]

### 第 4 步

使用 sudo 执行程序

=> `sudo ./Vmware-Player*`

![](img/b48bb5eea64d70d0c5160c63325a327c_18_0.png)

[不需要许可证密钥。如果你想安装 vmware workstation 而不是 vmware player，你需要许可证密钥]

安装成功后，屏幕将显示：

12

## UBUNTU $ CENTOS 管理员

![](img/b48bb5eea64d70d0c5160c63325a327c_19_0.png)

***

## UBUNTU 服务器安装

### 要求：

1) 至少 4GB 内存的主机 PC
2) VMWARE WORKSTATION/VIRTUALBOX
3) UBUNTU SERVER ISO 镜像

### 第 1 步

启动 VMware Workstation 新虚拟机向导

![](img/b48bb5eea64d70d0c5160c63325a327c_20_0.png)

### 第 2 步

选择安装媒体或源。

![](img/b48bb5eea64d70d0c5160c63325a327c_21_0.png)

## Tanvir Rahman

### 第 3 步

Vmware 的最终配置如下：

![](img/b48bb5eea64d70d0c5160c63325a327c_22_0.png)

### 第 4 步

开始安装，首先设置语言：

- English
- Castellano
- Français
- Deutsch
- Eesti
- Hungarian
- Dutch
- Norwegian
- Polski
- Русский
- Español

### 第 5 步

从软件选择中选择带 GUI 的服务器

![](img/b48bb5eea64d70d0c5160c63325a327c_23_0.png)

### 第 6 步

选择用于安装的卷。在本次安装中，我们选择整个磁盘引导分区：

![](img/b48bb5eea64d70d0c5160c63325a327c_24_0.png)

### 第 7 步

有三种分区类型：

- 引导：使用整个磁盘
- 手动：在手动分区中用户必须分配空间：
  1) `/boot`
  2) `/swap`
  3) `/root`

### 第 8 步

基于 LVM 的引导：此选项允许用户设置 LVM

![](img/b48bb5eea64d70d0c5160c63325a327c_25_0.png)

# UBUNTU CENTOS 管理员

![](img/b48bb5eea64d70d0c5160c63325a327c_31_0.png)

# 第 8 步

等待安装完成。完成后重启系统。

# 第 9 步

使用 root 凭登录

Tanvir Rahman

# 总结：

我们学习了如何使用引导分区在 VMware 虚拟机上设置 CentOS 服务器。

***

# LINUX 命令行

每个 Linux 工作站版本都有漂亮的 GUI（图形用户界面），但大多数 Ubuntu 或 Centos 服务器的 root 可以在命令行模式下完成任何操作。你可以为它添加图形用户界面，但如果没有命令行，你就无法妥善地管理服务器。一旦学会了命令行，你会发现它比图形模式更强大、更灵活管理服务器。

## 以 root 身份运行

默认情况下，每个 Linux 操作系统都会创建一个 root 用户。许多操作系统（如 CentOS）会要求 root 密码。但 Ubuntu 服务器不会这样做。这有一个非常好的理由。在 Linux 操作系统中，root 拥有无限权限。root 可以做任何事情，更改任何事情，甚至从服务器上删除任何事情。因此，以 root 身份工作时非常小心。这就是为什么在 Tanvir 的 ubuntu 服务器中，每次执行任何需要超级用户权限的操作都要使用 `sudo` 命令。此命令允许普通用户执行需要超级用户权限的任务。你输入 sudo 然后输入你的命令，可能会提示输入密码，提供密码后它将以超级用户权限执行操作。但如果你想要 root shell，请输入此命令：

```
=> sudo su
```

但不建议使用 root shell 工作。除非绝对必要，否则不要使用 root shell。如果需要超级用户权限，请使用 sudo。

# 终端与 shell

### 什么是终端

终端是一个打开窗口并让你操作 shell 的程序。在 Linux 发行版中你可以许多不同的终端模拟器，例如 Gnome terminal, konsole, xterm, rxvt, nxterm, eterm, Tilikix 等。终端让你与 shell 交互。

### 什么是 shell

Shell 本身是一个程序，它接收键盘上的命令并将其交给操作系统执行。你可以使用图形用户界面工作，但如果你使用的服务器没有图形用户界面，这将是你获得的唯一界面，你必须在 CLI（命令行界面）中完成所有工作。

有不同类型的 shell：

- tsh -> tsh 是一种带有类似于 C 语言的脚本语言的 shell
- sash -> 独立 shell。这是一个非常极简的 shell，运行于几乎所有系统。它主要用于系统故障排除
- zsh -> zsh 是一个与 bash 兼容但具有许多额外功能的 shell
- fish -> fish 代表 friendly interactive shell（友好交互 shell）。主要在桌面流行。它有非常好的自动补全功能
- Bash -> bash 代表 Bourne Again Shell，它是原始 UNIX 程序 sh 的增强版本。它由 Steve Bourne 编写。它是最流行的 shell，也是大多数 Linux 操作系统的默认 shell。

我们将在所有示例中使用 Bash。

***

# 基础 LINUX 命令

这些是操作 Linux 操作系统的基本命令。

## 命令名：ls

**描述：**

`ls` 命令用于查看目录内部的文件和文件夹。它是 Linux 中最常用的命令。

**语法：**

`ls [-option] <directory>`

- 1) `ls -m` 将用逗号分隔显示文件和文件夹
- 2) `ls -a` 也会显示隐藏文件
- 3) `ls -l` 将以列表格式显示文件和文件夹
- 4) `ls -lh` 将显示带有大小的文件
- 5) `ls -i` 将显示带有 Inode 的文件夹列表
- 6) `ls -t` 将在目录列表运行时显示修改时间

## 命令名：more

**描述：**

它的工作方式类似于 `more` 命令。它还提供了滚动选项。

**语法：**

```
more <options> <file_name>
```

- 1) `less -E` : 第一次到达末尾时自动退出
- 2) `less -f` : 强制打开非普通文件
- 3) `less -F` : 如果整个文件都能显示在屏幕上则退出
- 4) `less -g` : 高亮显示搜索到的字符串
- 5) `less -G` : 抑制搜索命令找到的所有字符串高亮
- 6) `less -i` : 忽略大小写
- 7) `less <pattern>` : 告诉 less 从文件中模式第一次出现的地方开始
- 8) `less -s` : 将连续的空行合并为一行
- 9) `less -n` : 抑制行号
- 10) `less <pattern>` : 告诉 less 从文件中模式第一次出现的地方开始
- 11) `less -s` : 使连续的空行压缩
- 12) `less -N` : 显示行号

## 命令名：strings

**描述：**

显示文件的内容

**语法：**

`strings <filename>`

## 命令名：tree

**描述：**

以树形格式显示目录

**语法：**

`tree <directory>`

[你可能需要通过包管理器安装 `tree`]

## 命令名：dir

**描述：**

显示目录内部的文件和文件夹

**语法：**

`dir <directory_name>`

[你必须在此命令执行前安装它]

## 命令名：cal

**描述：**

显示日历

**语法：**

`cal <month> <year>`

## 命令名：clear

**描述：**

清除屏幕

**语法：**

```
clear
```

## 命令名：bc

**描述：**

基础计算器

**语法：**

```
bc
```

## 命令名：mkdir

**描述：**

创建目录

**语法：**

```
mkdir <directory> : 用于创建单个目录
mkdir -p <directory>: 用于创建递归目录
```

## 命令名：rmdir

**描述：**

删除空目录。你无法用此命令删除任何包含文件的目录

**语法：**

`rmdir <empty_directory>`

## 命令名：file

**描述：**

显示文件类型

**语法：**

`file <filename>`

## 命令名：ln

**描述：**

创建文件名的链接。在硬链接的情况下，你删除主文件链接不会被删除；但在软链接的情况下，如果你删除主文件，链接的文件将被删除。

**语法：**

`ln <option> <source_file> <shortcut_file>`

- `ln -s` : 用于创建软链接
- `ln -P` : 用于创建硬链接

## 命令名：history

**描述：**

显示用户的命令历史，它将显示最后 100 条命令，你可以根据需要设置限制

**语法：**

`history`

## 命令名：locate

**描述：**

在整个系统中搜索该文件[你需要运行 `updateddb` 命令获取最新条目]

**语法：**

`locate <file_name>`

## 命令名：uname

**描述：**

显示关于内核、操作系统和硬件的所有信息

**语法：**

- `uname -a` : 所有信息，顺序如下
- `uname -s` : 打印内核名称
- `uname -n` : 打印主机名
- `uname -r` : 打印内核版本
- `uname -v` : 打印内核版本
- `uname -m` : 打印机器硬件名称
- `uname -p` : 打印处理器类型
- `uname -i` : 打印硬件平台
- `uname -o` : 打印操作系统

## 命令名：tar

**描述：**

用于创建包和提取包

**语法：**

- `tar -cvf <archive_name> <source>` : 用于创建包
- `tar -xvf` : 用于提取包

## 命令名：gzip

**描述：**

对普通文件或存档进行压缩

**语法：**

`gzip <file_name>`

## 命令名：gunzip

**描述：**

用于解压缩压缩文件

**语法：**

`gunzip <compressed_file>`

## 命令名：lsmod

**描述：**

显示内核使用的模块列表

**语法：**

`lsmod`

## 命令名：rmmod

**描述：**

删除内核使用的任何模块[不建议 .除非你绝对确定自己在做什么]

**语法：**
