
`verify(8)` 实用程序可以使用 `"-a"` 选项在活动域上运行。这允许在集群处于运行状态时检查 `cluster_root` 域。这是一个重大消息，因为通常 `verify` 会在没有挂载文件集的域上运行。以下示例显示了 `verify` 命令在 `cluster_root` 域（活动域）上运行。注意，由于域当前处于活动状态，下面输出中会报告一些多余的错误（以粗体显示）。

## CAUTION:

`verify -a` 命令应仅在作为该域的 CFS 服务器的成员上运行。

域的 CFS 服务器可以从 `cfsmgr(8)` 命令的输出中得知。

```
# cfsmgr /
Domain or filesystem name = /
Server Name = molari
Server Status : OK
```

```
# showfdmn cluster_root
Id          Date Created      LogPgs Version Domain Name
3be01cb1.000be1e0 Wed Oct 31 10:45:53 2001 512 4 cluster_root
Vol 512-Blks Free % Used Cmode Rbks Wbks Vol Name
1L 401408 165040 59% on 256 256 /dev/disk/dsk3b
```

```
# df /
Filesystem     512-blocks Used Available Capacity Mounted on
cluster_root#root 401408 215962 165040 57% /
```

```
# /sbin/advfs/verify -a cluster_root
+++ Domain verification +++
Domain Id 3be01cb1.000be1e0
Checking disks ...
Checking storage allocated on disk /dev/disk/dsk1b
Checking mcell list ...
Checking that all in-use mcells are attached to a file's metadata mcell chain...
Checking tag directories ...
Found 2 references to files that cannot be found in any directory.
Most likely this is from file activity on the active domain.
+++ Fileset verification +++
++++ Fileset root ++++
Checking frag file headers ...
Checking frag file type lists ...
Scanning directories and files ...
100
Scanned 175 directories.
Scanning tags ...
2100
Scanned a total of 2146 tags.
Searching for lost files ...
Creating //lost+found
2100
Found 4 lost files out of 2146 checked.
Most likely this is from file activity on the active domain.
```

在不太可能的情况下，集群成员在 `verify` 命令活动时发生故障，导致文件集处于无法挂载状态，不要绝望。检查 `/etc/fdmns/domain_name/fset[0-9]_verify_identifier` 下找到的临时挂载点，其中 `identifier` 是 `verify` 实用程序选择的唯一 id。卸载并删除这些挂载点，您应该又恢复正常。这些奇怪的挂载点之所以遗留下来，是因为 `verify` 在操作中途被中断，其临时挂载被切换到另一个成员。（这不会发生在独立系统上。）

当一个以前是独立的节点被添加到现有集群时，没有神奇的方法让其域被识别并使其文件系统被挂载。好吧，也许该机制有点神奇。考虑到诸如 `verify`、`defragment(8)`、`salvage(8)`、`advscan(8)`、`fixfdmn(8)` 等命令所完成的工作，总是令人惊叹，这些命令是省力的（有时是保工作的）实用程序。新成员的 AdvFS 文件系统必须在 `/etc/fstab` 文件中体现，该文件由所有集群成员共享。让域被识别可以通过两种方式完成：手动在 `/etc/fdms` 下为新域名称创建目录条目，然后创建指向域卷的符号链接；或使用（有点神奇的）`advscan` 命令，该命令搜索 AdvFS 分区，并在适当时在 `/etc/fdms` 中创建条目。

`verify` 实用程序以特殊方式处理 `cluster_root` 域。正如我们所讨论的，如果使用 `"-a"` 选项调用，实用程序可以在文件系统挂载时检查根文件系统的完整性。但在使用 `"-a"` 选项时，强大的修复选项 `"-f"` 和 `"-d"` 是不可用的。所以你手头有一个来自 `verify` 的精彩报告，指出存在多个元数据错误，你希望该实用程序（足够智能，可以判断域的元数据存在问题）能够更进一步，尽力修复这些问题。在正常情况下这不是什么大问题，因为目标域上没有挂载文件系统，因此 `verify` 可以随心所欲地处理元数据。但当 `cluster_root` 是问题域时，我们遇到了棘手的情况，因为 `cluster_root` 文件系统已挂载，无法卸载，否则将失去对几乎所有东西的访问，包括 `verify` 命令本身。

在这种情况下，您必须启动“紧急修复”磁盘，它可以是初始集群成员的系统磁盘。启动后，您可以让 `verify` 尝试修复 `cluster_root` 域，或从备份存储中恢复该域。

### 19.4.2 事件管理器

事件管理器（EVM）支持集群范围的事件。某些事件将具有 `cluster_event` 属性。如果该属性设置为 `false`，事件将仅发布在生成该事件的成员上；否则它将发布在所有集群成员上。CAA、CFS、CLUA、CNX 和 DRD 集群子系统具有 EVM 模板。

事件管理器在第 8 章中讨论，`cluster_event` 属性在第 12 章中介绍。

### 19.4.3 打印

连接到集群成员的打印机可以被其他集群成员访问。

使用 `lprsetup(8)` 时，将会出现额外的 `on` 属性，用于指示哪个集群成员与打印机有物理连接。`/etc/printcap` 文件不是 CDSL，因此由所有集群成员共享。以下输出显示了新的 `on` printcap 选项的使用情况，然后显示了在 `lprsetup` 中输入 `?` 时在提示输入 `on` 字符串时可获得的信息。

```
# grep ':on' /etc/printcap
:on=molari:\
```

```
# lprsetup

Tru64 UNIX Printer Setup Program

Command < add modify delete exit view quit help >: m
```

正在修改打印机条目，输入 '?' 获取帮助。

输入要修改的打印机名称（或输入 view 查看 printcap 文件）：lp0

输入要更改的符号名称。

输入 'p' 打印当前值，输入 'l' 列出所有 printcap 值，或输入 'q' 退出。

输入符号名称：on

babylon5 集群中有 3 个节点。

是否要查看集群成员节点名列表（y/n）？ y

| 成员 ID | 成员主机名 |

|-----------|-----------------|

| 1         | molari          |

| 2         | sheridan        |

| 3         | ivanova         |

为符号 'on' 输入新值？ [molari] ？

`on` 参数指定 on-list，即被授权为假脱机队列运行队列守护进程的一个或多个集群成员节点名列表。on-list 字符串的格式如下面的示例所示：

```
on=localhost: \
on=node1: \
on=node1,node2,node3: \
```

如果未指定此参数，则默认假定为 `localhost`。

on-list 中节点的顺序（从左到右）指定了从最高到最低的优先级，成员节点父打印守护进程将使用该优先级来确定由哪个成员节点运行队列守护进程。

如果指定了 `localhost`，则所有成员节点都将被授权运行队列守护进程。实际运行它的节点由第一个在此队列为空时向队列提交作业的节点决定。

在集群中，仅对于使用 TCP 连接的打印机，才应指定 `localhost` 或不指定值。

如果设备连接到属于多节点集群一部分的节点，则连接到 `/dev/` 目录中所指定设备的打印机必须指定 on-list。如果集群仅包含一个节点，建议指定 on-list。

对于非集群的独立主机，是否使用指定本地主机名或 'localhost' 的 on-list 是可选的。

输入新值，或按 RETURN 使用默认值。
