
其中 `system` 可以是 IP 地址或主机名。一旦添加了打印机，你就可以像使用其他打印机一样使用它。

## 章节总结

CUPS 是一个基于 IPP（互联网打印协议）的跨平台打印服务器。它处理通过打印队列设置和发送任务。配置打印机最简单的方法是通过命令行界面。你也可以使用 Web 界面配置 CUPS，通过将连接到打印机的系统上的浏览器指向 `localhost:631` 来访问它。从 Web 界面，你可以配置打印队列并修改队列中的打印任务。你可以使用命令行中的 UNIX 命令来发送任务 (`lp`)、显示打印队列 (`lpstat`) 以及从队列中删除任务 (`cancel`)。此外，CUPS 提供了 `lpinfo` 和 `lpadmin` 工具，允许你从命令行配置打印机。CUPS 和 Samba 允许你从 Windows 机器在 Linux 打印机上打印，反之亦然。

# 练习题

1. 你可以使用哪些命令行将文件发送到默认打印机？
2. 哪个命令可以取消系统上的所有打印任务？
3. 哪些命令可以列出未完成的打印任务？
4. 使用 Samba 共享打印机的目的是什么？
5. 写出 CUPS 支持三个打印协议。哪一个是原生协议？
6. 哪个命令列出 CUPS 可用的已安装驱动程序？
7. 你如何在不使用打印队列的情况下发送文本文件到打印机？为什么这样做是一个坏主意？
8. 假设你有一个厂家提供的名为 `printer.ppd` 的 PostScript 定义文件的打印机。你会使用哪个命令将此打印机以 USB 为名称添加到系统的第一个端口上？
9. 你如何定义一个配额，允许每个用户每周向名为 `LaserJet` 的打印机打印最多 50 页？
10. 为 `/etc/cups/cupsd.conf` 内部的 `<Location>` 容器定义一组访问控制规则，只要用户位于本地系统或 `domain.com` 域内，即可向所有打印机打印。

## 高级练习题

# 15 构建 Linux 内核

## 本章内容

- 下载内核源码 573
- 配置和编译 Linux 内核 575
- 安装内核、模块和相关文件 582
- GRUB：Linux 引导加载程序 583
- `dmesg`：显示内核消息 589

一旦安装了 Ubuntu Linux，你可能想要配置并构建一个新的 Linux 内核。Ubuntu Linux 带有一个预先编译的内核，这简化了安装过程。然而，通过配置和构建新内核，你可以创建一个符合你及其独特需求的定制化内核。定制化内核通常比通用内核要小。

有时你并不需要构建新内核。相反，你可以动态更改许多以前需要构建新内核才能更改的内容。这些更改的两种方法是使用启动命令行参数（第 82 页）或修改 `/etc/sysctl.conf`，系统在启动时 `sysctl` 会使用该文件（第 572 页）。

你可以将启动命令行上使用的任何参数添加到 `/etc/default/grub` 中的 `GRUB_CMDLINE_LINUX_DEFAULT` 变量中。例如，`acpioff` 可以防止 `acpid` 启动高级配置和电源接口守护进程。更多信息请参阅第 82 页。

`sysctl` 工具在系统运行时修改内核参数。该工具利用了 `/proc/sys` 的功能，该目录定义了 `sysctl` 可以修改的参数。

命令 `sysctl -a` 显示 `sysctl` 参数的完整列表。下面是显示和更改 `domainname` 内核参数的示例。在此示例中不需要引号，但你必须对任何会被 shell 解释的字符加上引号。

```bash
$ /bin/sysctl kernel.domainname

kernel.domainname = tcp.com

$ sudo /bin/sysctl -w kernel.domainname="example.com"

kernel.domainname = example.com

kernel.domainname = example.com
```

## 构建新内核时准备好安装光盘/DVD

当你构建新的 Linux 内核以安装新版本或更改现有内核的配置时，请确保手头准备好了安装光盘/DVD。这张光盘允许你重启系统，即使你已经完全破坏了系统软件。拥有这张光盘/DVD 往往意味着瞬间的恐慌与彻底的神经崩溃之间的区别。

在开始构建新内核之前，你必须下载、安装并清理源码。本章描述了完成这些任务的步骤。

如果你没有在 `/usr/src` 中工作，则必须将 `linux-source*` 文件复制到你所在的目录；否则，请使用 `cd` 进入 `/usr/src`。使用 `tar` 解压 Linux 源码文件：

```
$ tar -xjf linux-source-2.6.32.tar.bz2
```

### git：获取最新的内核源码

`git` 工具（GNU 原生接口，tools-git.com）可以下载多个内核源码的最新版本，并保持这些源码为最新状态。如果尚未安装，请运行以下命令安装 `git`：

```
$ sudo aptitude install git-core
```

#### 安装 git-core 而不是 git 包

请确保安装的是 `git-core`，而不是 `git` 软件包，该包对于下载内核源码没有用处。

以下命令使用 `git` 将一个开发版（非发布版）内核副本下载到工作目录的 `/ubuntu-2.6` 子目录中。作为 `src` 组的成员，你可以在 `/usr/src` 目录中工作。否则，你可以在任何你拥有写权限的目录中工作。你应该并且以非特权用户工作。

```
$ git clone git://kernel.ubuntu/ubuntu/ubuntu-lucid/ubuntu-2.6/

Initialized git repository in /home/sam/ubuntu-2.6/.

remote: Counting objects: 162412,

remote: Compressing objects: 100% (292458/292458), received 195684 (delta 1318584)

remote: Total 162417 (delta 162417/162417), 406.0 MiB | 392 KiB/s, done.

Receiving: 100% (134605/134605), done.

Resolving deltas: 100% (134605/134605), done.

Checking files: 100% (31201/31201), done.
```

请访问 `ubuntu.com` 和 `git.kernel.org` 获取可以下载的 Ubuntu 内核列表。将你想要下载的内核 URL 替换为上述命令中的 URL，并指定一个用于存放它的目录名称。例如，以下命令将最新的 Jaunty 内核下载到工作目录下的 `jaunty` 目录：

```
$ git clone git://kernel.ubuntu/ubuntu/ubuntu-jaunty jaunty
```

一旦下载了内核，请 `cd` 进入包含代码的目录，并运行以下命令更新源码，以便在 `git-clone` 命令中指定的 URL 上可用：

```
$ git pull

Already up-to-date.
```

如示例所示，你刚刚下载的文件应该是最新的。运行此命令可以同步工作目录中的代码。

### /usr/src/linux：工作目录

传统上，正在运行的内核源码保留在 `/usr/src/linux` 中。以下命令创建适当的符号链接。此示例显示的内核目录名称为 `linux-source-2.6.32`；你所工作的系统上的名称会略有不同。

```
# ln -s /usr/src/linux-linux-source-2.6.32 /usr/src/linux
```
