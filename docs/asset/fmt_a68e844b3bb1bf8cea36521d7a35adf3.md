
```bash
lilo
```

- 14. 当你下次重启 Linux 时，在初始 BIOS 消息之后会显示 LILO 启动提示。`timeout=50` 给你五秒钟时间来选择启动的内核。如果你按下 Shift 键然后按 Tab 键，将获得可用内核列表

```
LILO boot:  dos vmlinux  new_linux
```

- 15. 输入 `new_linux` 来加载你的新内核。否则，输入 `vm-linux`，或直接按 Enter 键获取旧版本。如果你等待超过五秒钟，旧内核会自动启动。你可以将此时间更改为任何想要的值。

这个过程需要很多指令，但只要稍微练习，其实非常简单。随着可加载模块的出现，这个过程已不再那么，但在你建立稳定的内核模块设置后它是很有用的。当你的系统处于生产模式时，为了简单起见，你可能想要重新编译常用函数。

## 定义 Red Hat 启动过程

第 4 章介绍了 Linux 启动过程。回想一下 `rc` 脚本用于启动各种守护进程并使系统运行。提供 `/etc/rc.d/rc.local` 脚本是为了让你添加指令来启动自己的守护进程。在下一章中，我将使用它启动几个守护进程，但我想在这里提到这是一个重要功能。

该脚本在所有其他启动脚本运行之后执行。因此，当你的脚本启动时，系统应该已经具有完全的功能。例如，网络服务应该已经启动，磁盘应该已经挂载。在你添加自己的功能之前，`rc.local` 脚本仅设置你登录时看到的标准登录界面。列表 5-11 显示了该脚本。

### 列表 5-11：`/etc/rc.d/rc.local` 文件

```bash
#!/bin/sh

## 此脚本将在所有其他 init 脚本*之后*执行。
## 如果你不想做完整的 Sys V 风格 init 操作，
## 可以在这里放入你自己的初始化内容。

if [ -f /etc/redhat-release ]; then
  R=$(cat /etc/redhat-release)

arch=$(uname -m)
case "$arch" in
  x86*) a="an2";
  i386*) a="an3";
esac

NUMPROC=$(cat /proc/cpuinfo | grep -i ^bogomips | wc -l)
if [ "$NUMPROC -gt 1 ]; then
  SMP="$NUMPROC-processor"
  if [ "$NUMPROC" = "8" -o "$NUMPROC" = "11" ]; then
    a="an2"
  else
  fi
```

## 这将在每次启动时覆盖 `/etc/issue`。

# 想要将内容写入 `/etc/issue`，否则在重启时会丢失它们。

```bash
echo "" /etc/issue
echo "$SR" /etc/issue
echo "Kernel\$(uname -r) on $SAMP\$(uname -m)" /etc/issue
```

```bash
cp -f /etc/issue /etc/issue.net
echo > /etc/issue
```

fi

如果你需要，可以修改其他脚本，但修改这个脚本是一个简单的过程。如果你使用它，不必担心破坏任何东西。

## 总结

Linux 配置是一个大课题。在本章中，通过示例描述了配置 Red Hat Linux 的基础。`RPM` 系统使得添加、删除和升级系统功能、应用程序和实用程序的任务变得非常简单。Linux 系统本身是模块化的。

## 第三部分：扩展你的网络服务

### 第 6 章通过示例学习 Samba

### 第 7 章连接互联网

### 第 8 章创建 NFS、NIS、DNS 和电子邮件服务器

## 第 6 章

### 通过示例学习 Samba

本章内容

- 重配置 Samba
- 理解 Samba 守护进程
- 理解 Samba 配置
- 修改 Samba 配置
- 修改 Linux
- 配置 Linux 打印机
- 添加 Samba 打印共享
- 验证 Samba 服务请求

在第 1 和第 2 章中，你学习了如何建立一个简单的客户端/服务器网络。该网络拥有所有基本要素，可以作为实用性个人或业务系统的基础：

- 多用户、多任务、虚拟内存并支持 TCP/IP 网络的 Linux 操作系统。
- 由微软兼容网络 Samba 服务器导出的资源。
- Windows 95/98/NT 客户端，可以连接并使用由 Linux-Samba 服务器提供的服务。

通过在这个基础上添加一些新部分，你可以创建一个强大的网络。本章将展示如何扩展你的简单网络，创建一个能够运行小型业务或家庭办公室的 Linux-Samba 服务器。

如果你在 Red Hat 安装过程中（第 1 章）没有安装 Samba，那么现在安装它。

- 1. 以 root 身份登录 chivas。
+ 2. 挂载 Red Hat 出版版 CD-ROM。

`mount /mnt/cdrom`

+ 3. 安装 Samba 软件包。

`rpm -ivh /mnt/cdrom/RedHot/RPMS/samba`

+ 4. 本章稍后给出的几个示例需要修改 Samba 配置文件 `/etc/smb.conf`。现在制作一个备份副本是一个好主意。

`cp /etc/smb.conf /etc/smb.conf.orig`

该文件将用于所有示例中。

从第 2 章中描述的基础配方开始，你可以添加所有你需要的 Windows 客户端，直到服务器过载为止（Samba 没有实际限制；唯一的限制是你的服务器的性能）。你通过修改 Samba 配置文件 `/etc/smb.conf` 来添加 Windows 客户端。该文件控制着以下要素：

- 在网络上共享的目录。它们被称为共享（shares）或服务（services）。
- 在网络上共享的打印机。这些也被称为共享（shares）或服务（services）。
- 谁可以使用每个目录。访问权限可以提供给个人、特定组或所有人。
- 谁可以使用每个打印机。访问权限可以提供给个人、特定组或所有人。
- 用于安全、访问和调优的各种杂参数。

本章侧重于重新配置 Samba。通过修改 Samba 服务器，你可以立即将最初的简单示例转变为真正可用的服务器。本章还描述了如何通过使用用户和修改权限来扩展你的 Samba 系统。随着 Samba 2.0 的引入，增加了一个图形化界面。它简化了修改 Samba 的工作。然而，理解 `smb.conf` 文件如何影响 Samba 的行为以及如何修改它非常重要。从长远来看，使用图形界面可以简化你的工作，除非你理解底层系统，否则你将无法充分理解你的系统。因此，大多数示例都展示了如何手动修改。

## 理解 Samba

在原理上，添加 Samba 客户端的过程非常简单。通过编辑 `smb.conf` 文件，你可以添加、删除和修改共享。共享是一种资源——通常是目录或打印机——Samba 服务器向网络提供的资源。从 Samba 配置的角度来看，`smb.conf` 文件被分为若干定义服务的节（sections）。

![](img/1fa05dc2b61f40be78509e4d8bfc1fe6_198_0.png)

## 学习 Samba：一个示例

你将在本章中多次修改 `smb.conf` 文件，因此在开始之前为它创建一个备份副本。在每个示例开始时，从备份副本恢复 `smb.conf` 以尽量减少冲突。使用以下命令创建备份副本：

`cp /etc/smb.conf /etc/smb.conf.orig`

有很多参数可用于配置 Samba。某些变体是同义词；另一些用于精细调整。由于你可以以多种方式组合几个参数，配置 Samba 是一项复杂的任务。

## 理解守护进程 (Daemons)

Samba 的核心是两个守护进程——在后台持续运行的系统进程。`smbd` 守护进程监控网络共享请求。当它检测到共享请求时，`smbd` 遍历 Linux 获取 Samba 所代表的资源——即目录或打印机，并将该资源提供给请求它的客户端。资源——例如一个文件——留留在 Linux 服务器上，但 Samba 客户端可以像它位于客户端磁盘上一样使用它。名称服务器——`nmbd` 控制 Windows 客户端的浏览（例如当你打开“网络”时），并响应 Windows 客户端查找 Samba 的请求（名称服务器将名称转换为 IP 地址。因此，`nmbd` 将 `localamba.com` 转换为 `192.168.1.1`）。两个守护进程在启动时读取 `smb.conf` 文件以确确定导出哪些服务。当你从 Windows 环境打开目录、文件或打印机时，你会请求共享。在第 1 章中，例如当你从“网络”双击计算机图标时，你会访问共享；你应该看到一个包含 `/root` 目录内容的窗口。如果什么都没看到，尝试复制文件到 `/root` 目录。接下来，以 root 身份登录 Linux 服务器并输入以下命令：

`ps aux | grep smbd`
