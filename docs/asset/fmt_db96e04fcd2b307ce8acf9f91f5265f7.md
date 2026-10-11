
如果您需要的信息不在缓存内存中，而是在 RAM 中，那么访问将花费更长的时间。所有内存的速度都在增加，而 RAM 的速度增加得特别快。您对 RAM 的使用方式有很大控制权。首先，您可以决定系统中配置了多少 RAM。整个 HP 产品线，无论是工作站还是服务器系统，都支持比系统实际需要的更多的 RAM。

截至本文撰写之时，RAM 价格低廉，且成本还在持续下降。在配置系统时，RAM 不是应该省钱的地方。此外，你可以高效地利用已配置的所有 RAM。一个示例是配置高效的 HP-UX 内核。HP-UX 内核始终加载在 RAM 中。这意味着如果它比你的需求大了 2 或 3 MB，那么你就失去了 2 或 3 MB 用于其他用途的空间。如果你需要访问 RAM 中的某些信息，其访问速度将比在缓存（`cache`）中慢大约一个数量级。

### 虚拟内存

如果你的系统只有缓存和，比方说，64 MB 的 RAM，那么你就只能运行消耗约 64 MB 物理内存的用户进程。利用内存管理，你可以使用虚拟内存来运行远超物理内存大小的用户进程。虚拟内存允许你仅将进程的一部分加载到 RAM 中，而将其余部分保留在磁盘上。你在内存和磁盘之间以页（`pages`）为单位来回移动数据块。

### 交换区（Swap）

`Swap` 用于扩展内存大小，即在磁盘上预留一块区域作为 RAM 的扩展。当系统负载较高时，交换区空间用于容纳那些在物理内存中没有可用空间的部分或全部进程。HP-UX 通过 `vhand`、`statddaemon` 和 `svapper` 进程为你处理所有这些交换操作。你需要确保磁盘上预留了足够的交换区空间，以便内存管理能够进行而不会耗尽交换区空间。

存在三种类型的交换区空间：主交换区、次交换区和文件系统交换区。如下所述：

- **主交换区（Primary swap）**：在启动时可用的交换区。主交换区位于与根文件系统相同的磁盘上。如果这个主交换区出现问题，你可能会很难引导系统。
- **次交换区（Secondary swap）**：位于根磁盘以外的其他磁盘上的交换区。
- **文件系统交换区（File system swap）**：这是一种既支持文件和数据结构，又支持交换操作的文件系统。

不要过于纠结于配置交换区的大小。最低限度，交换区应该是物理内存大小的两倍（这是安装过程的默认大小）。此外，我们的主要应用程序将定义所需的交换区数量。我接触过的应用程序大多会明确说明应用程序所需的最大交换区数量。如果你正在运行多个应用程序，并且它们将同时运行，请累加每个应用程序所需的交换区数量。

# 第 6 章

## 用户和组

## 虚拟分区与用户

每个虚拟分区（Virtual Partition）就像一个独立的服务器。这意味着你在各自的虚拟分区中有独立的用户。需要在虚拟分区之间共享的任何用户相关信息，将以与在物理上分离的服务器之间共享相同的方式进行。例如，你可能希望用户有能力从一个虚拟分区远程登录到另一个虚拟分区。你可以通过在每个虚拟分区中设置适当的网络文件来实现这一目标，就像在独立的服务器上那样（有关网络的详细信息，请参见第 13 章）。图 6-1 展示了虚拟分区与用户之间的关系：

![](img/eff8b9287a5f38c5adf538f24aacf29e_395_0.png)

**图 6-1** 虚拟分区和用户

如图 6-1 所示，每个虚拟分区都有自己的操作系统实例和用户集。从软件角度看，vPar 是隔离的，因此用户似乎存在于不同的服务器上。为了在用户之间共享信息，例如用户数据库，你可以实现诸如网络信息系统（NIS）等技术。使用 NIS，你可以创建一个共享于不同系统之间的用户信息数据库，在这种情况下，即不同的 vPar，因为从软件角度来看，它们等同于不同的服务器。

现在让我们在每个 vPar 上创建一个新用户。在 *cable1* 上，我们将创建用户 *cable1us*，并验证该用户不存在于 *cable2* 上。在 *cable2* 上，我们将创建用户 *cable2us*，并验证该用户不存在于 *cable1* 上。有关创建用户的详细信息，请参阅本章的背景部分。

图 6-2 展示了在 vPar *cable1* 中使用系统管理经理（SAM）创建用户 *cable1us* 的屏幕截图：

![](img/eff8b9287a5f38c5adf538f24aacf29e_396_0.png)

**图 6-2** 在 SAM 中创建 *cable1us* 用户

图 6-2 显示了 *cvhdccon3* 的主机名，这是对 vPar *cable1* 服务器名称的对应。

用户 *cable1us* 是在 vPar *cable1* 中创建的，并且仅存在于 *cable1* 中。我们将很快验证这一点。我们使用 SAM 在 vPar *cable2* 中创建用户 *cable2us* 时执行了相同的程序。

现在，*cable1* 中应该有一个用户无法在 *cable2* 中查看，反之亦然。以下显示了连接到 *cable1* 并列出 `/etc/passwd` 内容的过程。

```bash
cvhdccon3:/ # cat /etc/passwd
root:*:hiIXKsAzUIPy6:0:3:::/sbin/sh      cable1 listing
daemon:*:*:1:5:::/sbin/sh
bin:*:*:2:2::/usr/bin:/sbin/sh
sys:*:*:3:3::/
adm:*:*:4:4::/var/adm:/sbin/sh
uucp:*:*:5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp:*:*:9:7::/var/spool/lp:/sbin/sh
nuucp:*:*:11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb:*:*:27:1:ALLBASE::/sbin/sh
nobody:*:*:-2:-2::/
www:*:*:30:1::/
webadmin:*:*:40:1::/usr/obam/server/nologindir:/usr/bin/false
snmbull:*:*:101:101:Do not USE or DELETE - needed by Samba:
        /home/snmbull:/sbin/sh
opc_op:*:*:777:777:OPC DEFAULT OPERATOR:/home/opc_op_op:/sbin/sh
Cable2us:*:102:20:::/home/Cable2us:/usr/bin/sh  <-- cable2us
cvhdccon3:/ #
```

`cable1` 的这个列表表明，`cable1us` 存在于 `cable1` 上的 `/etc/passwd` 文件中；然而，此文件中没有 `cable2us`。以下显示了连接到 `cable2` 并列出 `/etc/passwd` 内容的过程。

```bash
# cat /etc/passwd
root: * :X6GAMrnH.aBs:0:3:::/sbin/sh      cable2 listing
daemon: * : * :1:5:::/sbin/sh
bin: * : * :2:2::/usr/bin:/sbin/sh
sys: * : * :3:3::/
adm: * : * :4:4::/var/adm:/sbin/sh
uucp: * : * :5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp: * : * :9:7::/var/spool/lp:/sbin/sh
nuucp: * : * :11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb: * : * :27:1:ALLBASE::/sbin/sh
nobody: * : * :-2:-2::/
www: * : * :30:1::/
webadmin: * : * :40:1::/usr/obam/server/nologindir:/usr/bin/false
sam_exec: xxx: 0: 1::/home/sam_exec:/usr/bin/sh
Cable2us: * :101: 20::/home/Cable2us:/usr/bin/sh      <-- cable2us
#
```

`cable2` 的这个列表表明，`cable2us` 存在于 `cable2` 上的 `/etc/passwd` 文件中；然而，此文件中没有 `cable1us`。

该列表表明，各自 vPar 的唯一用户仅存在于其创建的 vPar 上。此外，每个 vPar 都有自己的 `root` 和其他系统级用户。

接下来，让我们看看 vPar 中单个用户的设置信息。

### 单个用户设置
