

Heartbeat 集群更倾向于不进行故障回切，即使 node1 恢复，node2 仍将是集群的活动节点。要测试故障回切，只需重启 node2 并观察磁盘切换到 node1 即可。

NOTE 要创建复制磁盘、容错的 Samba 或 NFS 集群而不是 Apache 集群，只需在两个节点上正常安装并配置 Samba 或 NFS 并共享 /mnt/shared 目录。然后根据使用的服务，将 /etc/ha.d/haresources 中的 apache2 替换为 samba 或 nfs-user-server，这样它将启动或停止这些 init 脚本而不是 apache2。你甚至可以在同一台机器上同时设置 Samba 和 NFS，并在 haresources 中同时列出 samba 和 nfs-user-server。

## drbdadm 磁盘管理

一旦你拥有一个可用的 DRBD 磁盘，drbdadm 就是你管理磁盘资源的主要工具。DRBD init 脚本应该负责初始化你的资源，但你可以使用

```
$ sudo drbdadm up r0
```

启动资源，将 r0 替换为你想要启动的资源名称。同样，你也可以使用以下命令关闭非活动资源

```
$ sudo drbdadm down r0
```

你也可以手动更改节点是处于主模式还是次模式，虽然在 Heartbeat 集群中我建议让 Heartbeat 来处理此事。如果你确实决定从主模式切换到次模式，请先卸载磁盘。另外，如果任何节点当前是主节点，DRBD 在节点连接时（/proc/drbd 中的 cs 值）不会让你将其更改为次模式，因此你必须先将它们彼此断开连接。要为特定资源手动设置主模式或次模式，运行

```
$ sudo drbdadm primary r0
$ sudo drbdadm secondary r0
```

## CHANGE DRBD.CONF

在某个时候你可能想要在 /etc/drbd.conf 文件中进行更改，例如更改脑裂恢复模式。每当你进行更改时，请确保相同的更改已添加到所有节点上的 /etc/drbd.conf 中，然后在两个节点上运行

```
$ sudo drbdadm adjust r0
```

将 r0 替换为你想要更改的资源名称。

## REPLACE A FAILED DISK

理想情况下，你用于 DRBD 的磁盘应设置在某种 RAID 中，以便磁盘故障不会导致节点宕机。如果你像本示例中一样将 DRBD 磁盘设置在单个驱动器上并且驱动器故障，你将需要运行几个命令来添加新的驱动器。在本示例中我假设 /dev/sdb 在我的 node1 服务器上故障。首先，默认情况下 DRBD 应该在磁盘发生故障时自动分离并移除磁盘，因此除非你有意调整了该默认值，否则 DRBD 应该为你完成这项工作。一旦你添加并分区了替换驱动器（在我的例子中它将是 /dev/sdb1），然后你首先需要在 /dev/sdb1 上重新创建内部元数据，然后附加资源：

```
$ sudo drbdadm create-md r0
$ sudo drbdadm attach r0
```

## MANUALLY SOLVE SPLIT BRAIN

DRBD 会尝试自动解决脑裂问题，但有时它无法确定哪个节点应覆盖另一个节点。在这种情况下，你可能有两个节点都已挂载其 DRBD 磁盘并正在写入它。如果发生这种情况，你必须决定哪个节点具有你想要保留的数据版本。假设在我的例子中 node1 和 node2 发生了脑裂并已彼此断开连接。我决定 node2 具有最新数据，应成为主节点并覆盖 node1。在这种情况下我必须告诉 node1 丢弃其数据，所以我去 node1，确保任何 DRBD 磁盘已卸载，然后输入

```
$ sudo drbdadm secondary r0
$ sudo drbdadm -- --discard-my-data connect r0
```

如果 node2 已经处于 WFConnection 状态，它将自动在此时重新连接到 node1。否则我需要去 node2，即具有良好数据的节点，并输入

```
$ sudo drbdadm connect r0
```

现在 node2 将同步其数据到 node1。

这些步骤应该能让你使用坚固的复制磁盘运行集群。有关 DRBD 的更详细信息，包括我在此处列出的更高级的集群选项，请访问官方网站 www.drbd.org。

