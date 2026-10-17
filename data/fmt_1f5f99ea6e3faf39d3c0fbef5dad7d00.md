
`************ (end of perfstat -v output) *************`

# 第 13 章

## 网络

### 虚拟分区与网络

每个虚拟分区至少应配备一张专用网络卡。vPar 将通过网络卡与其他 vPar 及其他系统进行通信。与所有组件一样，不同虚拟分区中的网络卡是相互独立管理的，并且与其所附着的虚拟分区也是独立管理的。在接下来的章节中，我们将对虚拟分区的网络卡和整体网络进行一些基本操作。我们将查看网络卡的配置，以及虚拟分区如何通过网络相互通信——即使这些 vPar 运行在同一系统上也是如此。

要在同一系统上运行的两个虚拟分区之间执行如 `telnet` 或 *文件传输协议* 等基本任务，您需要使用它们的网络卡。没有允许 vPar 之间通过背板而非通过各自 vPar 的网络卡进行通信的低级 vPar 专用功能。

![](img/eff8b9287a5f38c5adf538f24aacf29e_849_0.png)

### 虚拟分区的主机相关信息

虚拟分区的一个方面可能会让人困惑，即与每个虚拟分区相关的主机信息。虚拟分区从所有实际用途上来说都是不同的主机。这意味着，连接到某个虚拟分区的系统认为它与运行在同一服务器上的任何其他虚拟分区都是完全独立的主机。因此，对于每个虚拟分区，您既有定义该虚拟分区的信息，也有定义主机的信息。从网络角度来看，例如使用 `telnet` 连接到虚拟分区时，您会使用主机名。从虚拟分区角度来看，例如执行 `vparstatus` 等 VPar 命令时，您会使用 VPar 名称。最好让这两个名称保持一致，这样您就可以使用同时定义 VPar 和主机名的一个名称来执行任何命令。

在我们第 2 章的早期示例中，我们在两个单独的磁盘上加载了 HP-UX 11i，每个磁盘将用于一个单独的虚拟分区。在为各自的虚拟分区加载操作系统时，您可以在加载操作系统时指定主机相关信息。例如，在加载 HP-UX 11i 时，您可以输入主机名和其他系统相关信息。每个 HP-UX 11i 实例的此信息是不同的，因为即使虚拟分区运行在同一物理服务器上，11i 的实例用于不同的虚拟分区。虚拟分区实际上是不同的主机，因此将具有不同的系统相关参数。在 HP-UX 11i 安装完成后，或者在虚拟分区启动并运行后，可以使用 `set_params` 更改每个虚拟分区的主机相关信息。

![](img/eff8b9287a5f38c5adf538f24aacf29e_849_1.png)

对于习惯只使用一个 HP-UX 实例和因此只有一组主机相关信息的服务器 Unix 用户来说，一台物理计算机上有多个主机的概念可能需要一点时间才能适应。

虚拟分区相关信息，如名称，可以使用 `vparmmodify` 进行修改。主机相关信息使用 `set_params` 进行更新（或通过手动更新相应的文件）。因此，对于每个虚拟分区，您既有定义该虚拟分区的信息，也有定义主机的信息。

让我们使用 `vparstatus` 查看两个虚拟分区，以查看这两个 VPar 的 LAN 接口对应的 I/O 地址：

```
# vparstatus -v

[Virtual Partition Details]
Name:  cable1
State:  Up
Attributes:  Dynamic,Manual
Kernnel Path:  /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:  2/3
Bound [Path]:  33
        37
Unbound [Path]:

[IO Details]
    2.9.2.1.2.0  BOOT
    2.5.4.0  CONSOLE
    0.0.0.0                <-- LAN for cable1
    0.7.1.0.3.0

[Memory Details]         *
Specified [Base  /Range]:
        (bytes) (MB)
Total Memory (MB):  2048

[Virtual Partition Details]
Name:  cable2
State:  Up
Attributes:  Dynamic,Manual
Kernnel Path:  /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max:  1/2
Bound [Path]:  97
Unbound [Path]:  101

[IO Details]
    0.8.0.0.0.0.5.0.0.0, BOOT
    0.10.0.0          <-- LAN for cable2

[Memory Details]
Specified [Base  /Range]:
        (bytes) (MB)
Total Memory (MB): 1024
```

这两个硬件路径对应于不同的本地总线适配器（LBA），这是撰写本文时的要求。第一个 vPar 使用 LBA 0 上的 Core I/O 卡，第二个 vPar 使用 LBA 10。现在让我们继续查看这两张卡的软件配置。

我们在第 2 章的许多示例中大量使用了名为 *cable1* 的 vPar。以下内容显示了 vPar *cable1* 上 `/etc/hosts` 文件的内容：

```
# cat /etc/hosts
# @(B)B,i1.i1_LRhosts $Revision: 1.9.214.1 $ $Date: 96/10/08
13:20:01 $
#
# The form for each entry is:
# <internet address>	<official hostname>	<aliases>
#
# For example:
# 192.1.2.34	hpcrm loghost
#
# See the hosts(4) manual page for more information.
# Note: The entries cannot be preceded by a space.
#	The format described in this file is the correct format.
# The original Berkeley manual page contains an error in
# the format description.
#
172.16.15.36	cvhdccon3
172.16.14.44	cvhdccon4
127.0.0.1	localhost	loopback
#
```

此文件中未提及 vPar 名称 *cable1*。就 HP-UX 而言，*cvhdccon3* 的主机名是该主机和此虚拟分区所需的全部信息。该系统上运行的第二个 vPar 的主机名是 *cvhdccon4*。这两个主机之间的通信是通过网络电缆使用 `/etc/hosts` 中显示的两个主机名进行的。`/etc/hosts` 文件中不存在 vPar 名称。所有与 vPar 相关的信息都在 `/etc/vpdb` 中。如果您的 *主机名* 和虚拟分区名称确实不同，您可能希望添加 vPar 名称的别名。您可以为 *cable1* 在 `/etc/hosts` 文件中添加 *cvhdccon3* 的别名，并为 *cable2* 添加 *cvhdccon4* 的别名。

现在让我们在两个主机上运行 `iconfig`，以查看网络接口是如何设置的：

请注意，第一个 vPar 的 LAN 接口为 *lan0*，第二个为 *lan1*。该服务器有两个 LAN 接口，尽管它们属于不同的 vPar 和 HP-UX 实例，但为了让服务器能够区分这两个接口，需要使用两个不同的 LAN 接口名称；我们将在接下来的 `netconf` 文件中看到这一点。

与主机相关的信息存储在 `/etc/rc.config.d/netconf` 中。以下列表显示了与 *cvhdcn3* 相关的信息，同样没有提及 vPar 名称 *cable1*：

# 主机 cvhdcn3 (vPar cable1) 上的 netconf
