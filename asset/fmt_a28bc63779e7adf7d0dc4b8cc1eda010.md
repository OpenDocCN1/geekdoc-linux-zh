
你可能注意在执行 `mkramfs` 命令时，列表 9-10 中关于组 ID (GID) 的警告信息。`cramfs` 文件系统使用非常精简的元数据来缩小文件系统大小并提高执行速度。`cramfs` 文件系统的“特征”之一是将组 ID 字段截断为 8 位。Linux 使用的是 16 位组 ID 字段。结果是，用大于 255 的组 ID 创建的文件会被截断，并发出列表 9-10 中的警告。

尽管在文件大小、文件最大数量等方面存在局限性，但 `cramfs` 文件系统对于启动 ROM 来是理想的，因为只读操作和快速压缩是其理想的特征。

## 9.8 网络文件系统 (NFS)

如果你在 UNIX 环境下开发过，你无疑对网络文件系统 (`NFS`) 非常熟悉。配置得当，`NFS` 允许你在 `NFS` 服务器上导出目录，并将该目录挂载到远程客户端机器上，就像本地文件系统一样。这在大型 UNIX/Linux 机器网络中非常有用，可以是嵌入式开发者的万灵药。通过在目标板上使用 `NFS`，嵌入式开发人员可以在开发调试期间访问大量的文件、库、工具和实用程序，即使嵌入式系统资源受限。

与其他文件系统一样，你的内核必须配置 `NFS` 支持，包括服务器端和客户端功能。`NFS` 服务器和客户端功能在内核配置中是独立配置的。

配置和调优 `NFS` 的详细说明超出了本书的范围，但简短的介绍将有助于说明 `NFS` 在嵌入式环境开发期间有多用。请参本章中的章节以获取有关 `NFS` 详细信息的索引，包括完整的 `NFS` 使用指南。

在启用了 `NFS` 的开发工作站上，一个配置文件包含了一个指定你想要通过网络文件系统导出的目录列表。在 Red Hat、Ubuntu 和大多数其他发行版中，该文件位于 `/etc` 目录并命名为 `exports`。列表 9-12 是一个 `/etc/exports` 示例，可能会在嵌入式开发的工作站上找到。

### 列表 9-12 /etc/exports 的内容

```bash
$ cat /etc/exports

# /etc/exports

/coyote-target * (rw,sync,no_root_squash,no_all_squash,no_subtree_check)

/home/chris/workspace * (rw,sync,no_root_squash,no_all_squash,no_subtree_check)

$
```

该文件包含了 Linux 开发工作站上两个目录的名称。第一个目录包含一个用于 ADI Engineering Coyote 板板的目标文件系统。第二个目录是一个通用工作区，包含了针对嵌入式系统的项目。这些是随机的，你可以以任何方式配置 `NFS`。

### 9.8.1 NFS 上的根文件系统

当目标系统资源受限时，将你的项目挂载到目标机非常有用。当你对项目进行更改时，这特别有用。对于开发目的，如果你的嵌入式系统加载了你在 Linux 工作站上熟悉的全部工具和实用程序，它可以极大提高生产力。事实上，几十种命令行工具和开发实用程序可以帮助缩短开发进度。

配置嵌入式系统在启动时通过 `NFS` 挂载根文件系统相对简单。首先，你必须为目标内核配置 `NFS` 支持。还有一个配置选项用于启用挂载 `NFS` 远程目录。这如图 9-3 所示。

图 9-3 内核配置

### 列表 9-13 目标文件系统摘要

```bash
$ du -h --max-depth=1

724M /usr

4K /opt

39M /lib

12K /dev

27M /var

3.6M /boot

4K /workspace

1.8M /etc

4K /home

4K /mnt

4K /root

29M /bin

32M /sbin
```

### 列表 9-13 续

```bash
64K ./share

855M .

$ find -type f | wc -l

29430
```

剩下的就是以某种方式将信息传递给内核，以便它知道去哪里寻找 `NFS` 服务器。可以使用几种方法来实现这一点；其中某些取决于所选的架构和启动加载程序。至少，可以在上电时通过内核命令行向内核传递适当参数，以配置其 IP 端口和服务器信息。一个典型的内核命令行可能如下所示：

```
console=ttyS0.115200 ip=boot root=/dev/nfs
```

这告诉内核期望通过 `NFS` 根文件系统，并从 `BOOTP` 服务器获取参数（服务器名称、服务器 IP 地址和要挂载的根目录）。这在项目开发阶段是一种常见且极其有用的配置。如果你在静态地配置目标机的 IP，你的内核命令行可能如下：

```
console=ttyS0.115200                               \
ip=192.168.11.139:192.168.11.1:255.255.255.0:coyetel:eth0:off \
nfsroot=192.168.11.11::coyote-target \
root=/dev/nfs
```

当然，这应该是一行。`ip=` 参数定义在 `Documentation/files/nfsroot.txt` 中，并具有如下单行语法：

```
ip=<client-ip>:<server-ip>:<gw-ip>
:<netmask>:<hostname>:<device>:<autoconf
```

在这里，`client-ip` 是目标地址；`server-ip` 是 `NFS` 服务器的地址；`gw-ip` 是网关（路由器），以以防服务器位于不同的子网；`netmask` 定义 IP 地址的类别。`hostname` 是作为目标主机传递的字符串；`device` 是 Linux 设备名称，例如 `eth0`；`autoconf` 定义用于初始化 IP 参数的协议，例如 `BOOTP` 或 `DHCP`。将其设置为 `off` 则不进行配置。

## 9.9 伪文件系统

在内核配置菜单中，许多文件系统归属于“伪文件系统”（Pseudo File Systems）类别。它们提供了一系列广泛应用于应用程序中的设施。有关更多信息，特别是关于 `/proc` 文件系统，可以花一个下午时间研究这个实用的设施。在本章的最后一节可以找到额外阅读的参考文献。

### 9.9.1 /proc 文件系统

`/proc` 文件系统的命名源于其原始用途：一个允许内核通信 Linux 系统上每个运行进程信息的接口。随着时间的推移，它已经成长并成熟，提供了比进程信息多得的内容。我们在这里介绍亮点：`/proc` 文件系统的完整介绍留给你们作为练习。

`/proc` 文件系统已成为所有简单的、嵌入式 Linux 系统的虚拟必需。许多用户级函数依赖 `/proc` 文件系统的内容来工作。例如，不带任何参数执行的 `mount` 命令会根据 `/proc/mounts` 提供的信息列出运行系统上的所有当前挂载点。如果 `/proc` 文件系统不可用，`mount` 命令将静默返回。列表 9-14 展示了在 ADI 工程开发板上的这种情况。

列表 9-14 挂载对 /proc 的依赖

```
# mount

roots on / type roots (rw)

/dev/root on type nfs

(rw,v2,size=4096,hard,udp,nolock,addr=192.168.11.19)

tmpfs on /dev/shm type tmpfs (rw)

/proc on /proc type proc (rw,nodiratime)

< 现在卸载 proc 并重试 ...>
```

```
/proc
# mount
#
```

注意列表 9-14，`/proc` 本身被列为一个已挂载的文件系统，其类型为 `proc` 且挂载在 `/proc` 上。这不是双关语；你的系统在顶层目录树中必须有一个名为 `/proc` 的挂载点，作为 `/proc` 文件系统的挂载目标。要挂载 `/proc` 文件系统，像挂载任何其他文件系统一样使用 `mount` 命令：

```
# mount -t proc /proc /proc
```

> 你可以在文件系统的任意任何地方挂载 `/proc`，但所有需要 `proc` 的实用程序（包括 `mount`）都期望发现它挂载在 `/proc` 上。

根据 man 帮助页，`mount` 命令的一般形式为：

```
mount [-t ftype] somewhere
```

在前面的调用中，我们可以将 `/proc` 替换为 `none`，如下所示：

```
mount -t proc none /proc
```
