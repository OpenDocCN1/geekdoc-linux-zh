

# 15
# 构建 Linux 内核

# 本章内容

- 下载内核源码 . . . . . . . . . . . . . . . . . . . . 573
- 配置和编译 Linux 内核 . . . . . . . . . . . . . . . . . . 575
- 安装内核、模块及相关文件 . . . . . . . . . . . . . . . . . 582
- GRUB: Linux 启动程序 . . . . . . . . . . . . . . . . . . . 583
- dmesg: 显示内核消息 . . . . . . . . . . . . . . . . . . . . 589

一旦你安装了 Ubuntu Linux，你可能想要重新配置并构建一个新的 Linux 内核。Ubuntu Linux 自带了一个预构建的内核，这简化了安装过程。然而，该内核可能没有针对所有系统功能进行正确配置。通过配置和构建新内核，你可以创建一个针对系统及其独特需求定制的内核。定制的内核通常比通用内核更小。

有时你并不需要构建新内核。相反，你可以动态更改许多以前需要构建新内核的设置。实现这些更改有两种方法：使用启动命令行参数（第 82 页）或修改 `/etc/sysctl.conf`，后者会在系统启动时生效（第 572 页）。

你可以将你在启动命令行中使用的相同参数添加到 `/etc/default/grub` 中的 `GRUB_CMDLINE_LINUX_DEFAULT` 变量中。例如，`acpi=off` 防止 `acpid`（高级配置和电源接口守护进程）启动。更多信息请参阅第 82 页。

## sysctl
`sysctl` 工具可以在系统运行时修改内核参数。该工具利用了 `/proc/sys` 的功能，该目录定义了 `sysctl` 可以修改的参数。

命令 `sysctl -a` 显示 sysctl 参数的完整列表。以下是显示和更改域名（domainname）的示例。在此示例中不需要引号，但你必须对任何会被 shell 解释的字符加引号。

```
$ /sbin/sysctl kernel.domainname
kernel.domainname = tcorp.com
$ sudo /sbin/sysctl -w kernel.domainname="example.com"
kernel.domainname = example.com
$ /sbin/sysctl kernel.domainname
kernel.domainname = example.com
```

## 构建新内核时请备好安装 CD/DVD

**注意**：当你构建新的 Linux 内核以安装新版本或更改现有版本的配置时，请确保你手头准备好了安装 CD/DVD。这允许你在即使完全破坏了系统软件的情况下也能重启系统。拥有此 CD/DVD 可能意味着在瞬间的恐慌与全面的神经崩溃之间产生区别。

在开始构建新内核之前，你必须下载、安装并清理源码。你还需要构建一个描述你想要构建的新内核的配置文件。本章描述了完成这些任务涉及的步骤。

## 前提条件

安装以下软件包：

- linux-source（最新发布的内核源码；如果你使用 git 下载代码，则不需要）。尝试安装 `linux-source` 会显示持有最新内核的包名称，然后你再安装该包；请参阅下一节。
- build-essential（元包；包含编译代码所需的软件包）。
- fakeroot, kernel-package（内核特定）
- git-core（用于使用 git 下载内核源码）
- ncurses-dev（用于使用 `make menuconfig` 配置内核）
- libglade2-dev（用于使用 `make gconfig` 配置内核）
- module-assistant, debhelper（创建模块）

## 编译内核需要大量磁盘空间

在编译内核之前，请确保你有足够的磁盘空间。一旦编译了默认内核，它将占用大约 3.5 GB字节的空间。此磁盘空间必须在编译内核的文件系统中可用。

## 下载内核源码

本节描述了在本地系统中下载内核源码的两种方法：`aptitude`（或 Synaptic）和 `git`。如果你想下载未经过 Ubuntu 定制（补丁）的代码，请访问 kernel.org 或查看关于 git 的章节。

## aptitude：下载并安装内核源码

下载 Ubuntu 内核最新发布版本的更新内核源码最简单的方法是使用 `aptitude`。以下命令确保包索引是最新的并下载 `linux-source` 包。`dpkg` 脚本会将压缩的源码解压到 `/usr/src/linux-source:*`：

```
$ sudo aptitude update
$ sudo aptitude install linux-source
```

将安装以下新软件包：
linux-source linux-source-2.6.32

```
$ ls -l /usr/src/linux-source/
1 root root 65726108 2010-04-09 18:23 /usr/src/linux-source-2.6.32.bz2
-rw-r--
```

由于 `/usr/src` 与 `src` 组相关，如果你是该组的成员，可以在 `/usr/src` 中提取内核。否则，你可以在任何你有访问权的目录中提取。

## 不要使用 root 权限

在配置或构建内核的任何部分（安装步骤除外），你都不需要 root 权限权限。内核文件说：“不要妄用 root 名”。只要你是 `src` 组的成员，就可以在 `/usr/src` 下下载、配置和编译内核，而无需 root 权限。

你可以使用 `usermod` 将自己加入 `src` 组。以下命令将 Max 添加到 `src` 组以便他在 `/usr/src` 中工作。Max 需要注销并重新登录，以便系统识别其为该组成员。

```
$ sudo usermod --append --groups src max
```

如果你不在 `/usr/src` 中工作，必须将 `linux-source*` 文件复制到你工作的目录；否则，进入 `/usr/src`。使用 `tar` 解压文件：

```
$ tar -xjf linux-source-2.6.32.bz2
```

## git：获取最新源码

`git` 工具（GNU 交互式工具）可以下载多个内核的源码并保持这些源码更新。如果没有安装，执行以下命令安装 git：

```
$ sudo aptitude install git-core
```

访问 kernel.com/git 和 git.kernel.org 可获取可以下载的内核列表。将你想下载的内核 URL 替换为上述命令中的 URL，并指定一个适当目录名称存放下载的文件。例如，以下命令将最新的 jaunty 内核下载到工作目录下的 `jaunty` 目录：

```
$ git clone git://kernel1.ubuntu.com/ubuntu/ubuntu-jaunty.git jaunty
```

一旦下载了内核，进入代码所在的目录并执行以下命令，更新源码以匹配你在 `git-clone` 命令中指定的 URL：

```
$ git pull
Already up-to-date.
```

