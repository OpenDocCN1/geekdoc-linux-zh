
像往常一样，测试安装以确保一切正常工作。当 Windows 95/98 PC 连接到 Samba 打印机共享时，你会看到一个请求安装打印程序的屏幕对话框（图 15.7）。

这应该安装打印机驱动程序。如果没有，请检查拼写错误和明显的错误。你也应该能够打印到共享打印机。如果没有，请使用本章之前使用的故障排除步骤。

# 第 16 章 在 Linux 和 Windows 中使用 NFS 和 NIS

NFS 是原生的 UNIX 协议，允许 UNIX 机器通过网络共享驱动器。它执行了微软 SMB 协议的一些功能。NFS 是一个简单得协议，因为它不包含身份验证和打印功能。身份验证由 UNIX（或 Linux）主机处理，打印功能由 `lpr` 和 `lpd` 处理。

NFS 是混合网络的一个良好协议。它不仅用于 Linux 和所有其他形式的 UNIX，还适用于所有主要的操作系统，包括大型机、中型机和 PC 的操作系统。它比 SMB 简单得多，因此使用的系统和网络资源更少。它不是持久连接，这意味着如果 NFS 客户端失去了与 NFS 服务器的联系，它将在服务器上线时重新连接。

Linux 内核中拥有（内置的）NFS 支持，以及管理 NFS 的工具。NFS 允许 Linux 机器与另一台机器共享驱动器或目录（作为服务器）。它允许 Linux 机器在其他机器上挂载驱动器（作为客户端）。

Windows 不支持 NFS，但有许多第三方程序为 Windows 添加 NFS 支持。将 Windows 机器连接到机器的方法有两种：一种是在每台 Windows 机器上加载 NFS 程序；另一种是使用一台机器作为 NFS 机器和 Windows 机器之间的网关。这些程序和方法将在本章稍后讨论。

## 16.1 设置 Linux 为 NFS 服务器

将 Linux 设置为 NFS 服务器将允许你共享 Linux 机器上的驱动器和目录。虽然 Linux 发行版包含了 NFS 支持，但仍然需要进行设置。

需要做的第一件事是启动 `portmap` 服务。大多数发行版默认启动 `portmap`。要查看 `portmap` 是否已启动，输入：

```
rpcinfo -p

program vers proto port

100000 2 tcp 111 portmapper

100000 2 udp 111 portmapper
```

你应该能看到 `portmapper` 连接到 `tcp` 和 `udp` 端口。如果 `portmapper` 未启动，你需要将其添加到 `init` 脚本中。你可能需要检查手册或参考书查看如何这样做，因为这随发行版而异。`portmapper` 程序名为 `portmap`、`rpc` 或 `rpcbind`，位于 `/sbin` 或 `/usr/sbin` 目录。`init` 脚本位于 `/etc/rc.d`、`/etc/init.d` 或 `/etc/rc.d/init.d`。

例如，在 Red Hat Linux 发行版中，你会将脚本 `portmap` 添加到 `/etc/rc.d/init.d` 目录。Red Hat 自带的 `portmapper` 脚本如下：

```bash
#! /bin/sh

# portmap          Start/Stop RPC portmapper

# chkconfig: 345 11 89

# description: The portmapper manages RPC connections, which are used by \
#               protocols such as NFS and NIS. The portmapper server must be \
#               running on machines which acts as servers for protocols \
#               make use of the RPC mechanism.
```

## 16.2 在 Linux 上使用 NFS 客户端

这是一个对 NFS 的非常简单的解释，涵盖了基础知识。有整本书都在专门介绍 NFS 的细节。

为了让 NFS能够工作，内核中必须构建 NFS 支持。大多数发行版都已经在内核中内置了 NFS 支持。如果没有，则需要通过重新编译内核或添加 NFS 内核模块来添加 NFS 支持。如前所述，重新编译内核超出了本书的范围。有很多书籍提供了关于编译内核的详细介绍，或者你可以访问 `http://www.ibiblio.org/mdw/HOWTO/Kernel-HOWTO.html` 了解有关编译内核的详情。

一旦在内核中激活了 NFS，就可以直接使用 `mount` 命令来访问远程 NFS 驱动器：

```
mount -o rsize=4096,wsize=4096 mmcune:/mnt/home/alisa /mnt/alisa
```

当然，你必须是 `root` 或等效用户才能使用 `mount` 命令。让我们来看这些参数的含义：

- `-o` 表示有可以跟随的选项。
- `rsize`—以字节为单位的读缓冲区大小。
- `wsize`—以字节为单位的写缓冲区大小。
- `mmcune`—NFS 服务器的名称。
- `/mnt/home/alisa`—服务器上的 NFS 目录。
- `/mnt/alisa`—挂载 NFS 目录的本地目录。

### 16.2.1 优化 NFS

可以对 `rsize` 和 `wsize` 参数进行优化以获得更高的速度。遗憾的是，唯一的方法是不断尝试。通常情况下，`rsize` 和 `wsize` 应该在不牺牲可靠性的情况下尽可能大。大多数时候，保持这些值的默认值更好。

优化 `rsize` 和 `wsize`。从 `rsize` 和 `wsize` 为 `1024` 开始，观察拷贝一个大文件（64MB 或更大）需要多长时间。重复几次并取平均时间。然后将 `rsize` 和 `wsize` 的值各增加 `1024`，并重复此过程，直到两个值都达到 `16,384` 字节。

在确定了这些值的最佳大小后，我们需要确保它们是可靠的。这相当难以察觉到。尝试运行几个命令。然后尝试大文件。如果程序在没有错误消息的情况下终止或失败，那么说明 `rsize` 和 `wsize` 太大，需要调小。大多数 Linux 系统在 `rsize` 和 `wsize` 均为 `4096` 时性能最佳，尽管你的结果可能会有所不同。

### 16.2.2 硬挂载与软挂载

NFS 如何处理连接丢失同样重要。有硬挂载（hard mounts）和软挂载（soft mounts）。软挂载会向访问 NFS 卷的程序发送错误。某些程序可以处理这种情况，但大多数不能。

在大多数情况下，硬挂载是更好的选择。它会挂起任何访问 NFS 挂载的程序。它通过 `intr` 选项添加，该选项会停止使用 NFS 挂载的程序。在大多数情况下，硬 `intr` 是最佳选项。

一旦确定了各种选项，就可以将其添加到 `fstab`。`fstab` 是 Linux 中定义驱动器参数的地方。`fstab` 条目按此顺序排列，用空格分隔：驱动器、挂载点、文件系统类型、逗号分隔的选项、dump 和 fsck 顺序。例如：

```
mmcune:/mnt/home/alisa  /mnt/alisa  nfs
size=4096,hard,intr 0
```
