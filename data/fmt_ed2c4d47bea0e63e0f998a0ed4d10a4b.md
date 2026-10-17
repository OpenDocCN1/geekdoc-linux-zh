
`securenets` 的每一行列出了映射和 IP 地址。以下是 `/etc/ypserv.conf` 的某些选项示例：

本文档由未注册的 Chmag 创建，请访问 `http://www.bisenter.com` 进行注册。感谢。

分发。当你在主服务器上运行 `ypbind` 时，`ypcalls` 执行：你不需要手动重新制作。

编辑 `var/yp/Makefile` 以设置选项并指定要创建哪些映射。后续章节将详细讨论 `var/yp/Makefile`。

## 变量

以下是可以在 `/var/yp/Makefile` 中设置的变量列表。`Red Hat` 单词后的值是 `Red Hat` 分发的文件中设置的值。

### B

不要更改。

`Red Hat`: 未设置

### NOPUSH

指定 `ypserv` 不将映射复制（推送）到从用服务器。如果你没有任何从用 NIS 服务器，请将其设置为 `TRUE`；设置为 `FALSE` 则会导致 NIS 将映射复制到从用服务器。

`Red Hat`: `TRUE`

### MINUID, MINGID

指定包含在 NIS 映射中的最低 UID 和 GID 数字。在 `etc/passwd` 和 `etc/group` 文件中，较小的 ID 编号属于 `root` 以及系统账户和组。为了增强安全性，NIS 不会发布这些用户和组的密码及组信息。将 `MINUID` 设置为你想包含在 NIS 映射中的最低 UID，并将 `MINGID` 设置为你想包含的最低 GID 数字。

`Red Hat`: `500/500`

### NFSNOOBODYUID, NFSNOOBODYGID

指定名为 `nfsnobody` 的用户的 UID 和 GID。NIS 不导出此用户的值。设置为 `0` 以导出 `nfsnobody` 的映射。

`Red Hat`: `65534/65534`

### MERGE_PASSWD, MERGE_GROUP

设置为 `TRUE` 会合并密码和组映射中的 `/etc/shadow`、`/etc/password` 文件以及 `/etc/gshadow` 和 `/etc/group` 文件，从而启用影子用户密码和组密码。

`Red Hat`: `TRUE/TRUE`

## 文件位置

`/var/yp/Makefile` 的后续章节指定了标准文件位置；通常你不需要更改它们。`makefile` 的这部分被分为以下几组：

- `Commands`（命令）：定位 `gawk` 和 `make` 并为 `formask` 设置一个值（第 420 页）
- `Source directories`（源目录）：定位包含 NIS 源的目录
- `NIS source files`（NIS 源文件）：定位构建 NIS 数据库的 NIS 源文件
- `Servers`（服务器）：定位列出 NIS 服务器的文件

## all: 目标

`/var/yp/Makefile` 中的 `all:` 目标指定了要为 NIS 构建的映射：

```
all: password group hosts pcs netid protocols mail \
# # netgr shadow publicKey networks bootstrap printcap \
# # amd.home auto.master auto.home local.passwd.adjunct \
# timezone locale netmasks
```

`all:` 目标的第一行列出了默认构建的映射。该行以单词 `all` 开头，后跟着一个冒号 `:` 和一个制表符 `TAB`。由于 `all:` 目标的前三行都以反斜杠 `\` 结尾，因此 `all:` 目标中的四个物理行都是长行的一部分。最后三行物理行被注释掉了。取消行的注释并删除或移动映射，直到列表符合你的需求。

根据你的需求，你可以编辑 `Makefile` 中的 `all:` 目标并在 `/var/yp` 目录下运行 `make`，以修改 NIS 分发的映射列表。

## 启动服务器

在完成上述步骤后，启动服务器以及随后的服务器。使用 `hconfig` 使系统在每次进入多用户模式时启动 `ypserver`，并使用服务立即启动 `ypserver`。更多信息请参阅第 663 页的“前提条件”。

### ypxfrd: 映射服务器

`ypfrd` 守护进程监控从服务器向从用服务器复制大型 NIS 数据库的过程。它允许从用服务器复制映射，避免每个从用服务器都需要复制原始数据然后编译映射。当 NIS 从用服务器收到主服务器有新映射的消息时，它开始从映射服务器读取。

`ypfrd` 守护进程仅在主服务器上运行；没有必要在从用服务器上运行。使用 `hconfig` 配置 `ypxfrd` 在系统每次进入多用户模式时启动，并使用服务立即启动 `ypxfrd`。更多信息请参阅第 663 页的前提条件。

### ypinit: 构建或导入映射

`ypinit` 工具构建或导入 NIS 数据库。在主服务器上，它从 `/etc` 中的 `passwd`、`group`、`hosts`、`networks`、`protocols`、`netgroup` 和 `rpc` 文件中收集信息并构建数据库。在从用服务器上，`ypinit` 从主服务器复制数据库。

你必须通过提供其绝对路径 (`/usr/lib/yp/ypinit`) 来运行它。使用 `m` 选项配置 `/var/yp` 下的域子目录并构建主服务器上的映射；在从用服务器上使用 `master` 选项从主（（服务器）导入映射。在下面的示例中，`ypinit` 询问每个从用服务器的名称；它已经有了主服务器的映射，因为这是一个在系统上运行的命令（示例中为 `peach`）。使用 `CONTROL-D` 和单独的一行结束列表。在你回答对创建的服务器列表的查询后，`ypinit` 会构建 `Makefile`。

```
# /usr/lib/yp/ypinit -m
```

此时，我们已经构建了一个将运行 NIS 服务器的主机列表。`peach` 在 NIS 服务器主机列表中。请继续添加列表，每行一个。完成列表后，输入 `control-D`。

- 下一个要添加主机: `peach`
- 下一个要添加主机: `speed`
- 下一个要添加主机: `CONTROL-D`

当前创建的服务器列表如下：

- `peach`
- `speed`

是否正确？[y/n]: `y`

我们需要几分钟来构建...

NIS 服务器已设置为主服务器。

## 章节总结

NIS（网络信息服务）通过将常用的管理文件维护在中央数据库中，并让客户端联系服务器从数据库中检索信息，从而简化了文件的管理。NIS 所服务的网络称为 NIS 域。每个 NIS 域都有一个主服务器；大型网络可能有多个从服务器。

NIS 提供的信息源于本地配置文件，例如 `/etc/passwd` 和 `/etc/hosts`。这些文件被称为源文件或主文件。在 NIS 能够存储源文件中包含的信息之前，必须将其转换为 `dbm` 格式的文件，这些称为映射（maps）。`ypcat` 和 `ypmatch` 工具用于显示 NIS 映射中的信息。

当你使用 NIS 进行密码身份验证时，`ypasswd` 工具替代了客户端上 `passwd` 的功能。`/etc/ypserv.conf` 文件保存 NIS 服务器配置信息，它指定了 NIS 服务器的选项和访问规则。为了增强系统安全性，你可以创建一个 `/var/yp/securenets` 文件，防止未经授权的系统向 NIS 服务器发送 RPC 请求并检索 NIS 映射。

# 练习题

1. `passwd` 和 `yppasswd` 工具之间有什么区别？
2. 你该如何防止 NIS 将 `root` 用户和其他系统用户导出到客户端？
3. 你该如何让 NIS 用户信息覆盖客户端系统上的本地用户信息？
4. 为什么 `/etc/passwd` 文件需要两个 NIS 映射？

# 高级练习题

5. 你如何使用 NIS 为小型网络镜像私有 DNS 服务器的功能？为什么在大型网络中不应这样使用 NIS？
6. 你该如何判断工作目录是否为 NIS 用户的家目录？
7. 当你将 NIS 与 NFS 使用时，它提供了什么优势？
8. 请一种实现 NIS 映射的方法，使其能够在多个字段上进行索引。

# 22. NFS：共享文件系统

| 本章内容 | |
| :--- | :--- |
| 设置 NFS 客户端 | 676 |
| JumpStart：挂载远程目录层次结构 | 676 |
| 提高性能 | 680 |
| 设置 NFS 服务器 | 682 |
| JumpStart：使用 system-config-nfs 配置 NFS 服务器 | 683 |
| 导出目录层次结构 | 684 |
| automount：自动挂载目录层次结构 | 690 |

NFS（网络文件系统）协议最初由 Sun Microsystems 开发的 UNIX 事实标准，允许服务器与异构网络上的客户端系统共享选定的目录层次结构。NFS 运行在 UNIX、DOS、Windows、VMS、Linux 等等系统上。远程计算机上的文件（文件系统）看起来就像在本地系统（客户端）上一样。文件的物理位置对于 NFS 用户来说是无关的。

NFS 减少了存储需求和系统负载。例如，公司中的每个系统传统上都保留一份应用程序的副本。为了升级程序，管理员需要在每个系统上进行升级。NFS 允许你在单个系统上存储程序的副本，并通过网络让其他用户访问它。这种场景通过减少需要维护相同数据的位置数量，最大限度地减少了存储需求。除了提高效率外，NFS 让网络上的用户能够访问相同的数据（而不仅仅是应用程序），从而提高了数据的一致性和可靠性。通过整合数据，NFS 减少了管理开销并为用户提供了便利。

# 引言

图 22-1 显示了典型的客户端/服务器设置中从客户端到服务器的数据流。NFS 目录层次结构在用户和应用程序看来仅仅是另一个目录层次结构。通过观察它，你无法判断给定目录包含的是远程挂载的 NFS 目录层次结构而不是本地的 `ext3` 文件系统。NFS 服务器将客户端的命令翻译为服务器文件系统的操作。

# 图 22-1 典型 NFS 客户端/服务器设置中的数据流

![](img/0f75ae90508d45878c00a5b098fe29d4_912_0.png)

在许多计算机设施中，用户文件存储在配备大容量磁盘驱动器设备的中央文件服务器上，这些设备可以快速方便地创建数据的备份副本。无盘系统从文件服务器（netboot，下将讨论）、CD 或软盘磁盘启动，并从文件服务器加载系统软件。Linux 终端服务器项目 (`LTSP.org`) 网站上说明了一切：“Linux 为部署从网络服务器启动的无盘工作站提供了极佳的平台。LTSP 的核心是在 Linux 环境中运行客户端计算机。”由于无盘工作站不需要大量的计算能力，你可以通过将它们作为无盘系统使用，让旧的淘汰计算机获得第二次生命。

# Netboot/PXE

你可以对设置适当的系统进行 `netboot`（第 1044 页）。红帽 Linux 包含了用于网络启动启动系统的 PXE（预启动执行环境）服务器包。旧系统有时会使用 `ftp`（简单文件传输协议）进行启动。非 Intel 架构历史上一直包含 `netboot` 能力，红帽 Linux 也支持这种能力。你可以通过构建 Linux 内核，使其通过 NFS 挂载 `root()`。鉴于设置系统的多种方法，你选择的方法取决于你想做什么。更多信息请参阅 *Remote-boot-HOWTO*。

# 无数据系统

另一种类型的 Linux 系统是无数据系统，其中客户端拥有磁盘但不存储任何用户数据。（注：此处原文存在大量重复和损坏，已根据逻辑内容进行处理）。

`df` 工具显示文件系统列表，以及每个文件系统的可用空间。`-h`（人类可读）选项使输出更易于理解。

```bash
df -h
```

| 文件系统 | 大小 | 可用 | 使用率 | 挂载在 |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/sda1` | 985M | 844M | 10% | `grape/gc1` |
| `/dev/sda5` | 3.9G | 738M | 81% | `grape/gc5` |
| `speedy/home` | 3.9G | 14G | 64% | `/` |

# 错误

你可能会丢失对文件的访问。例如，网络问题或远程系统崩溃可能会导致文件临时不可用。当你尝试访问这些远程文件时，你会收到错误消息，例如 `NFS 未响应`。当本地系统可以重新连接远程服务器时，你会看到另一个消息，例如 `NFS 正常`。建立稳定的网络和服务器（或不使用 NFS）是防止此类问题的最佳方法。

## 安全

NFS 基于信任主机范式（第 362 页），因此存在许多困扰此类范式的安全缺陷。此外，NFS 不是加密的。由于这些问题，你应该只在局域网内实现 NFS，这样可以（合理地）确保局域网内的系统确实如它们所称。确保防火墙阻止来自局域网外的 NFS 流量，并且永远不在互联网上使用 NFS。

为了提高安全性，确保 UID 和 GID 在服务器和客户端上相同（页码）。

## 更多信息

Web

`nfs.sourceforge.net`

HOWTO

`NFS HOWTO`

`网络启动与 PXE 远程启动微型 HOWTO`

书籍

`Callaghan` 著，`Addison-Wesley` 出版（1999年12月）

## 设置 NFS 客户端

本节介绍了如何设置 NFS 客户端、挂载目录树以及提高 NFS 性能。

## 前提条件

安装以下软件包：

- `nfs-utils`
- `system-config-nfs`（可选）

为了启用可靠的文件锁定，必须运行 `portmap` 实用程序（`portmap` 软件包的一部分；请参阅 [RPC 网络服务](...) 第 377 页）。

NFS 客户端不需要启动守护进程。

## 快速上手：挂载远程目录层级

要设置 NFS 客户端，请按照挂载本地目录树的方式来挂载远程目录树（第 466 页）。接下来的章节将详细介绍此过程。

## mount: 挂载远程目录层级

示例展示了两种挂载远程目录树的方法，假设 `speed` 与本地系统处于同一网络上，并与本地系统共享 `home` 和 `export`。`speed` 上的 `export` 目录包含两个你想挂载的目录树：`/export/progs` 和 `/export/oracle`。

示例将 `speed` 的 `home` 目录挂载到本地系统的 `speed.home`，将 `export/progs` 挂载到 `apps`，将 `/export/oracle` 挂载到 `oracle`。

首先，使用 `mkdir` 创建作为远程目录树挂载点的目录：

```
# mkdir /speed.home /apps /oracle
```

你可以从导出的目录树中挂载任何目录。在例中，`speed` 导出 `export`，而本地系统导出 `/export/progs` 和 `/export/oracle`。以下命令手动挂载一次这些目录树：

```
# mount speedy:/home /speedy.home
# mount -o ro,nosuid speedy:/export/progs /apps
# mount -o ro speedy:/export/oracle /oracle
```

如果你收到错误 `mount: RPC: Program not registered`，可能意味着服务器上没有运行 NFS。

默认情况下，目录树是以读写模式挂载的，即 NFS 服务器以读写权限导出它们。以下命令的第一条通过 `speedy` 将 `/home` 目录树挂载到本地目录 `speedy.home`。第二条和第三条命令使用 `ro` 选项强制进行只读挂载。第二条命令添加了 `nosuid` 选项，该选项强制使挂载目录树中的 `setuid`（第 183 页）可执行文件在本地系统中以普通权限运行。

### nosuid 选项

如果用户具有运行 `setuid` 程序的能力，该用户就拥有超级用户的权限。这种能力应该受到限制。除非你确定用户需要从挂载的目录树中运行具有 `setuid` 权限的程序，否则请始终使用 `nosuid` 选项挂载目录树。例如，当无盘工作站使用 NFS 挂载根分区时，你需要挂载一个具有 `setuid` 权限的目录树。

### nodev 选项

挂载设备文件会产生另一个潜在的安全漏洞。虽然最佳策略是不挂载不可信的目录树，但并非总是能实现这一策略。除非用户需要使用挂载目录树上的设备，否则请使用 `nodev` 选项挂载目录树，这可以防止挂载目录树上的字符和块特殊文件（第 463 页）被当作设备。

### fstab 文件

如果你频繁挂载目录树，可以将目录树的条目添加到 `/etc/fstab` 文件（第 681 页）。（或者，你可以使用 `automount`；参见第 690 页）。以下 `/etc/fstab` 条目会在系统挂载文件系统的同时，挂载与之前示例相同的目录树。

```
$ cat /etc/fstab

speedy:/home          /speedy.home  nfs r,nosuid 0 0
speedy:/export/progs /apps     nfs r,nosuid 0 0
speedy:/export/oracle /oracle nfs r 0 0
```

使用 NFS 挂载的文件在本地系统中始终是有类型的，无论它在远程系统的什么位置。通常，你不会对备份的 NFS 目录树运行 `fsck`。`fstab` 第一类、第三类和第五类的条目通常是 `nfs`（文件系统类型）、`0`（不备份此目录转储 [545]）以及在该目录树上的 `0`（不拒绝 [470]）。挂载 NFS 目录树的选项与挂载 `ext3` 或其他类型的文件系统的选项不同。详情请见下一节。

## umount: 卸载远程目录层级

使用 `umount` 卸载远程目录的方法与卸载本地文件系统的方法相同（第 469 页）。

## mount: 挂载目录树
