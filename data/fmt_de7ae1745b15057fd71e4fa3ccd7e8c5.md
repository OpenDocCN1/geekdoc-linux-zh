
在此上下文中，`pam_unix.so` 模块引入了用户名信息，根据 `/etc/shadow` 配置文件中的设置判断用户账户处于激活状态。最后，检查 `/etc/pam.d/common-session` 配置文件。除非安装了适当的 LDAP 模块，它有两行活动代码：

```
session required pam_unix.so
session optional pam_foreground.so
```

第一条 `session` 命令记录登录和注销。第二条命令由于它被设置为可选的（`optional`），PAM 会忽略模块的成功或失败。

## 认证目标 10.02

## 设置网络文件系统

在本节中，你将看到如何配置 NFS、CIFS 和 FTP 服务以基本操作。NFS 提供了与其他 Linux 和 Unix 系统的互操作性。CIFS 提供了与 Microsoft 系统的交互性。FTP 是最老的文件共享服务之一，几乎每个常用的操作系统都可用，并且仍在在使用。

> 理解配置网络文件系统的基础知识。虽然简要提到了“Windows 共享”和 FTP，但 UCP 课程主要关注 NFS 概念，涉及 `/etc/exports` 以及与 NFS 内核服务器相关的守护进程。

## 网络文件系统 (NFS)

NFS 是在 Linux 和 Unix 计算机目录上共享文件和打印机的标准。它最初由 Sun Microsystems 在 20 世纪 80 年代开发。多年来它一直支持 NFS（作为客户端和服务器），并且 NFS 在基于 Unix 的网络的组织中继续流行。

NFS 共享的一个弱点是缺乏加密。默认情况下，NFS 共享是不加密的，目前的守护进程无法加密此类数据。

你可以通过编辑 `/etc/exports` 直接创建共享的目录，或者使用 Ubuntu 的共享工具（将在本文末尾讨论）。

### 所需软件包

三个包与 NFS 密切相关：`portmap`、`nfs-common` 和 `nfskernelserver`。如果默认没有安装它们，你可能需要使用下面的命令将它们集成到系统中：

```
$ sudo apt-get install portmap nfs-common nfskernelserver
```

`portmap` 包必须运行 NFS 才能工作——包括客户端和服务器。如果你在连接 NFS 服务器时遇到问题，请确保运行以下命令启动守护进程：

```
$ sudo /etc/init.d/portmap restart
```

它也是 NIS 服务器顺利运行的前提，因此本地系统可能已经安装并运行。它通常配置为在启动过程中启动。

一旦 `portmap` 服务启动，你应该运行 `rpcinfo -p` 命令来查看使用 `portmap` 的服务。以下来自我的 Ubuntu 系统的输出显示 `/sbin/portmap`、`/usr/sbin/rpc.nfsd` 和 `/usr/sbin/rpc.mountd` 守护进程正在运行：

| | program | service |
| :--- | :--- | :--- |
| 100000 | 2 udp | 111 portmapper |
| 100003 | 2 udp | 2049 nfs |
| 100005 | 1 udp | 36883 mount |
| 100005 | 1 tcp | 37988 mount |

## 配置 NFS 以基本操作

NFS 相当简单。主要的 NFS 配置文件是 `/etc/exports`。该文件的每一行都列出了要导出的目录、导出目标的主机，

# 368 第 10 章：网络身份验证与文件系统

适用于此导出的选项。你只能导出一次特定的目录。参考以下 `/etc/exports` 文件中的示例：

```
/pub (ro,sync) one.example.net (rw, sync)
/home *example.net (rw, sync)
/tftpboot nodisk.example.net (rw,no_root_squash, sync)
```

在该示例中，`/pub` 目录以只读模式导出给所有用户。`/home` 目录以读/写权限导出到一个特定的计算机，即 `/example.net` 网络上的任何计算机。最后，`/tftboot` 目录在 `nodisk.example.net` 计算机上以完全读/写权限导出（即使对于 root 用户）。

这些选项都包含了 `sync` 标志。这要求在文件复制完成之前，所有更改必须写入磁盘。

![](img/8521db60567337b3b9ca1b288c5d36b6_387_0.png)

请务必小心处理 `/etc/exports`；问题的常见原因之一是导出项末尾有多余的空格。如果在 `(ro,sync)` 中的逗号后有空格，该目录将无法导出，并且你会收到错误消息。

## 通配符与通配匹配（Globbing）

在 Linux 配置中，你可以使用正确的通配符指定一组计算机，这在 Linux 中也称为通配匹配（globbing）。你对通配符的操作取决于配置文件。NFS 的 `/etc/exports` 文件使用“常规”通配符；例如，`*example.net` 指定 `example.net` 域名内的所有计算机。相比之下，`/etc/exports` 则不那么常规；以点开头的 `.example.net` 表示该域内的所有计算机。

对于 IPv4，通配符需要某种形式的子网掩码。例如，`192.168.0.0/255.255.255.0` 指定 `192.168.0.0` 网络，其 IP 地址范围从 `192.168.0.1` 到 `192.168.0.254`。某些服务支持使用 CIDR（类间域网路由）路由。在 CIDR 中，`255.255.255.0` 掩码了 24 位，CIDR 用数字 24 表示此。如果你在用 CIDR 记法配置网络，可以将此网络表示为 `192.168.0.0/24`。

## 激活导出列表

一旦你修改了 `/etc/exports`，你还需要进行后续操作。首先，这只是导出的目录默认集。你需要使用 `exports -a` 命令来激活它们。下一次启动 Ubuntu Linux 时，NFS 内核服务器启动脚本（`/etc/init.d/nfs-kernel-server`）会自动运行 `exports -r` 命令，该命令会同步导出的目录。

当你向 `/etc/exports` 添加共享时，`exports -r` 命令会添加新目录。然而，如果你正在修改、移动或删除共享，最安全的方法是在使用 `exports -a` 命令重新导出共享之前，先用 `exports -ua` 命令临时取消挂载所有文件系统。

一旦导出激活，它们就很容易检查。只需在服务器上运行 `showmount -e localhost`。如果你在查找远程 NFS 服务器的导出列表，例如，`showmount -e enterprise5` 会查找来自 `enterprise5` 计算机导出的 NFS 目录列表。

## 从命令行挂载 NFS 目录

在进行任何复杂操作之前，你应该从 Linux 或 Unix 客户端测试共享的 NFS 目录。但首先，你应该检查共享 NFS 目录列表。如果你在 NFS 服务器上并想检查本地列表，命令是：

```
$ showmount -e localhost
```

如果你没有看到共享目录列表，请检查本章早些描述的步骤。确保你已经配置了 `/etc/exports` 文件。记得导出共享目录。如果你没有在 NFS 系统上启动 `nfs-kernel-server` 和 `portmap` 守护进程，你的 NFS 服务器将无法为远程工作。如果你在远程 NFS 客户端计算机上，并想查看来自 `ubuntuserver1` 计算机的共享目录列表，请运行以下命令：

```
$ showmount -e ubuntuserver1
```

如果不作用，有几点需要检查：防火墙以及 `/etc/hosts` 或 DNS 服务器。如果权威 `/etc/hosts` 或 DNS 服务器存在问题，请替换为 NFS 服务器的 IP 地址。你将看到类似下面的输出：

```
Export list for ubuntuserver1
/home/michael *
```

现在要在本地挂载此目录，你需要一个空的本地目录。根据需要，创建一个如 `/mnt/remote` 的目录。然后你可以从 `ubuntuserver1` 挂载共享目录：

```
$ mount -t nfs ubuntuserver1:/home/michael /mnt/remote
```
