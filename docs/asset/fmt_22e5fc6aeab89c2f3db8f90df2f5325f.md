
http://www.tru64unix.compaq.com/internet/osis.htm

# 20.9 参考文献

- TruCluster 服务器集群管理指南
- TruCluster 服务器技术概览
- Tru64 UNIX 系统管理指南
- Tru64 UNIX 网络管理指南 (V5.0A 和 V5.1)
- Tru64 UNIX 网络管理指南：服务 (V5.1A)
- Tru64 UNIX V5.1A 版本发布说明
- Tru64 UNIX 5.1A 和 TruCluster 服务器 5.1A：补丁包-0001 补丁摘要和发布说明
- Tru64 UNIX 参考页（文中已注）。
- Tru64 UNIX 系统管理员指南 – Cheek, Fafrak, Hancock, Moore, Yates (Digital Press, ISBN: 1-55558-255-9)。

# 集群管理任务

在构建集群后，需要实施某些管理任务以确保系统运行顺畅。其中一些任务涉及监控集群的行为；另一些则更为复杂，涉及更改集群的行为。了解作为系统管理员好朋友的守护进程的行为是有好处的，这样你就能知道检查哪些进程并保持它们持续运行。

在本章中，我们将涵盖以下内容：

- 集群管理 GUI 21.1
- 移动 /tmp 文件系统 21.2
- 将交换分区移动到本地磁盘 21.3
- 负载均衡 CFS 服务器 21.4
- 配置 21.5
- 集群范围内的 cron 21.6
- 关键服务守护进程 21.7
- 重要的文件和信息 21.8
- 集群命令总结 21.9

## 21.1 集群管理 GUI

有一个良好的图形用户界面 (GUI)，系统管理员可以使用它来监控管理集群。这类工具在集群中特别有用，因为它们展示了硬件、文件系统或其他集群组件。启动此 GUI 非常简单。从图形显示设备启动 SysMan。

```
$ sysman -station
```

或

```
$ sms
```

这启动了类似于下面的窗口：

![](img/81b06a4c1716280bf493aad27d10_0)

图 21-1: SysMan 主界面

如图 21-1 所示，主界面显示类别的“正常”或“异常”。如果某个类别不是带勾选的绿色框，你可以双击它查看是黄色还是红色。由于这不是颜色的，图 21-2 描述了你在查看主界面时可能看到的图标。例如，通过选择磁盘，你可以修改磁盘、创建 AdvFS 域，或启动事件查看器以查看与磁盘相关的任何事件，如 21-4 所示。

| 绿色 | 表示一切正常。 |
| 黄色 | 表示潜在问题，已发生事件。 |
| 红色 | 表示发生了严重问题。 |

图 21-2: SysMan 颜色/图标描述

![](img/81b06a4c1716280bf493aad27d611_0)

图 21-3: SysMan 硬件视图

![](img/81b06a4c1716280bf493aad27d611_1)

图 21-4: SysMan 弹出菜单

SysMan Station 可以显示多个视图，正如你可能猜到的那样，硬件视图是最有用的之一。我们不会查看每一个视图，另一个特别好用的是 physical_filesystems 视图，如图 21-5 所示。

此视图列出了各种挂载的文件系统及其对应的 CFS 服务关系。如果你想管理 CFS 配置，可以从此处启动 CFS 管理器并更改文件系统的 CFS 服务器。此外，你可能希望监控在集群生命周期内 CFS 关系如何以及何时发生了变化。

![](img/81b06a4c1716280bf493aad27d612_0)

图 21-5: SysMan 物理文件系统视图

## 21.2 移动 /tmp 文件系统

系统管理员经常希望将 `/tmp` 文件系统移动到集群成员的本地驱动，或者移动到其他地方以提高文件系统性能。移动 `/tmp` 的另一个原因是用户可能会通过向 `/tmp` 写入数据来填充根文件系统。创建一个独立的文件系统可以消除这种可能性。

### 21.2.1 在本地磁盘上创建 /tmp

首先，在目标磁盘/分区上创建 AdvFS 域和文件集。

```
# mkfdfn /dev/disk/dsk21c gilligan_tmp
```

```
# mkfset gilligan_tmp tmp
```

然后修改 `/etc/fstab` 文件以包含此挂载项。

```
gilligan_tmp#tmp    /cluster/members/member2/tmp  advfs rw 0 0
```

你可以通过执行 `clu_get_info(8)` 命令来验证 gilligan 确实是 member2。

```
[gilligan]
# clu_get_info -m 2
Cluster memberid = 2
Hostname = gilligan.alf.cpqcorp.net
Cluster interconnect IP name = gilligan-mc0
Member state = UP
```

现在，当 gilligan 启动时，由于它对 `dsk21` 有访问权限，它将能够挂载文件系统。任何其他成员将无法挂载该文件系统，但这完全没有关系。

### 21.2.2 在共享总线磁盘上创建 /tmp

另一种可能性是在恰好位于共享总线的磁盘上创建 `/tmp`。再次像上述方法一样创建域并向 `/etc/fstab` 文件添加条目。如果你希望 `/tmp` 仅对使用它的成员可见，可以使用 `mount(8)` 命令配合 `"o server_only"` 参数来挂载文件系统。这并不是必须，但可能是理想的，尽管文件系统位于共享资源上，它的行为也会像本地总线示例一样。

## 21.3 将 Swap 移动到本地磁盘

将 `/tmp` 移动到本地或备用位置是一个相当简单的操作，移动 swap 也是如此。你需要做的是修改 `/etc/sysconfig` 文件，列出你预期的交换分区：

```
vm:
swapdevice=/dev/disk/dsk15b, /dev/disk/dsk3b
```

如果你正在添加额外的交换空间，请执行 `"swapon -a"`。如果你正在替换主交换空间，将需要重启以使更改生效，因为你无法从操作系统中强行拔掉交换分区。需要注意的是，将交换空间移动到本地磁盘有助于性能并减少到共享总线的 I/O，但它也会使交换分区更容易受到控制器问题的影响。如果 swap 被移动到本地分区且该路径发生故障，可能会导致系统挂起或崩溃（panic）。如果 swap 分区在共享磁盘上，只要至少有一个成员访问数据，你就不会遇到这个问题。在共享磁盘上拥有 swap 的另一个用处是，如果成员崩溃且由于某种原因无法启动，崩溃转储（crash dump）可以由另一个集群成员处理，并可以在原始成员重启之前开始崩溃分析。如果我们知道 `disk6` 是另一个成员的交换分区，且该分区足够大以容纳崩溃转储，我们就可以处理该转储并创建所需的 `vmunix.0` 和 `vmcore.0` 文件（如果我们愿意，还可以从这些文件创建 `crash-data.0`）。

```
# /sbin/savecore -d /dev/disk/disk6b
System went down at Jun 27 23:11:13 2002
Saving 23949312 bytes of image in vmcore.0
```

```
/usr/bin/crashdc vmunix.0 vmcore.0 > crash-data.0
```

```
# ls
crash-data.0  vmunix.0  vmcore.0
```

要查看当前配置的 swap，请执行 `"swapon -s"` 命令：

```
# swapon -s
Swap partition /dev/disk/disk16b (default swap):
  Allocated space:      211639 pages (1.61GB)
  In-use space:        129 pages ( 0%)
  Free space:           211510 pages ( 99%)
Swap partition /dev/disk/disk4b:
  Allocated space:      124063 pages (969MB)
  In-use space:        129 pages ( 0%)
  Free space:           123934 pages ( 99%)
Total swap allocation:
  Allocated space:      335702 pages (2.56GB)
  Reserved space:       11873 pages ( 3%)
  In-use space:        258 pages ( 0%)
  Available space:     323829 pages ( 96%)
```
